## [1. 수 정렬하기 3(10989번)](https://www.acmicpc.net/problem/10989)
- N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.
```python
import sys
n = int(sys.stdin.readline())
# 카운팅 배열 선언
counting_arr = [0] * 10001

for i in range(n):
    # 숫자 입력받는데, 누적합으로 바로 바꿔줌
    counting_arr[int(sys.stdin.readline())] += 1
# 출력부분 
for i in range(10001):
    # 0이 아님 = 숫자가 있었다는 뜻
    if counting_arr[i] != 0:
        # 0부터 counting_arr[i]번 까지 순회를 돌면서 i를 출력한다.
        # 예를들어 0이 3번 나왔으면 counting_arr[0]==3, 그러니 0부터 2까지 총 3번을 돌며 0을 출력한다.
        for j in range(counting_arr[i]):
            print(i)

```
계수 정렬을 사용하는 문제였음.  
- 계수 정렬이란? : 정렬을 위해 가장 큰 수 +1만큼의 크기의 배열을 만들어주고, 거기서 나온 수 만큼 카운팅을 해줌, 그리고 누적합을 통해 숫자를 정렬하는 방법을 의미한다.  
- 계수 정렬의 시간 복잡도 : O(n)
- 정렬해야 할 숫자가 적거나 작을 때 사용한다. 단점은 추가적인 메모리가 필요함.


## [2. 나무 자르기(2805번)](https://www.acmicpc.net/problem/2805)
- 적어도 M미터의 나무를 집에 가져가기 위해서 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하시오.
```python
import sys
input = sys.stdin.readline

n,m = map(int, input().split())
trees = list(map(int, input().split()))
start, end = 1, max(trees)

while start <= end:
    mid = (start + end)//2
    sum = 0
    for i in trees:
        # 벌목 가능한 나무 = mid 보다 큰 나무만 잘라줌
        if mid < i:
            sum += (i - mid)
            # sum이 m보다 큰 경우 탈출하게 함(시간초과 때문에 작성)
            if sum > m:
                break
    # 토막난 조각의 합이 m보다 크면 mid가 start 값이 되어야함
    # 예제 1번 -> 1번 돌고 나면 mid = 9, sum은 26이 됨.
    # 26은 7(m의 값) 보다 크므로 범위를 좁혀야 한다.
    # sum(현재 26)을 줄이기 위해서는 mid값이 커져야 함 그래서 start값이 mid값을 넣어준다.
    if sum >= m:
        start = mid + 1
    else:
        end = mid - 1

print(end)

```
이분탐색(이진탐색, binary search)
- 이진 탐색(Binary search)은 정렬된 배열에 특정 원소가 존재하는지 여부를 파악하는 등의 문제를 O(log n) 시간에 해결하는 알고리즘이다.
- 반으로 나누고 크면 오른쪽, 작으면 왼쪽으로 가는 로직을 반복하여 원하는 값을 찾을 수 있다.
- 여기서는 원하는 값(m)을 찾기 위해서 이분탐색을 사용해야 하는 문제였음


## [4. 그르다 김가놈(18113번)](https://www.acmicpc.net/problem/18113)
- 공장에서는 김밥 N개에 대해서, 김밥 꼬다리를 잘라내고 손질된 김밥을 김밥조각으로 만드는 작업을 한다. 꼬다리를 잘라낼 때에는 양쪽에서 균일하게 K cm만큼 잘라낸다. 만약 김밥의 길이가 2K cm보다 짧아서 한쪽밖에 자르지 못한다면, 한쪽만 꼬다리를 잘라낸다. 김밥 길이가 K cm이거나 그보다 짧으면 그 김밥은 폐기한다.

- 손질된 김밥들은 모두 일정한 길이 P로 잘라서 P cm의 김밥조각들로 만든다. P는 양의 정수여야 한다. 정래는 일정한 길이 P cm로 자른 김밥조각을 최소 M개 만들고 싶다. P를 최대한 길게 하고 싶을 때, P는 얼마로 설정해야 하는지 구하시오.
```python
import sys
input = sys.stdin.readline

n,k,m = map(int, input().split())
kimbap, p = [],-1
for i in range(n):
    x = int(input())

    # 꼬다리 계산하기
    if x > 2 * k:
        kimbap.append(x - 2 * k)
    elif x > k and x < 2 * k:
        kimbap.append(x - k)

# 김밥 길이 계산하기 -> binary search
if kimbap:
    kimbap.sort()
    start, end = 1, max(kimbap)

while start <= end:
    # 안넣어주면 틀렸습니다 나오길래 넣어줬음
    if start > end:
        break
    mid = (start+end)//2
    sum = 0
    for i in kimbap:
        sum += i // mid
        if sum > m:
            break

    if sum >= m:
        p = max(p, mid)
        start = mid +1
    else:
        end = mid -1
print(p)
```
마찬가지로 이분탐색을 이용하는 문제였는데, 아직 감이 확 잡히지 않아서 다시 처음부터 짜 볼 예정이다.