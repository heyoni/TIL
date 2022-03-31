## [1. N과 M(15649)](https://www.acmicpc.net/problem/15649)

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
l = []

# 1. 문제풀기
# 재귀함수를 이용하여 수열을 만든다.
def backtracking():
    if len(l) == M:
        print(' '.join(map(str,l)))
        return

    for i in range(1,N+1):
        if i not in l:
            l.append(i)
            back_tracking()
            l.pop()

backtracking()
```

처음에는 아무 생각없이 라이브러리 사용하려고 했다가, 백트레킹 문제인걸 알고 난 뒤 다시 풀었다.  
백트레킹 : 퇴각검색, 길을 가다가 이 길이 아닌 것 같으면 왔던 길로 되돌아가 다른 경로를 탐색한다.  
"만든 수열 안에 값이 있으면 재귀하여 새로운 값을 넣는다."

## [1. N과 M2(15650)](https://www.acmicpc.net/problem/15650)

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 중복없는 수열을 모두 구하는 프로그램을 작성하시오. 단, 오름차순

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
l = []

# 1. 해결하기
# 기존에 뽑았던 숫자는 뒷 자리가 클 수 없기 때문에 start를 줌
def backtracking(start):
    if len(l) == M:
        print(*l)
        return

    for i in range(start,N+1):
        if i not in l:
            l.append(i)
            backtracking(i+1)
            l.pop()

backtracking(1)
```

1, 2는 이미 뽑혔으므로 2, 1은 뽑을 수 없다. 그러므로 start값이 무조건 커야한다. 그래서 새로운 조건을 추가했다.  
처음에는 set을 이용하여 풀었는데, 틀린 답이라고 해서 다시 작성했다. 알 수록 어려운 알고리즘의 세계...
