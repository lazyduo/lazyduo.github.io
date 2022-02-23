---
title: "Bit Mask 업무 실사용 예시"
date: 2022-02-23 10:31:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - bitmask
---

@ PostgreSQL Server Extension

Status Code를 bit mask하여 컨디션을 줄 때도 or(|)로 주고, 체크할 때도 and(&)로 쉽게 가능.

## code

```c
/* Returns bit mask indicating which condition(s) caused the wake-up. */
int events = WaitLatch(MyLatch,
                    WL_LATCH_SET | WL_TIMEOUT | WL_POSTMASTER_DEATH,
                    1000L,
                    PG_WAIT_EXTENSION);
ResetLatch(MyLatch);
if (events & WL_POSTMASTER_DEATH)
    elog(FATAL, "unexpected Postmaster dead");
```