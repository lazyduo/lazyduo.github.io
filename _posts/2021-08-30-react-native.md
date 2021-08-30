---
title: "React Native"
date: 2021-08-30 17:20:00 +0900
classes: wide
tags:
    - tech
    - yumi
    - react
    - react native
    - memo
    - web design
---

이제 `YUMI` 프로젝트도 모바일 앱으로 전환 시킬 날이 다가오고 있습니다. 아무래도 Frontend가 React 기반이다 보니, `React Native`로 모바일 앱을 개발하려고 합니다.

React Native는, iOS와 Android 각각에 앱을 만들 필요 없이, 하나의 개발로 두 플랫폼에서 호환 가능한 앱을 만드는 하이브리드형(?) 모바일 프레임워크입니다. 이 부분이 가장 큰 장점이 될 수도 있고, 단점이 될 수 있는데, 아무래도 Native Language인 iOS의 `Swift`, Android의 `Kotlin`에 비해 각 플랫폼의 장점을 최대한 활용을 못한다는 점이 단점으로 작용합니다.

근본적인 이유는 어쨋든 iOS와 Android는 다르기 때문입니다!

여하튼 YUMI 프로젝트는 React Native로 모바일 앱을 만들기로 결정하였고, 이제 공부를 시작해야하는 상황입니다...

여기서는 공부하는 과정에서 도움이 될 것 같아 메모하는 느낌으로 작성합니다.

유튜브 튜토리얼 참고 [Link](https://www.youtube.com/watch?v=0-S5a0eXPoc)

## Android, iOS 호환 문제

플랫폼 차이로 Android에서는 동작하고, iOS에서는 동작하지 않거나 혹은 그 반대의 경우가 분명 존재합니다.

예를 들어 `SafeAreaView` (상단의 시간, 배터리등의 status를 나타내는 영역을 제외한 뷰)에서 안드로이드는 따로 패딩을 줘서 처리해야하는 문제가 있다.

이 때는, `Platform` 과 `StatusBar` api를 호출해 아래와 같이 styles를 적용합니다. (1:14:49 Platform-specific code)

```react
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    // 이 부분
    paddingTop: Platform.OS === "android" ? StatusBar.currentHeight : 0,
  },
});
```

