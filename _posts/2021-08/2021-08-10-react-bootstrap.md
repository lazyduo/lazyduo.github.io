---
title: "React - Bootstrap - Reactstrap"
date: 2021-08-10 08:59:00 +0900
classes: wide
tags:
    - tech
    - yumi
    - react
    - memo
    - web design
---

`YUMI Project`를 시작할 때는 Django를 더 많이 쓰겠지 했는데, 우리가 `React`를 활용한 Front End 작업을 맨땅에 헤딩하다 보니 새롭게 접하는 것들이 많았습니다.

이번에는 `Redux`나 `Hooks` 같이 기술적인 부분이 아니라 오로지 '디자인'적인 부분에 관해 살펴봅니다.

# 들어가기 앞서
## Sass (scss)

`Sass(Syntatically awesome stylesheets)` 기존의 'css'의 단점을 보완한 스크립트 언어이다. 프로젝트가 커짐에 따라 스타일 시트도 관리가 필요해지는데, 관리하는데 있어 매우 유용한 variable, nesting, mixini, inheritance 등의 개념이 추가 되었다. 이 sass는 기존의 css와는 문법이 약간 다른데, css와 완전히 호환되도록 새로운 구문을 도입한 것이 `scss`라고 한다. 요즘 프로젝트에서는 sass를 쓰기 위해 전부 `.scss`를 사용하는 것으로 보인다.

`scss`에서는 우리 프로젝트 structure에서 'src > assets > scss' 에서 확인할 수 있듯이 꽤나 심플하게 관리되고 있음을 알 수 있다. '.scss'는 약속으로 파일명에 `_` 언더바를 붙여서 쉽게 import한다.

```scss
@import "/scss/variables";
```

위 처럼 import를 하면 scss 디렉토리 하위의 '\_variables.scss' 파일을 자동으로 인식하게 된다.

보통의 scss를 사용하는 프로젝트들은 이렇게 'variables' 파일을 따로 두어 '\$'로 구분 하는 변수들을 전부 설정하여 모든 스타일 시트에 쉽게 적용할 수 있도록 사용하는 것으로 보인다.

```scss
// _variables.scss

$header-height: 70px;
$header-bg: #ffffff;
$header-item-color: #555b6d;
```

(header 관련된 변수들을 설정한 모습)

## Bootstrap

FE Engineer가 아니더라도 한 번 쯤 들어봤을 법한, `Bootstrap`. Bootstrap은 responsive, mobile-first 사이트를 만들기 위한 가장 유명한 'CSS Framework'이다. 트위터 개발자들이 만들었고, 오픈소스로 많은 개발자들이 기여하며 지금의 부트스트랩이 탄생했다. 웹 사이트 제작에 필요한 여러 Layout, Content, Forms, Componenets 등을 제공하여, 개발자들이 따로 기능들을 만들지 않고 부트스트랩에서 이미 잘 정형화 되어 있는 feature 들을 가져와서 쉽고 빠르게 개발 가능하다.

웹사이트에서 비슷비슷하게 보이는 버튼들, Dropdown, 사이드바 이런 것들 전부 Bootstrap의 도움을 받았다고 보면 된다.

`YUMI Project`에서도 bootstrap을 customize하여 사용하고 있다.

```js
<div className="page-title-box d-flex align-items-center justify-content-between">
```

bootstrap의 class를 이용하여 diplay: flex, align-items: center, justify-content: space-between 을 적용한 모습.
(react에서는 class를 적용할 때 'className'으로 적용하는 것을 주의하자)

# Reactstrap !

이제 `React`에서 `Bootstrap`을 쉽게 사용해 보자. `reactstrap`은 React의 컴포넌트 개념을 살려서 Bootstrap의 feature들을 사용한다고 보면 된다.

예를 들어, 'Dropdowns' 같은 경우, 기존의 Bootstrap에서는 아래와 같이 class에 bootstrap class들을 추가하여 dropdown, dropdown-menu, dropdown-item을 관리하는 것을 볼 수 있는데, reactstrap에서는 각각을 Component 형태로 불러와서 사용함을 알 수 있다.

- Bootstrap
{% raw %}
```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
    Dropdown button
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
    <li><a class="dropdown-item" href="#">Something else here</a></li>
  </ul>
</div>
```
{% endraw %}

- Reactstrap

```react
import React, { useState } from 'react';
import { Dropdown, DropdownToggle, DropdownMenu, DropdownItem } from 'reactstrap';

const Example = (props) => {
  const [dropdownOpen, setDropdownOpen] = useState(false);

  const toggle = () => setDropdownOpen(prevState => !prevState);

  return (
    <Dropdown isOpen={dropdownOpen} toggle={toggle}>
      <DropdownToggle caret>
        Dropdown
      </DropdownToggle>
      <DropdownMenu>
        <DropdownItem header>Header</DropdownItem>
        <DropdownItem>Some Action</DropdownItem>
        <DropdownItem text>Dropdown Item Text</DropdownItem>
        <DropdownItem disabled>Action (disabled)</DropdownItem>
        <DropdownItem divider />
        <DropdownItem>Foo Action</DropdownItem>
        <DropdownItem>Bar Action</DropdownItem>
        <DropdownItem>Quo Action</DropdownItem>
      </DropdownMenu>
    </Dropdown>
  );
}

export default Example;
```
