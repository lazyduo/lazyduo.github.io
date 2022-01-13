---
title: "GitLab EE Runner"
date: 2022-01-13 15:45:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - git
    - gitlab
---

GitLab EE VM에서 Runner 추가하는 방법.

## Install

VM Machine Architecture 및 OS에 맞게 아래 링크에서 install이 우선적으로 필요.

[Link](https://docs.gitlab.com/runner/install/index.html)

## Register

```bash
sudo gitlab-runner register
```

url, registration-token은 project의 "Settings > CI / CD > Runners" 에서 확인 가능하다.

또한 executor를 잘 정해야하는데, 보통 docker image로 빌드를 많이 해서 docker로 많이 쓰이고, 자신의 CI 빌드 script에 맞춰서 executor를 설정해 주면 된다.

## Tips

runner 설정에서 "Indicates whether this runner can pick jobs without tags" check 해주어야 tag 없는 job도 runner가 실행시켜 준다.

