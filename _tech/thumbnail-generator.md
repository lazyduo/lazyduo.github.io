---
title: "Tech > Project LOLHUB > Thumbnail Generator"
classes: wide
author_profile: false
toc: true
toc_sticky: true
sidebar:
    nav: "tech"
categories: project
tags:
    - lolhub
---

## 개요

원하는 스타일의 Youtube Thumbnail을 생성해주는 App 입니다. Python PIL 라이브러리로 Image Processing 했습니다. 비록 완전히 정해진 스타일 안에서만 만들 수 있다는 단점이 있지만, 채널 운영자라면 고정된 스타일을 만들어 놓고 사용하면 편리할 것 입니다. (물론 스타일을 코딩해야되는 것은 사용자 몫입니다)

- 구현 웹 화면

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-main.png){: .align-center}

유저가 title, subtitle, tag를 입력하고, 추천한 이미지 중에서 원하는 배경 이미지를 선택하면 지정된 썸네일 preset으로 썸네일을 만들어 줍니다.


## PIL(pillow) 시작하기

Python Imaging Library 사용을 위해 pillow를 설치한다. PIL은 Python 2 시절의 라이브러리이고 이걸 fork한게 pillow라고 보면 된다. (결국 같은거)

```console
$ pip install pillow
```

자세한 모듈 사용법은 아래 링크를 참고하면 된다.

- [pillow docs](https://pillow.readthedocs.io/en/stable/reference/index.html)

## Image Module

이미지 객체를 받는다고 보면된다. 도화지를 가져오는 셈이다. 썸네일 생성을 위해 `Image.open('file_path')`를 이용해서 배경이미지를 불러오고 그 위에 다른 이미지들을 얹는 형태로 구현 했다.

```python
size = (1280, 720)
orig = (1920, 1080)

background = Image.open('background_path').convert('RGBA')
bg_cropped = background.crop((
    orig[0] / 2 - size[0] / 2,  # left
    orig[1] / 2 - size[1] / 2,  # top
    orig[0] / 2 + size[0] / 2,  # right
    orig[1] / 2 + size[1] / 2))  # bottom

mask = Image.open('mask_path`).convert('RGBA')

bg_cropped.paste(mask, (0, 0), mask)
```

Youtube 썸네일의 경우 권장 사이즈가 `(1280, 720)`이기 때문에 `Image`를 받는 동시에 `Image.crop(box=None)`으로 잘라 주었다. Argument인 box는 절대 위치를 (left, upper, right, lower) tuple로 받기 때문에 원본 이미지의 중심에서 권장 사이즈를 잡도록 처리하였다.

`Image.paste(im, box=None, mask=None)`는 Image에 im Image를 붙여 넣어준다. 주의 할 점은 원본과 붙일 Image의 `mode`(RGB, RGBA 등)가 맞아야 한다. 이게 맞지 않으면 전혀 동작하지 않는다. 여기서는 mask 기능을 이용해서 원본 이미지에 검은색 수평 그라데이션을 입혀서 아래쪽을 어둡게 하는 효과를 주었다.

mask 시킬 검정색 투명 그라데이션 이미지를 따로 준비한다. 이때, 투명도가 있는 이미지 이므로 `Image.convert('RGBA')`로 RGBA mode로 이미지를 맞춰 준다. 준비한 이미지를 paste하면서 self mask처리를 하면 원본 이미지에 영향을 받지 않도록 이쁘게 입힐 수 있다.

`bg_cropped.paste(mask, (0, 0), mask)` !!!

특히, 배경이 투명한 png 이미지들을 깔끔하게 붙여 넣기위해서 이 방법이 정말 많이 쓰였다.

- 배경에 어두운 그라데이션이 입혀진 것을 확인 할 수 있다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-1.jpg){: .align-center}

- 응용으로 사선 방향으로 이미지들 마스크 시켜 표현한 모습

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-2.jpg){: .align-center}

위 이미지 같은 경우는 사선으로 잘린 mask를 위치마다 만들어서 하나하나 추가하면서 그렸다. 챔피언 이미지를 랜덤으로 받아오는거는 단순히 지정된 asset 폴더에서 `random` 함수로 얻어 오게 구현 한 것이다. (Riot이 모든 챔피언 및 스킨 이미지를 다 제공해준다)
## ImageDraw Module

주어진 배경 이미지 위에 2D 그래픽 이미지를 그릴 수 있도록 해준다. 이 모듈로 추가적인 디테일을 주었다. 외곽 테두리를 그리거나 사각형 이미지를 넣을 때 주로 사용하였다.

쉽다. `draw = ImageDraw.Draw(im)`으로 '어디에' 그릴 것인지 핸들을 받고, `ImageDraw.rectangle()` 등으로 그리면 된다. `fill, outline, width`등 추가 parameter를 받는다.

```python
def overlay_square(self, im, color, area_size):
    draw = ImageDraw.Draw(im)
    draw.rectangle(
        area_size,
        fill=color
    )
    return
