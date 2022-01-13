---
title: "GitHub Personal Access Token"
date: 2021-08-15 23:41:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - Github_Pages
    - github
    - git
---

2021, Aug 13th 부터 terminal을 통한 github 연결 시 기존의 username, password로 쳐서 들어가는 방법이 제한 되었다.

로컬에 token 저장하여 사용하는 방법.

1. Personal Access Tokens 만들기 : Github \> Settings \> Developer settings \> Personal acess tokens

2. Git Credential Manager Core 설치 : [Linux](https://github.com/microsoft/Git-Credential-Manager-Core#linux-install-instructions)

3. git config --global credential.credentialStore plaintext : Personal acess token 선택하여 '1'에서 만든 token 입력