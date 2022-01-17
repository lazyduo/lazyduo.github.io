---
title: "GitLab kthreaddk - High CPU usage"
date: 2022-01-17 16:56:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - git
    - gitlab
    - mining
---

`kthreaddk` 라는 process가 지속적으로 CPU를 점유하고, 새로운 git session을 만들고 있었음.

*(hacker가 mining 하려고 심은거라고 함)*

다행이도 이 [링크](https://gitlab.com/gitlab-org/gitlab/-/issues/345091)에 해결 내용이 있었고,

VM은 지독한 CPU, 메모리 점유에서 벗어날 수 있었다...

1. GitLab update (13.12 이상에서는 해당 security 문제가 해결되었다고 하는 듯)
2. `/var/spool/cron/crontabs/git` 에서 상태 확인. 뭔가 이상한게 있으면 감염된 것이 맞음.
3. 최종 솔루션
    - Stop Gitlab
    - `pkill kthreaddk` 를 loop로 돌릴 수 있는 sh 파일 만들기
    - `htop -u git`으로 다 죽었는지 확인
    - `/tmp` 를 전부 지우기
    - Ran `crontab -u git -r`

이때, process 이름은 꼭 `kthreaddk`가 아니더라도 `kthreaddw`등 비슷한 이름으로 나올 수 있으니 알맞게 처리해주자.