```

`ImageDraw.text()` 글씨를 써보자. 시작 위치를 지정해주고, 내용, font, fill(color)를 지정해서 텍스트를 입힐 수 있다.

```python
def overlay_title(self, im, title_text, text_start, text_size, font):
        draw = ImageDraw.Draw(im)
        _font = ImageFont.truetype(font, text_size)
        draw.text(text_start, title_text, font=_font, fill='#f1f6e3')
        return
```

font를 받아오는 방법은 아래에 다루겠다.

## ImageFont Module

`Image.truetype(font, size)`로 font object를 생성하고, `ImageDraw.text()`와 함께 사용하여 text를 그릴 수 있다.

사용시 주의할 점은 딱 한가지다. font의 절대경로 위치를 넣어 주어야 한다. font의 실제 위치가 다르면 동작하지 않으니 주의하자.

```python
font = os.path.join(self.font_dir, 'Mont-HeavyDEMO.otf')
text_size = 130

_font = ImageFont.truetype(font, text_size)
```

## Save

3번 preset을 만드는 과정을 참고할 수 있도록 script 첨부하였다. 배경화면, 배너, Title, Sub-Title 순서대로 이미지를 만들고, 마지막에 RGB로 mode convert 후 저장할 수 있도록 했다.

`Image.save('path' + 'filename')`

```python
def make_thumbnail_3(self, **kwargs):
    # background
    thumbnail_background_path = kwargs['thumbnail_background_path']
    background = self.get_background_image_3(thumbnail_background_path)

    # banner
    thumbnail_banner = os.path.join(self.banner_dir, self.logo_name)
    self.overlay_banner(background, thumbnail_banner)
    self.log.debug('thumbnail banner : complete')

    # Title
    title_text = kwargs['thumbnail_title']
    title_font = os.path.join(self.font_dir, 'GmarketSansBold.otf')
    text_start = (71, 486)
    text_size = 85
    self.overlay_title(background,
        title_text, text_start, text_size, title_font)
    self.log.debug('thumbnail title : complete')

    # Sub-Title
    subtitle_font = os.path.join(self.font_dir, 'Recipekorea.ttf')
    subtitle_text = kwargs['thumbnail_subtitle']
    text_start = (78, 591)
    text_size = 50
    self.overlay_subtitle_2(background, subtitle_text,
        text_start, text_size, subtitle_font)
    self.log.debug('thumbnail subtitle : complete')

    # save
    result = background.convert('RGB')
    filename = os.path.join(self.thumbnail_dir,
        kwargs['vid_thumbnail_path'])
    result.save(filename)
    self.log.info('saved thumbnail to: ' + str(filename))
    return filename.split('/')[-1]
```

## 마치며

PIL 모듈 다룰 줄만 알면 나머지는 다 수작업이라 생성 기능 만드는거 자체는 어렵지 않다. 나 같은 경우 포토샵으로 미리 프리셋을 만들어 놓고, 그거랑 최대한 비슷하게 PIL을 통해 만들려고 노력했다. pixel 단위로 조정하는 세밀함은 필수! 

사실 기능 자체보다 Django랑 연결하고, 여런 html 페이지 연동시키고, 버튼 만들고 jQuery ajax 만들고 하는게 더 어려웠다. 프론트 엔드랑은 안맞는것인가?!

(현재 서버 이전을 해 놔서 다시 연결시켜 Django Web으로 돌리기 어려운 상태라.. 복기하는데 애를 좀 많이 먹었네요)

