---
title: "LeetCode - 1209. Remove All Adjacent Duplicates in String II"
date: 2021-10-13 17:54:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
---

Medium. 'word cnt'를 주면서 중복 수인 'k'와 일치하는지 확인 후 일치 한다면 스택에서 'pop()'시키는 것이 포인트. 'pop()' 이후에는 다시 현재 스택의 마지막 'word'와 일치하는지 체크하며 카운트를 늘려 나간다.

1. 현재 비교하고자 하는 단어(알파벳)과 일치하는지 확인
2. 일치한다면, 스택의 마지막 단어 카운트에 +1
3. 일치하지 않다면, 새롭게 단어 카운트를 스택에 추가한다
4. 현재 단어 카운트가 중복 수인 'k'와 일치한다면 스택에서 pop한다.
5. 최종적으로 만들어진 단어 카운트 스택을 파싱하여 최종 리턴 단어로 만든다.

runtime : 92~179ms / memory : 19MB

```python
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        word = ''
        word_cnt = [] # [[word, cnt]]
        
        for i in range(len(s)):
            if s[i] == word:
                word_cnt[-1][1] += 1
                if word_cnt[-1][1] == k:
                    word_cnt.pop()
                    
                    if word_cnt: # check list is empty
                        word = word_cnt[-1][0]
                    else:
                        word = ''
            else:
                word_cnt.append([s[i], 1])
                word = s[i]
        
        # parsing
        # [['a', 1], ['b', 2], ['c', 1]]
        # to 'abbc'
        answer= ''
        for alphabet, number in word_cnt:
            answer += alphabet * number
            
        return answer
```