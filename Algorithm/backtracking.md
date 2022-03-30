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
