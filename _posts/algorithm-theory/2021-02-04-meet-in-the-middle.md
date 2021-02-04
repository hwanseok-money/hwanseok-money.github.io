---
title: "[이론] meet in the middle"
excerpt: "BOJ 9985 Missing Piece 2001 풀이를 중심으로"
date: 2021-02-03
last_modified_at:
categories:
  - Algorithm-Practice
tags:
  - Algorithm-Practice
  - Practice
  - meet in the middle
  - 9985
  - Missing Piece 2001
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# ㅎㅎㅎ

2021.02.04 현재 c++ 외 다른 언어로 푼 사람은 저밖에 없네요 ㅎㅎ  

## 알고리즘 설명

두 지점 ㄱ과 ㄴ 사이의 거리가 10이라고 해보겠습니다. ㄱ에서 ㄴ으로 BFS를 진행하면 depth가 10일때까지 진행되어야 합니다. 한 depth마다 인접한 칸이 K개 있다고 하면 $O(k^depth)$만큼의 시간복잡도가 걸립니다.  

그런데 `양방향 BFS(Bidirectional BFS)`을 사용해서 ㄱ에서 ㄴ으로, ㄴ에서 ㄱ으로 동시에 BFS를 진행할 수 있습니다. 이 경우 $O(k^{depth/2})$만큼의 시간복잡도가 걸립니다. 절반으로 줄어듭니다.  

