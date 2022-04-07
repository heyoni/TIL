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

## [1-1. 피보나치 함수 - 성공(1003)](https://www.acmicpc.net/problem/1003)

각 테스트 케이스마다 0이 출력되는 횟수와 1이 출력되는 횟수를 공백으로 구분해서 출력한다.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

l = [[0,0]]*41
l[0] = [1, 0]
l[1] = [0, 1]

for i in range(2, 41):
    l[i] = [a+b for a, b in zip(l[i-1],l[i-2])]

T = int(input())
for _ in range(T):
    k = int(input())
    print(*l[k])
```

DP : 동적 계획법이라고 부름. 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제에서 구한 정답은 큰 문제에서도 동일하다.  
피보나치 수열을 무한 재귀를 통해 구하는 것 보단 '메모이제이션'기법을 통해 정답을 저장하고, 그 값을 가져와 쓰는 것이 훨씬 효율적이다.  
이 문제에서는 '0과 1이 출력되는 횟수' 이기 때문에 리스트를 만들어서 0과 1이 출력되는 횟수를 저장했고, 직접 손으로 풀어보니`l[i] = l[i-1]+l[i-2]` 라는 공식을 얻어서 이 방식대로 리스트에 저장했다.

- 오랜만에 zip을 쓰다보니 많이 헤맸다.
- 함수를 통해 구현하는 방법(정석)도 있어서 해볼 것.
