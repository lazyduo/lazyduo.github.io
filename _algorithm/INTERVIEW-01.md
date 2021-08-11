---
title: "INTERVIEW - 01"
date: 2021-07-30 13:11:00 +0900
classes: wide
author_profile: true
sidebar:
    nav: "tech"
tags:
    - python
    - interview
---

생애 첫 개발자 인터뷰 후기 겸 해결하지 못한 부분들 답답해서 정리.

## 총평

일단 내 스스로 한테 너무 화가 난다.

평소랑 다르게 자신감이 결여되어 있었다. 5년 전 취업 준비했을 때의 당당했던 모습 같은건 전부 사라져 있었다. 지금 다니는 회사가 지금까지 사람을 멍청하게 만들어서인지, 전공 분야가 아닌 새롭게 도전하는 분야여서 인지, 내 답에 대한 확신이 계속 부족했다. 더 좋은 답이 분명 있다는 걸 아는 상황에서 답이라고 말하기 너무 힘들었다.

변명이 길다.

너무 초라해져 버린 것 같다. 결과가 어떻든 열심히 하자.

## 인터뷰

총 4번의 인터뷰로 1시간씩 총 4시간 동안 진행되었다. 과거 처음 취준 할 때는 인터뷰라고 해도 개인별로 길게 잡아야 20분 정도 걸렸지, 나머지는 다 대기시간이었다. 이렇게 1시간 온전히 면접관님과 같이 대화하면서 하는 경험은 처음이었다. 그것도 네 분의 면접관님과 각각 1시간씩! 정말 힘들었다.

### 첫번째

아이스브레이킹과 코딩테스트. 솔직히 이때부터 조금 당황했다. 음 뭐랄까 아예 인터뷰 형식에 대해서 잘못 캐치하고 있었다. 프로젝트 결과물 혹은 짠 코드들을 보면서 사용한 기술들 위주로 얘기를 나누게 될 줄 알았는데, 좀 더 기본적인 코딩테스트가 메인이었다.

숫자 배열의 Local Minimum 찾기.

당연히 무지성으로 O(n)인 코드를 짰다. (이렇게 쉬울리 없잖아) 면접관께서 시간복잡도를 더 줄이라고 하셔서, Binary Search를 적용했지만 Binary Search 코드 형태를 외우고 있는게 아니라서 시간이 좀 걸렸고, 답은 나오지만 조건을 제대로 설정 못했다. 말그대로 굉장히 찜찜한, 더러운 코드를 작성 했다.

결국, 기본적인 알고리즘 형태는 어느 정도 외워서 바로 써먹는 것도 좋겠다는 면접관님의 쓴 말씀을 듣게 됨.

### 두번째

가장 망했다고 생각하는 인터뷰. 그냥 머리가 굳었다. 그 당시 만큼은 공간지각능력이 없는 사람이었다. 이상하게 머리가 잘 안돌아갔다. 정말로.

이 후기를 쓰는 가장 큰 이유이기도 하다. 이 인터뷰에서의 문제를 다시 풀어 보았다.

문제는 **블록의 숫자가 주어졌을 때, 만들 수 있는 블록 모양(테트리스 피스)의 개수를 구할 것.**

문제 자체는 심플 했지만, 단계 단계를 거쳐야 할 것이 많았다. 일단 새로 작성한 아래 코드를 참고하자. (아직 수정할 부분은 많지만 그래도 답은 나온다.)

1. print_p(p) : p(piece) 모양을 보기 좋은 형태로 출력해준다. 가뜩이나 배열로 되어 있어서 눈에 잘 안들어와서 하나 만들었다.

2. rotate_clockwise(p) : piece를 시계방향으로 회전 시켜준다. 

3. is_same(p1, p2) : rotate_clockwise를 이용해서 p1과 p2가 같은 모양인지 확인한다. (인터뷰에서는 여기까지만 완성했다...)

4. get_candidates(p) : 현재 piece의 상하좌우로 배열을 확장하고, 한 블록을 추가하게 될 경우 가능한 후보들을 반환한다.
  인터뷰 때 배열(리스트)를 복사할 때 단순히 '=' 처리해서 reference가 같은 바람에 계속 새로운 배열이 생성되지 못하고 overwrite 되어서 망했다.
  shallow copy와 deep copy 개념을 모르고 있어서 당황했다. python에서는 copy 라이브러리의 deepcopy를 쓰거나, 새로이 오브젝트를 만든 후에 복사를 진행해야한다.

5. trim_zeros(p) : 확장된 배열의 필요 없는 부분을 제거해 준다. (trim)

6. remove_duplicated_candidates : 후보들 중에서 중복 되는 모양의 piece들을 is_same()으로 찾아서 없애준다. 하나 하나 찾아서 없앴다.

7. main() : 처음에 하나의 블록에서 시작하여 input block size 까지 반복해서 candidates를 늘려나가면서 최종 답을 얻는다.

이렇게 많은 과정이 필요했는데, 면접관님 너무하셨습니다...