[boj 9985](https://www.acmicpc.net/problem/9985)문제는 이 방법을 사용하는 문제 중 하나입니다.  

입력이 아래와 같이 주어지면 3*3 격자칸에서 4번만의 이동으로 초기값에서 목표값으로 바꿀 수 있느냐 없느냐를 판단하는 문제입니다. 자세한 문제의 조건은 위 링크를 확인해주세요.  

```
START 3 4
1 5 2
4 X 3
7 8 6
1 2 3
4 5 6
7 8 X
END
```  

D가 10까지 커질 수 있기 때문에, 글고 BFS의 depth는 15까지 커질 수 있습니다. 만약 depth가 15에 도착해도 불가능하면 불가능하다록 출력하면 되도록 시간초과를 피할 수 있도록 조건을 추가해두었습니다.  

문제를 어떤 숫자를 x방향으로 옮기는 것이 아니라 x를 인접한 4가지 방향 중 한 곳으로 움직이는 것으로 생각해보겠습니다. 그러면 x가 움직일 수 있는 경우의 수는 상하좌우 4곳이고, 절반의 depth만큼 진행할 수 있으므로 $4^7~4^8$ 정도의 경우의  수를 판단하게 됩니다. 이정도는 1억보다 추웅분히 작기 때문에 시도해볼 수 있습니다.  

### python에서 대입연산은 참조

이 문제에서 주의할 점이 있습니다. `python에서 대입연산은 참조`라는 점을 기억해야 합니다.  

```python
class Node:
    def __init__(self, side=None):
        self.r = -1
        self.c = -1
        if side is not None:
            self.cell = [[0] * side for _ in range(side)]

    def set_point(self, r, c):
        self.r = r
        self.c = c


lst = []
curr = Node(3)

curr.set_point(1, 2)
lst.append(curr)
curr.set_point(4, 5)
lst.append(curr)
front = lst[0]
print(front.r, front.c)  # 4 5
front = lst[1]
print(front.r, front.c)  # 4 5
```

밑에서 list에 (1,2)과 (4,5)를 넣었는데 모두 (4,5),(4,5)가 됩니다. 실제로 list에 append 된 값은 curr가 가리키는 참조이기 때문입니다. 아래와 같이 deepcopy를 하면 이 문제를 해결할 수 있습니다.  

```python
from copy import deepcopy
lst = []
curr = Node(3)

curr.set_point(1, 2)
lst.append(deepcopy(curr))
curr.set_point(4, 5)
lst.append(deepcopy(curr))
front = lst[0]
print(front.r, front.c)  # 1 2
front = lst[1]
print(front.r, front.c)  # 4 5
```  

위 동작이 어색한 분들은 [python3-object](https://hwanseok-dev.github.io/python/python3-object/)포스팅을 확인 바랍니다.  

### 문제 풀이

위 문제에서 주어지는 게임판을 cell셀이라고 하겠습니다. 이 문제의 포인트는 셀의 상태를 기반으로 방문했는지 여부를 따지는 것입니다. BFS가 모든 노드를 한 번만 방문하는 알고리즘이기 때문에 방문여부를 따지는 것은 당연합니다. 하지만 이 문제에서는 cell이 d*d칸이기 때문에 cpp로 따지면 bool visited[r][c] 함수를 어떻게 사용해야할지가 막막합니다. 이 문제는 cell을 list로 만들고 list를 dict의 key로 사용하는 방법을 적용합니다. 대신 list는 dict의 key로 사용될 수 없어서 str(list)를 key로 사용합니다.  

list는 dict의 key가 될 수 없다는 점을 모르시는 분은 아래의 포스팅도 확인해주세요. [python3-dictionary](https://hwanseok-dev.github.io/python/python3-dictionary/)  

정리해보면 `dict[str(cell)] = 몇 번째 depth에 방문했는지` 정보를 저장해야 합니다.(dict는 visited의 역할을 수행합니다.) 그리고 meet in the middle이 BFS인만큼 q.append(cell)을 해서 진행합니다. 이 때 앞서 언급한대로 q.append(deepcopy(cell))을 해주어야 문제가 발생하지 않습니다. primitive type의 bfs는 그냥 해도 되지만 object type의 bfs는 deepcopy()를 해야합니다. 새로운 객체를 만들어서 append(push)하는거죠  

```python
import sys
from math import sqrt, ceil
from bisect import bisect_left, bisect_right
from operator import itemgetter
from collections import Counter, deque
from copy import deepcopy
# sys.stdin = open("input.txt", "r")

# dp = [[[0] * K for _ in range(C)] for _ in range(R)]
# MOD = 1000000000
# n = int(input())
# arr = list(map(int, sys.stdin.readline().split()))
dr = [0, 0, 1, -1]
dc = [1, -1, 0, 0]


class Node:
    def __init__(self, side=None):
        self.r = -1
        self.c = -1
        if side is not None:
            self.cell = [[0] * side for _ in range(side)]

    def set_point(self, r, c):
        self.r = r
        self.c = c


while True:
    # 입력받기
    next_line = sys.stdin.readline()
    if next_line == '':
        break
    cmd, d, n = next_line.split()  # START, D, N
    d = int(d)
    n = int(n)
    nodes = [Node(d), Node(d)]
    for idx in range(2):
        for r in range(d):
            nodes[idx].cell[r][:] = sys.stdin.readline().split()
            for c in range(d):
                if nodes[idx].cell[r][c] == 'X':
                    nodes[idx].set_point(int(r), int(c))
    cmd = sys.stdin.readline()  # END

    # 문제풀이 시작
    dicts = [dict(), dict()]
    for idx in range(2):
        q = deque()
        # 현재 cell 상태를 dict에 저장
        # dicts[첫번째/두번째][Cell의 상태] = X 이동 횟수
        dicts[idx][str(nodes[idx].cell)] = 0
        q.append(nodes[idx])
        # N이 짝수라면 절반씩, 홀수라면 도착점(M[1])에서만 1만큼 더 탐색
        for depth in range(n // 2 + (n % 2 and idx)):
            q_size = len(q)
            for _ in range(q_size):
                curr = q.popleft()
                cr = curr.r
                cc = curr.c
                for k in range(4):
                    nr = cr + dr[k]
                    nc = cc + dc[k]
                    if nr < 0 or nr >= d or nc < 0 or nc >= d:
                        continue
                    curr.cell[cr][cc], curr.cell[nr][nc] = curr.cell[nr][nc], curr.cell[cr][cc]
                    if str(curr.cell) not in dicts[idx]:
                        curr.set_point(nr, nc)
                        dicts[idx][str(curr.cell)] = depth + 1
                        q.append(deepcopy(curr))
                    curr.cell[cr][cc], curr.cell[nr][nc] = curr.cell[nr][nc], curr.cell[cr][cc]
    result = n + 1
    for x1 in dicts[0]:
        if x1 in dicts[1]:
            # 시작점에서 BFS 한 위치외 도착점에서 BFS한 위치가 만나는 지점이 있는 경우
            result = min(result, dicts[0][x1] + dicts[1][x1])
    if result <= n:
        print("SOLVABLE WITHIN %d MOVES\n" % result)
    else:
        print("NOT SOLVABLE WITHIN %d MOVES\n" % n)
```

##  Reference

- [KKS님 감사합니다](https://m.blog.naver.com/PostView.nhn?blogId=kks227&logNo=221382873753&proxyReferer=https:%2F%2Fwww.google.com%2F)  

**Success Notice:**
어려운 문제였습니다. 아주 많이 수고하셨습니다. :+1:
{: .notice--success}