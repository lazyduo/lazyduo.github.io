---
title: "Scroll-To-Top 버튼 만들기"
date: 2021-05-01 23:04:00 +0900
toc: true
toc_sticky: true
tags:
    - tech
    - ETC
    - Github_Pages
---
현재 제 페이지는 Minimal Mistakes 템플릿을 사용 중입니다. 포스팅이 길어 지면 위로 돌아가는 버튼이 있으면 좋겠다는 생각이 많이 들어서 그 방법을 찾아 보았습니다.

아래에 잘 정리되어 있는 것 같아 천천히 따라해 볼 생각입니다.

[Add Scroll-To-Top Button to a Website](https://jun711.github.io/web/adding-scroll-to-top-button-to-a-website/)

## 결과

일단 원하는 모양으로 만들기 성공했습니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/scroll-to-top.png){: .align-center}

기존에는 `hover`할 때 굳이 필요없는 모션이 있었고, 청록색으로 화살표가 변하는게 마음에 들지 않았습니다. 깔끔을 추구하는(?) 제 페이지 스타일이랑 이게 더 잘 어울리는 것 같습니다.

굉장히 만족 스럽습니다!!

## 방법 정리

제가 구현한 방법 소개합니다. 일단 위 링크의 `jun711`의 jun711.github.io에서 큰 도움을 받았습니다. 같은 템플릿 minimal-mistakes를 사용중이라 보다 쉽게 할 수 있었습니다.

수정 및 추가가 필요한 부분은 총 4 부분입니다.

- `_includes/footer/custom.html`
- `assets/css/main.scss`
- `assets/css/js/scroll-to-top`
- `_config.yml`

### 1. 아이콘 만들기

우선 `_includes/footer/custom.html`를 만들고, 여기에 아이콘을 만들어 넣습니다.

fa-icon 사용법은 따로 정리해 두었습니다. 참고로 `<i>` 태그 마지막 부분(circle, up-arrow)은 'name' 개념입니다.

- [fa icon 사용법](https://lazyduo.github.io/fa-stack/)

```html
<!-- start custom footer snippets -->
<div id='scroll-to-top'>
    <span class='fa-stack fa-lg'>
        <i class='fa fa-circle fa-stack-2x circle'></i>
        <i class='fa fa-angle-double-up fa-stack-1x fa-inverse up-arrow'></i>
    </span>
</div>
<!-- end custom footer snippets -->
```

### 2. Style 지정

`assets/css/main.scss`에 scroll-to-top 관련 스타일을 추가 합니다. 이 때, 앞에서 했던 `custom.html`에서의 div **id**를 그대로 사용하는 것에  유의 합니다.

저는 jun711님의 세팅을 거의 그대로 사용하였고, 마우스를 올려 놨을 때 움직이는 액션이 싫어서 `:last-child`의 `active, hover` 부분을 주석 처리하였습니다. 움직이는 모션을 원하시면 주석 풀면 됩니다. 또한, 청록색의 색깔 변화 대신 바깥 원이 투명->반투명으로 보이도록 `#scroll-to-top span`의 color와 `active, hover`부분의 color를 조정해주었습니다. `.circle`은 위의 `custom.html`에서 `<i>`태그에서 이름 지정한 그 이름입니다.

```scss
#scroll-to-top {
    display: block;
    position: fixed;
    font-size: 21px;
    @media (max-width: 600px) {
        font-size: 20px;
    }
    bottom: 25px;
    right: 10%;
    @media (max-width: 600px) {
        right: 5%;
        bottom: 15px;
    }
    
    opacity: 0;
    z-index: 99;
    text-align: center;
    
    :last-child {
      transition: transform 0.7s ease-in-out;
      
    //   &:active, &:hover {
    //      transform: translateY(-10%);
    //   }
    }
    transform: translateY(30%);
    transition: transform 0.5s ease-in-out, opacity 0.5s ease-in-out;
}


#scroll-to-top span {
    cursor: pointer;
    color: #1a1d243f;

    &:hover, &:active {
        .circle {
            color: #1a1d24;
        }
    }
}
```
### 3. 자바스크립트 추가하기

`assets/css/js/`에 `scroll-to-top.js`파일을 추가합니다. 물론 js를 잘 모르기 때문에 jun711님거 그대로 사용했습니다. 내용은 스크롤 제어권을 갖고 스크롤을 위로 올리는 동작, 특정 위치 아래로 내릴때 나타나도록하고, 매끄럽게(smooth) 스크롤을 올리고 하는 것들입니다.

- [scroll-to-top.js](https://github.com/lazyduo/lazyduo.github.io/blob/master/assets/js/scroll-to-top.js)

### 4. _config.yml에 등록하기

마지막으로 `config.yml`에 위에서 만든 자바스크립트를 `head_scripts`로 등록해주면 됩니다. (아래 아무곳이나 추가해주면 됩니다) 그러면 모든 페이지에 아까 만든 js가 등록되게 되는 겁니다.

```yml
# JavaScript
head_scripts:
  - /assets/js/scroll-to-top.js
```

끝.