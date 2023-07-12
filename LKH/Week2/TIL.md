# 2023-07-12 Week 2 배운 점 정리

## 1074 Z

+ 분할 정복 문제
    + 문제를 풀기 위해선 분할 정복을 이용하여야 했음.
    + 분할 정복이란 큰 문제를 작은 문제로 나누어 푸는 것을 의미함.
    + 이 문제의 경우 2차원 배열을 4등분 하여 각각의 배열에 대해 재귀적으로 탐색을 진행하여야 함.
    + 이때, 재귀적으로 탐색을 진행할 때마다 4등분을 하여야 하므로 2의 제곱수인 4를 계속해서 곱해주어야 함.

저번 주차에서 풀지 못했던 Z 문제를 다시 풀어보았다.

```python
N, r, c = map(int, input().split())


def Z(n, x, y):
    if n == 1:
        return 2 * x + y
    # 1
    if x < 2 ** (n - 1) and y < 2 ** (n - 1):
        return Z(n - 1, x, y)
    # 2
    elif x < 2 ** (n - 1) <= y:
        return Z(n - 1, x, y - 2 ** (n - 1)) + 4 ** (n - 1)
    # 3
    elif x >= 2 ** (n - 1) > y:
        return Z(n - 1, x - 2 ** (n - 1), y) + 2 * 4 ** (n - 1)
    # 4
    else:
        return Z(n - 1, x - 2 ** (n - 1), y - 2 ** (n - 1)) + 3 * 4 ** (n - 1)


print(Z(N, r, c))
```

위와 같이 `Z` 라는 함수가 계속 반복되는 것을 확인 할 수 있는데, 이는 재귀적으로 문제를 풀어야 하기 때문이다.
`x` 와 `y` 는 2차원 배열의 인덱스를 의미하며, `n` 은 2차원 배열의 크기를 의미한다.

`n` 이 1이 될 때까지 `Z` 함수를 호출하며, `n` 이 1이 되면 `2 * x + y` 를 반환한다.

`n` 이 1이 아닐 때, `x` 와 `y` 를 2의 제곱수인 4로 나누어 4등분을 하여 재귀적으로 `Z` 함수를 호출한다.

## 1620 나는야 포켓몬 마스터 이다솜

+ 딕셔너리를 이용한 풀이
    + 딕셔너리를 이용하여 풀이하였음.
    + 딕셔너리의 `key` 값은 포켓몬의 이름을 의미하며, `value` 값은 포켓몬의 번호를 의미함.
    + 딕셔너리의 `key` 값과 value 값을 바꾸어 새로운 딕셔너리를 만들어서 풀이하였음.

```python
import sys

N, M = map(int, input().split())

pocketmon = {}
pocketmon2 = {}

input = sys.stdin.readline

for i in range(1, N + 1):
    name = input().rstrip()
    pocketmon[str(i)] = name
    pocketmon2[name] = str(i)

for i in range(1, M + 1):
    quiz = input().rstrip()
    if quiz.isalpha():
        print(pocketmon2[quiz])
    else:
        print(pocketmon[quiz])
```

위와 같이 딕셔너리를 이용하여 풀이하였다.

`pocketmon` 이라는 딕셔너리의 key 값은 포켓몬 도감의 수록된 번호들을 의미하며, `value` 값은 포켓몬의 이름를 의미한다.
반대로 `pocketmon2` 라는 딕셔너리는 `pocketmon` 딕셔너리의 `key` 값과 `value` 값을 바꾸어 만든 딕셔너리이다.
이렇게 하지 않고 딕셔너리 하나로 문제풀이를 하려고 했으나, 시간초과가 발생하였다.

### Hash Table 개념 정리

- `HashTable(해시 테이블)`은 `Key` 와 `Value` 의 쌍으로 데이터를 저장하는 자료구조 입니다.
  언어에 따라서 `HashMap`이라고도 불리며, 파이썬의 `Dictionary` 또한 `HashTable`로 구현되어 있습니다.


- `HashTable`(`HashMap`, `Dictionary`) 의 특징은 다음과 같습니다.

    - 순차적으로 데이터를 저장하지 않습니다.
    - `Key`를 통해서 `Value`값을 얻습니다.
    - `Value`값은 중복 가능 하지만 `Key`는 중복될 수 없습니다.
    - 수정 가능합니다.(mutable)

특히 파이썬에서는 `Dictionary`가 `List` 보다 훨씬 빠르게 동작하기 떄문에 데이터를 조회할 때 `Dictionary`를 사용하는 것이 좋습니다.
시간초과가 난다면 `Dictionary`를 사용할 수 있는지 확인해보는 것도 좋을 것 같습니다.

## 1697 숨바꼭질

+ BFS를 이용한 풀이
    + BFS를 이용하여 풀이하였음.
    + `cur` 이라는 변수에 현재 위치를 저장하고, `cnt` 라는 변수에 현재 위치까지 오는데 걸린 시간을 저장함.
    + `cur` 이라는 변수가 `end` 변수와 같아지면 `cnt` 를 반환함.

아래와 같은 코드를 작성하였지만 시간초과, 메모리 초과로 인한 채점이 불가능했다.


``` python
from collections import deque

cur, end = map(int, input().split())


def bfs(cur, end):
    queue = deque()
    queue.append([cur, 0])

    while queue:
        cur, cnt = queue.popleft()

        if cur == end:
            return cnt
        else:
            if cur*2 <= 100000: 
                queue.append([cur * 2, cnt + 1])
            if cur+1 <= 100000 and cur+1 <= end:
                queue.append([cur + 1, cnt + 1])
            if cur-1 >= 0:
                queue.append([cur - 1, cnt + 1])

    # 못 찾았을 경우
    return -1


print(bfs(cur, end))
```

이유는 다음시간에 알아보도록 하자, 지금 생각하기로는 큐에 너무 많은 데이터가 쌓이고 있어서 그런것 같다. ` append` 를 할 때마다 `queue` 에 데이터가 쌓이고 있기 때문이다.
`append` 하기 전 조건을 좀 다시 한번 살펴 봐야겠다.