```python
  # Tetris
  import copy

  def print_p(p):
      print('--------')
      for col in p:
          print(col, ',')
      print('--------')
      return

  def rotate_clockwise(p):
      cols = len(p)
      rows = len(p[0])

      new_p = [[0 for _ in range(cols)] for _ in range(rows)]

      for i in range(cols):
          for j in range(rows):
              new_p[j][cols - i - 1] = p[i][j]

      return new_p

  def trim_zeros(p):
      col_s, row_s = 1, 1
      col_e, row_e = len(p) - 2, len(p[0]) - 2

      # check edges
      if 1 in p[0]: # UP
          col_s -= 1
      if 1 in p[-1]: # DOWN
          col_e += 1
      if 1 in list(map(lambda x: x[0], p)): # LEFT
          row_s -= 1
      if 1 in list(map(lambda x: x[-1], p)): # RIGHT
          row_e += 1

      # deep copy
      new_p = [[0 for _ in range(row_e - row_s + 1)] for _ in range(col_e - col_s + 1)]
      for i in range(col_s, col_e + 1):
          for j in range(row_s, row_e + 1):
              new_p[i - col_s][j - row_s] = p[i][j]
      return new_p


  def get_candidates(p):
      # extend
      cols = len(p)
      rows = len(p[0])

      new_p = [[0 for _ in range(rows + 2)] for _ in range(cols + 2)]

      for i in range(cols):
          for j in range(rows):
              new_p[i+1][j+1] = p[i][j]

      # add block
      candidates = []
      cols = len(new_p)
      rows = len(new_p[0])
      direction = [(1, 0), (-1, 0), (0, 1), (0, -1)]
      for i in range(cols):
          for j in range(rows):
              if new_p[i][j] == 0:
                  # check neighbors
                  for dx, dy in direction:
                      new_i = i + dx
                      new_j = j + dy
                      if new_i >=0 and new_i < cols and new_j >=0 and new_j < rows:
                          if new_p[new_i][new_j] == 1:
                              candidate = copy.deepcopy(new_p)
                              candidate[i][j] = 1
                              candidates.append(trim_zeros(candidate))
                              break

      return candidates


  def is_same(p1, p2):

      for _ in range(4):
          if p1 == p2:
              return True
          p1 = rotate_clockwise(p1)

      return False

  def remove_duplicated_candidates(candidates):
      final_candidates = []
      while candidates:
          curr = candidates.pop()
          if candidates:
              flag = True
              for candidate in candidates:
                  if is_same(curr, candidate):
                      flag = False
                      break
              if flag:
                  final_candidates.append(curr)
          else:
              final_candidates.append(curr)

      return final_candidates


  if __name__ == '__main__':
      block_size= int(input('input block size...'))
      p0 = [[1]]
      candidates = [p0]

      for _ in range(block_size - 1):
          next_candidates = []
          for p in candidates:
              next_candidates += get_candidates(p)

          candidates = remove_duplicated_candidates(next_candidates)

      for candidate in candidates:
          print_p(candidate)

      print(f'Total number of Tetris pieces : {len(candidates)} (when block size = {block_size})')
```

우선 답은 아래와 같이 잘 나온다.

```cmd
  input block size...4
  --------
  [1] ,
  [1] ,
  [1] ,
  [1] ,
  --------
  [1, 1] ,
  [0, 1] ,
  [0, 1] ,
  --------
  [1, 1, 0] ,
  [0, 1, 1] ,
  --------
  [1, 1] ,
  [1, 1] ,
  --------
  [1, 1, 1] ,
  [0, 0, 1] ,
  --------
  [0, 1] ,
  [1, 1] ,
  [0, 1] ,
  --------
  [1, 0] ,
  [1, 1] ,
  [0, 1] ,
  Total number of Tetris pieces : 7 (when block size = 4)
```

### 세번째

그래도 잘 했다고 말해주셨지만, 마찬가지로 뭔가 찜찜한게 남았던 코딩 문제.

**절대 경로 혹은 상대경로를 받아서 경로를 정리하기.**

ex) 'a/b/../c' -> 'a/c', 'a/b//./c' -> 'a/b/c'

이 문제는 나 스스로가 입력값에 대한 출력값이 정확히 뭔지 잘 모르겠다는게 가장 큰 문제였다.

결과가 어떻게 나와야 맞는건지에 대한 확신이 없으니, 당연히 조건 처리를 잘 못할 수 밖에 없었다.

특히 맨 첫번째에서 '..'이 일어날 때 상대경로와 절대경로에서의 처리가 달라서 헤맸다.

(사실 아직도 조금 이해가 안되고 헷갈린다)

'./d' -> 'd', '/./d' -> '/d', '/../d' -> '/d', '../d' -> '../d' ????????

### 네번째

코딩테스트 없이 fundamental 개념 질문 만으로 인터뷰 진행하셨다.

내가 얼마나 기초가 없는 사람인가 뼈저리게 느꼈다.

1. static vs dynamic allocation : stack 메모리와 heap 메모리에 대한 설명을 잘 했더라면... 횡설수설 했다. [link](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)

2. Sort 알고리즘 설명과 각 알고리즘의 시간 복잡도 : 뭐든 정확하게 좀 알자...

3. Binary Tree의 traversal : 전위, 중위, 후위 개념을 아는가.

4. Linked List 의 순서상 가운데 값 찾기 : 포인터 두 개를 이용하는 방법!

5. Stack의 Max 값 추가 메모리 없이 O(1) 으로 구하기 : push, pop일 때 트릭을 줘서 해결 한다. push 할 때 Max 보다 클 경우 (2\*x - Max), pop 할 때 Max 보다 클 경우 (2\*Max - y), 원래 push한 값은 Max로 반환해야한다. 솔직히 한 번도 보지 못했던거라면 생각해내기에 너무나 힘든 문제다. [link](https://www.geeksforgeeks.org/find-maximum-in-a-stack-in-o1-time-and-o1-extra-space/)

## 정리

제발 대충 알지 말고 하나라도 제대로 알고 넘어가자.

