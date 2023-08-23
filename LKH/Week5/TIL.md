# 2023-08-22 Week 5 배운 점 정리


## 7576 토마토

+ bfs를 이용하여 풀이함.
  + 토마토가 익는데 걸리는 시간을 구하는 문제이므로, 익은 토마토를 기준으로 bfs를 수행함.
  + 익은 토마토를 기준으로 bfs를 수행하며, 익은 토마토의 상하좌우에 있는 토마토를 익게 만듬.
  + 처음엔 `Day_count` 변수를 활용하여 bfs에서 익은 토마토의 개수를 세었으나, 구현이 쉽지않아 다른 방식으로 진행함

```python
import sys

from collections import deque

M, N = map(int, sys.stdin.readline().split())

box = [list(map(int, sys.stdin.readline().split())) for _ in range(N)]

q = deque()
next_q = deque()
for i in range(N):
    for j in range(M):
        if box[i][j] == 1:
            q.append((i, j))
# 상하좌우

delta = [(0, 1), (0, -1), (1, 0), (-1, 0)]

def bfs(box):
    while q:
        x, y = q.popleft()
        for dx, dy in delta:
            nx, ny = x + dx, y + dy
            if 0 <= nx < N and 0 <= ny < M and box[nx][ny] == 0:
                box[nx][ny] = box[x][y] + 1
                q.append((nx, ny))import sys

from collections import deque

M, N = map(int, sys.stdin.readline().split())

box = [list(map(int, sys.stdin.readline().split())) for _ in range(N)]

q = deque()
next_q = deque()
for i in range(N):
    for j in range(M):
        if box[i][j] == 1:
            q.append((i, j))
# 상하좌우

delta = [(0, 1), (0, -1), (1, 0), (-1, 0)]

def bfs(box):
    while q:
        x, y = q.popleft()
        for dx, dy in delta:
            nx, ny = x + dx, y + dy
            if 0 <= nx < N and 0 <= ny < M and box[nx][ny] == 0:
                box[nx][ny] = box[x][y] + 1
                q.append((nx, ny))

bfs(box)

for i in range(N):
    for j in range(M):
        if box[i][j] == 0:
            print(-1)
            exit()

print(max(map(max, box)) - 1)

bfs(box)

for i in range(N):
    for j in range(M):
        if box[i][j] == 0:
            print(-1)
            exit()

print(max(map(max, box)) - 1)
```

## 11723 집합

+ 비트마스킹을 이용하여 풀이함.
  + 처음에는 `set` 자료구조를 활용하여 풀이했으나, 시간초과가 발생하여 비트마스킹을 활용하여 풀이함.
  + 비트마스킹을 활용하여 풀이하면, `set` 자료구조를 활용하여 풀이할 때보다 시간이 더 적게 걸림.
  + 또한 메모리 사용량도 더 적게 사용한다는 장점이 있음.

```python
import sys

input = sys.stdin.readline

S = 0
for _ in range(int(input())):
    cmd = input().split()
    if cmd[0] == "add":
        M = 1 << (int(cmd[1]) - 1)
        S = S | M
    elif cmd[0] == "remove":
        M = 1 << (int(cmd[1]) - 1)
        S = S & ~M
    elif cmd[0] == "check":
        M = 1 << (int(cmd[1]) - 1)
        if S & M:
            print(1)
        else:
            print(0)
    elif cmd[0] == "toggle":
        M = 1 << (int(cmd[1]) - 1)
        S = S ^ M
    elif cmd[0] == "all":
        S = 2 ** 20 - 1
    elif cmd[0] == "empty":
        S = 0
```

## 11726 2xn 타일링

+ dp를 이용하여 풀이하지 못해 풀이에 실패함.
  + dp를 이용하여 풀이하는 방법을 알아두어야 할 것 같음.
  + `math.factorial`을 이용하여 풀이하였는데, 풀이에 실패함.

+ 풀이에 실패한 코드

```python
import sys
import math

input = sys.stdin.readline

N = int(input())
ans = 0
if N % 2 == 0:
    onebytwo = list(map(int, range(0, N + 1, 2)))
    twobyone = list(map(int, range(N, -1, -2)))
else:
    onebytwo = list(map(int, range(1, N + 1, 2)))
    twobyone = list(map(int, range(N - 1, -1, -2)))

for o, x in zip(onebytwo, twobyone):
    ans += math.factorial(o + x // 2) / (math.factorial(o) * math.factorial(x // 2))

print(int(ans % 10007)
```

+ 문제점
  + 정수연산 : `math.factorial`을 이용하여 풀이하였는데, 이는 정수연산을 하지 않고 실수연산을 하기 때문에 정확한 값을 구할 수 없음.
  + `math.factorial`을 이용하지 않고 정수연산을 하여 풀이하면 정확한 값을 구할 수 있을지도?

