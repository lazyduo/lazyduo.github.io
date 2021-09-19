---
title: "React Native with M1 troubleshooting"
date: 2021-09-19 03:22:00 +0900
classes: wide
tags:
    - ETC
    - ETC_Posts
    - mac
    - m1
    - react-native
    - flipper
    - setup
---

거의 1주일을 괴롭혔던 react-native ios build 문제가 드디어 해결! (새벽 3시 반..)

flipper를 쓰지 않으면 podfile에서 flipper 부분을 코멘트 처리하면 되니까 매우 문제가 쉬워진다.
하지만 flipper를 쓰고 싶다면?? 문제가 복잡하다.

내가 이번에 react-native 앱을 ios 빌드하기 위해 했던 일들을 쭉 살펴보자.

## ios 폴더 삭제

```bash
#  from /~~~/ios/Podfile:7
#  -------------------------------------------
#  target 'YumiNative' do
>    config = use_native_modules!
#
#  -------------------------------------------
```

위 문제를 해결하기 위해서 아예 ios 폴더 자체를 다시 만들었다.
ios 폴더를 삭제한 후, 프로젝트 dir에서

```bash
yarn add react-native-eject
npx react-native eject
```

## Pod 리셋

```bash
cd ios
pod deintegrate
pod update
pod install
```

flipper를 사용하지 않을 경우 Podfile 하단 flipper 부분을 싹다 코멘트 처리하면 된다. 어떤 사람들은 flipper 버전 지정만 하면 된다고 하는데... 나는 안된다.

## flipper

제일 문제가 많았던 친구...

M1 / macOS 11.5.1 / xcode 12.5.1 / react-native 0.65.1

1. add Swift File for make Bridging-Header. 일종의 편법으로 xcode에서 swift file을 하나 생성하면 Bridging-Header를 만들겠냐고 하면 OK하면 된다. 근본적인 해결방법은 아래 post_install의 첫번째 부분인 것 같다.
2. XCODE > Build Setting > Exluded Architecture : add 'arm64' both Debug and Release. arm64 어쩌구 나오는 에러들을 해결하기 위한 설정. 아래 post_install에서 only_active_arch 도 arm관련인 것으로 추정된다. 어디서 봤는지 모르지만, 따로 추가해 준 부분인데,이게 없으면 arm64 관련 에러가 다시 등장한다.
3. RCT-Folly time.h problem -> the last line of Podfile script. 진짜 마지막 하나 남은 에러의 원인. time.h에서 어쩌구 하면서 에러가 난다. 아직도 진행중인 이슈인듯하다. 일단 아래의 마지막줄이 임시로 해결해 주었다.

제 Podfile 소스는 [여기](https://github.com/lazyduo/my_dotfiles/blob/main/ios/Podfile)를 참고하세요.


아래 Podfile의 원형을 제공해줘 드디어 이 삽질을 끝내게해 준 mikehardy([link](https://github.com/facebook/react-native/issues/31941#issuecomment-904995765)에 무한한 감사를..

```ruby
 post_install do |installer|
    react_native_post_install(installer)

    # Apple Silicon builds require a library path tweak for Swift library discovery or "symbol not found" for swift things
    installer.aggregate_targets.each do |aggregate_target| 
      aggregate_target.user_project.native_targets.each do |target|
        target.build_configurations.each do |config|
          config.build_settings['LIBRARY_SEARCH_PATHS'] = ['$(SDKROOT)/usr/lib/swift', '$(inherited)']
        end
      end
      aggregate_target.user_project.save
    end

     # Flipper requires a crude patch to bump up iOS deployment target, or "error: thread-local storage is not supported for the current target"
    # I'm not aware of any other way to fix this one other than bumping iOS deployment target to match react-native (iOS 11 now)
    installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings["ONLY_ACTIVE_ARCH"] = "NO"
        config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '11.0'
       end
    end

    # ...but if you bump iOS deployment target, Flipper barfs again "Time.h:52:17: error: typedef redefinition with different types"
    # We need to make one crude patch to RCT-Folly - set `__IPHONE_10_0` to our iOS target + 1
    # https://github.com/facebook/flipper/issues/834 - 84 comments and still going...
    `sed -i -e  $'s/__IPHONE_10_0/__IPHONE_12_0/' Pods/RCT-Folly/folly/portability/Time.h`
  end
```