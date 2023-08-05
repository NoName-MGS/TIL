# 2023-08-04 Week 4 배운 점 정리


## 10816 숫자 카드 2

+ 이분 탐색을 이용한 풀이
    + 이분 탐색을 이용하여 풀이하였음.
    + `card` 라는 변수에 숫자 카드의 정보를 저장하고, `find` 라는 변수에 찾아야 하는 숫자 카드의 정보를 저장함.
    + `card` 를 오름차순으로 정렬하고, `find` 를 순회하면서 `card` 에서 `find` 의 시작점과 끝점을 이분 탐색으로 찾아서 `end - start + 1` 을 출력함.

```python
from bisect import bisect_left, bisect_right

N = int(input())
Card = list(map(int, input().split()))
M = int(input())
Num = list(map(int, input().split()))

Card = sorted(Card)

for i in Num:
    print(bisect_right(Card, i) - bisect_left(Card, i), end=' ')
```

## 1920 수 찾기

+ 이분 탐색과 Sort를 이용한 풀이
    + `bisect` 라이브러리를 이용하여 이분 탐색을 구현하였음.
    + `bisect_left` 함수를 이용하여 `Aarr` 에서 `X` 의 시작점을 찾고, `bisect_right` 함수를 이용하여 `Aarr` 에서 `X` 의 끝점을 찾아서 `end - start + 1` 을 출력함.

```python
import sys
from bisect import bisect_left
input = sys.stdin.readline

N = int(input())
Aarr = list(map(int, input().split()))
M = int(input())
Xarr = list(map(int, input().split()))

Aarr.sort()
for X in Xarr:
    bisect = bisect_left(Aarr, X)
    if bisect < len(Aarr) and Aarr[bisect] == X :
        print(1)
    else:
        print(0)        
```
## bisect 라이브러리
  - bisect 모듈의 bisect_left, bisect_right 함수를 이용하여 이분 탐색을 구현할 수 있음.
  - bisect_left 함수는 정렬된 순서를 유지하면서 리스트 a에 x를 삽입할 가장 왼쪽 인덱스를 반환함.
  - bisect_right 함수는 정렬된 순서를 유지하면서 리스트 a에 x를 삽입할 가장 오른쪽 인덱스를 반환함.
  - bisect_left, bisect_right 함수는 시간 복잡도가 O(logN)으로 매우 빠름.
    - 단계마다 탐색 범위를 2로 나누는 것과 동일하므로 연산 횟수는 log₂𝑁에 비례한다
    - 예를 들어 초기 데이터 개수가 32개일 때, 이상적으로 1단계를 거치면 16개가량의 데이터만 남는다
    - 2단계를 거치면 8개가량의 데이터만 남는다
    - 3단계를 거치면 4개가량의 데이터만 남는다
    - 다시 말해 이진 탐색은 탐색 범위를 절반씩 줄이며, 시간 복잡도는 𝑂(log𝑁) 을 보장한다
  