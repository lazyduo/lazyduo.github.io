---
title: "Tech > Project LOLHUB > Thumbnail Generator"
layout: tag
taxonomy: thumbnail
classes: wide
author_profile: false
sidebar:
    nav: "tech"
---

## 개요

원하는 스타일의 Youtube Thumbnail을 생성해주는 App 입니다. Python PIL 라이브러리로 Image Processing 했습니다. 비록 완전히 정해진 스타일 안에서만 만들 수 있다는 단점이 있지만, 채널 운영자라면 고정된 스타일을 만들어 놓고 사용하면 편리할 것 입니다. (물론 스타일을 코딩해야되는 것은 사용자 몫입니다)

- 예시

<figure class="half">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-1.jpg">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-2.jpg">
</figure>

이 페이지에서는 이 썸네일 생성기를 어떻게 만들었는지 그 과정을 다루도록 하겠습니다. 기억 되살리는 중...

## PIL(pillow) 시작하기

Python Imaging Library 사용을 위해 pillow를 설치한다. PIL은 Python 2 시절의 라이브러리이고 이걸 fork한게 pillow라고 보면 된다. (결국 같은거)

```console
$ pip install pillow
```

### Image Module

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

mask = Image.open('/home/upoque/lol_hub_storage/data/resource/asset/'
    'black_gradation.png').convert('RGBA')

bg_cropped.paste(mask, (0, 0), mask)
```

Youtube 썸네일의 경우 권장 사이즈가 `(1280, 720)`이기 때문에 `Image`를 받는 동시에 `Image.crop(box=None)`으로 잘라 주었다. Argument인 box는 절대 위치를 (left, upper, right, lower) tuple로 받기 때문에 원본 이미지의 중심에서 권장 사이즈를 잡도록 처리하였다.

`Image.paste(im, box=None, mask=None)`는 Image에 im Image를 붙여 넣어준다. 주의 할 점은 원본과 붙일 Image의 `mode`(RGB, RGBA 등)가 맞아야 한다. 이게 맞지 않으면 전혀 동작하지 않는다. 여기서는 mask 기능을 이용해서 원본 이미지에 검은색 수평 그라데이션을 입혀서 아래쪽을 어둡게 하는 효과를 주었다.

mask 시킬 검정색 투명 그라데이션 이미지를 따로 준비한다. 이때, 투명도가 있는 이미지 이므로 `Image.convert('RGBA')`로 RGBA mode로 이미지를 맞춰 준다. 준비한 이미지를 paste하면서 self mask처리를 하면 원본 이미지에 영향을 받지 않도록 이쁘게 입힐 수 있다.

`bg_cropped.paste(mask, (0, 0), mask)` !!!

특히, 배경이 투명한 png 이미지들을 깔끔하게 붙여 넣기위해서 이 방법이 정말 많이 쓰였다.

- 배경에 어두운 그라데이션이 입혀진 것을 확인 할 수 있다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/thumbnail-sample-1.jpg){: .align-center}





