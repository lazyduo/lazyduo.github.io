---
title: "환경변수 Path"
date: 2021-04-29 23:23:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - ETC_Posts
---
환경변수 Path를 날려 먹었습니다...

## 환경 변수 Path 증발

환경 변수는 OS가 해당 프로세스를 실행시키기 위해 참조하는 변수값으로, 
path 변수는 프로레스를 실행 시킬 때 참조하는 경로라고 보면 된다. 
예를 들어, cmd창에서 `$ python`을 아무리 외쳐 봤자
python의 절대경로가 path에 등록되어 있지 않으면 절대 실행불가능하다.

이 점을 제대로 인지하지 못한 체, C++ 컴파일을 위해 gcc를 등록하면서
path 변수를 **overwrite** 시켜 버렸다. 그동안 저장되어 있던 변수가 싹 다 날라가 버린 것이다!!

## Path 변수 복구

`cmd > regedit`로 Regedit 창에서 아래 경로로 백업용 값을 확인할 수 있다고 한다.

`HKEY_LOCAL_MACHINE\SYSTEM\ContorlSet002\Contorl\Session Manager\Environment`

하지만, `ControlSet002`가 내 경우엔 없었다.
아마 gcc가 잘 안되서 '확인'을 여러번 누른다고 날라간 것 같다.


다른 방법으로, cmd창에서 `echo %PATH% ` 명령어 입력하는 방법을 시도해 보았다.
더 쉬운 방법이긴 하지만, 이 또한 현재 값과 이전 값 두개만 보여주는듯 하다.

**결론은 그냥 수동으로 다시 다 추가 했다.**

python, pip, git, powershell이 원래대로 돌아와서 기쁘다..