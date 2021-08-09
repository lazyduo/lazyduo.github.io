---
title: "React - YUMI의 흔적들"
date: 2021-07-20 13:46:00 +0900
classes: wide
tags:
    - tech
    - yumi
    - react
    - memo
    - web design
---

`YUMI PROJECT`를 위해 처음으로 `Django`나 `Flask`와 같은 web Framework의 Template에서 벗어나, `React`를 이용해서 Frontend 작업을 하기로 하였다. 물론 아무것도 모르니 이번에도 맨땅에 헤딩하면서 만들고 있다.

그래도 이전에 tuorial이나 JS가 아예 친숙하지 않은건 아니라서 나름 잘하고 있는듯??

이 글은 순수하게 공부한 내용 메모의 용도입니다.

## Form

React Hook 중 하나인, `useRef`를 이용해서 Form을 만든다.

일단 개요는 'form' 태그에서 onSubmit props를 만들고, 이 때 연결되는 함수에서 JS 'event' 객체를 이용하여 원래의 바닐라 JS의 form 기능이 발생하지 않도록 아래 method로 방지한다.

`event.preventDefault();`

그 후, 'input' 태그에 `ref`라는 props를 추가해주고, 이 값은 `useRef()`와 연동한다.

이렇게 하면 현재의 input 값을 `titleInputRef.current.value` 형태로 받아올 수 있다.
