## [1. N과 M(15649)](https://www.acmicpc.net/problem/15649)

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.(중복x)

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

## [2. N과 M2(15650)](https://www.acmicpc.net/problem/15650)

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

## [3. N과 M3(15651)](https://www.acmicpc.net/problem/15651)

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.(중복o)

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
l = []

def backtracking3():
    if len(l) == M:
        print(*l)
        return

    for i in range(1,N+1):
        l.append(i)
        backtracking3()
        l.pop()

backtracking3()
```

이게 백트레킹 1번 문제였어야 하지 않나.. 1, 2번 문제를 풀었으면 굉장히 쉽게 풀 수 있는 문제였다. if문을 제거하면 끝.

## [4. N과 M4(15652)](https://www.acmicpc.net/problem/15652)

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.(중복o, 비 내림차순)

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
l = []

def backtracking4(start):
    if len(l) == M:
        print(*l)
        return

    for i in range(start,N+1):
        l.append(i)
        backtracking4(i)
        l.pop()

backtracking4(1)
```

비 내림차순 : 길이가 K인 수열 A가 A1 ≤ A2 ≤ ... ≤ AK-1 ≤ AK를 만족하면, 비내림차순이라고 한다.  
2, 3번 문제를 섞어서 정답을 유추했다.

## [5. N-Queen(9663)](https://www.acmicpc.net/problem/9663)

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())

l = []
answer = 0
row = [0] * N

def is_there_queen(x):
    for i in range(x):
        if row[x] == row[i] or abs(row[x] - row[i]) == abs(x - i):
            return False

    return True


def set_queen(x):
    global answer
    if x == N:
        answer += 1
        return
    else:
        for i in range(N):
            row[x] = i
            if is_there_queen(x):
                set_queen(x+1)

set_queen(0)
print(answer)
```

1차원 배열로 퀸들의 위치를 정하고, 해당 퀸을 놓을 수 있는지에 대해서는 is_there_queen을 이용하여 검사한다.  
퀸이 죽지 않으려면

1. 같은 열인지
2. 왼쪽 아래/오른쪽 아래 대각선에 있는지

를 체크해줘야 한다.  
다른 방향을 체크해주지 않는 이유는 1행 1열부터 차근히 내려오기 때문에 이전 행열은 생각하지 않아도 된다.
python에서는 작동하지 않아서 pypy를 사용했다.


