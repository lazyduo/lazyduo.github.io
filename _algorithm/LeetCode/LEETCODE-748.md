---
title: "LeetCode - 748. Shortest Completing Word"
date: 2021-10-12 21:21:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - algorithm
---

크게 어렵진 않은데 이것저것 신경쓸게 있다.

1. `licencePlate`에서 알파벳만 카운팅하고, 대소문자는 똑같이 처리
2. 알파벳은 모두 사용해야함
3. `words`에서 조건에 맞는 'word' 중 가장 짧은 단어를 리턴해야함
4. 여러개의 'word'가 있다면 순서상 가장 먼저 나온 단어를 리턴

우선 `licensePlate` 처리를 '.lower()'와 'stack' 구조인 리스트를 통해서 알파벳들만 스택에 담았다.

'가장 짧은' completing word 를 리턴해야하므로 'answer' 뿐만 아니라 'answerLength'도 변수로 준비한다.

애초에 가장 짧은 단어를 리턴하므로 for문 처음 부터 단어 길이를 체크해서 불필요한 반복은 피했다.

조건 확인 부분은 앞에서 구한 스택을 복사하고, 단어를 앞에서 부터 차례로 확인하여 제거해 나갔다. 굳이 제거하는 이유는 조건 중에 반드시 모든 라이센스 알파벳을 사용해야한다는 조건이 있었기 떄문이다.

runtime : 64ms / memory : 14.5MB

```python
class Solution:
    def shortestCompletingWord(self, licensePlate: str, words: List[str]) -> str:
        L = list(licensePlate)
        
        # parsing licensePlate
        licenseStack = []
        for license in L:
            if license >= 'A' and license <= 'z':
                licenseStack.append(license.lower())
        
        answer = ''
        answerLength = 1000
        
        for word in words:
            if len(word) >= answerLength:
                continue

            temp = list(licenseStack)
            
            for w in word:
                if w in temp:
                    temp.remove(w)
                    
                if not temp:
                    answerLength = len(word)
                    answer = word
                    break
                        
        return answer
```