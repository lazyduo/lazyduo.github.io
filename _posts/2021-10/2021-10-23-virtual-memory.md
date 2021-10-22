---
title: "Virtual Memory"
date: 2021-10-23 00:01:00 +0900
classes: wide
tags:
    - tech
    - computer
---

## Virtual Memory
- 필요성 : 실제 주소로 바로바로 할당하면 fragment 들이 생겨서 메모리 낭비가 생김. 따라서 메모리를 효율적으로 쓰기 위해 알아서 잘 allocation 해주는 방법이 virtual memory, MMU 형태임.
- MMU (Memory Management Unit) : Virtual Address를 Physical Memory로 변환.
    - Page Table : VA PA mapping table
    - TTB (Translation Table Base Address) : Page Table 존재 위치 정보. MMU의 Register에 저장되어 있음. 외부 메모리에 저장되어 있어서, 매번 참조하면 느릴 수 있으므로 이를 Cache 처리함.
    - 4GB RAM 일 경우 레지스터의 크기는 32bit (2 \^ 32 = 4GB). Page Table 역시 4GB를 나타내어야하는데, page table의 한 개 Entry (32bit)는 1MB(무조건) 씩 가르킬 수 있기 때문에 4096 \* 32 bit = 16KB가 page Table 기본 크기.
    - 메모리 주소에서 12 bit(4K pages)는 page 정보로 virtual address에서 physical adress로 그대로 복사 된다.
    - TLB (Translation Lookaside Buffer) : 매번 page table을 참조하는 짓을 반복할 수 없으므로 사용되는 address-translation cache. page hit 이력이 있는지 없는지 판단해서 빠르게 access.
- [What is virtual memory? - Gary explains](https://www.youtube.com/watch?v=2quKyPnUShQ)