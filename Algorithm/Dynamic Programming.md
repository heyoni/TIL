## [1. 피보나치 함수 - 실패(1003)](https://www.acmicpc.net/problem/1003)

각 테스트 케이스마다 0이 출력되는 횟수와 1이 출력되는 횟수를 공백으로 구분해서 출력한다.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

def fibonacci(n):
    if n == 0:
        l[0] += 1
        return 0

    elif n == 1:
        l[1] += 1
        return 1

    else:
        return fibonacci(n-1) + fibonacci(n-2)

T = int(input())
for _ in range(T):
    l = [0, 0]
    n = int(input())
    fibonacci(n)
    print(*l)
```

시간 초과로 실패한 코드이다. 재귀함수의 호출을 줄일 방법을 생각해 봐야겠다.
