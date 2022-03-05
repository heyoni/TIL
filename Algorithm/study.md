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

## [3. 그르다 김가놈(18113번)](https://www.acmicpc.net/problem/18113)

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

## [4. 게임 개발(1516번)](https://www.acmicpc.net/problem/1516)

- 첫째 줄에 건물의 종류 수 N(1 ≤ N ≤ 500)이 주어진다. 다음 N개의 줄에는 각 건물을 짓는데 걸리는 시간과 그 건물을 짓기 위해 먼저 지어져야 하는 건물들의 번호가 주어진다. 건물의 번호는 1부터 N까지로 하고, 각 줄은 -1로 끝난다고 하자. 각 건물을 짓는데 걸리는 시간은 100,000보다 작거나 같은 자연수이다. 모든 건물을 짓는 것이 가능한 입력만 주어진다.

- N개의 각 건물이 완성되기까지 걸리는 최소 시간을 출력한다.

```python
import sys
from collections import deque
input = sys.stdin.readline

N = int(input())
time = [0] * (N+1)
indegree = [0] * (N+1)
graph = [[] for _ in range(N+1)]

for i in range(1,N+1):
    a = list(map(int,input().split()))
    time[i] = a[0]
    for j in a[1:-1]:
        graph[j].append(i)
        indegree[i] += 1

def topology_sort():
    result = [0]*(N+1)
    q = deque()

    for i in range(1, N+1):
        if indegree[i] == 0:
            q.append(i)
    for i in range(1, N+1):
        now_node = q.popleft()
        result[now_node] += time[now_node]

        for next_node in graph[now_node]:
            indegree[next_node] -= 1
            result[next_node] = max(result[next_node],result[now_node])
            if indegree[next_node] == 0:
                q.append(next_node)

    print(*result[1:])
topology_sort()
```

이전에 풀었던 문제와 같이 위상정렬을 이용하여 풀었다.  
근데 아직 result를 내는 부분을 명확하게 이해하지 못함.

## [5. 네트워크 연결(1922번)](https://www.acmicpc.net/problem/1922)

- 첫째 줄에 컴퓨터의 수 N (1 ≤ N ≤ 1000)가 주어진다.  
  둘째 줄에는 연결할 수 있는 선의 수 M (1 ≤ M ≤ 100,000)가 주어진다.  
  셋째 줄부터 M+2번째 줄까지 총 M개의 줄에 각 컴퓨터를 연결하는데 드는 비용이 주어진다.  
  이 비용의 정보는 세 개의 정수로 주어지는데, 만약에 a b c 가 주어져 있다고 하면 a컴퓨터와 b컴퓨터를 연결하는데 비용이 c (1 ≤ c ≤ 10,000) 만큼 든다는 것을 의미한다. a와 b는 같을 수도 있다.

- 모든 컴퓨터를 연결하는데 필요한 최소비용을 첫째 줄에 출력한다.

```python
import sys
input = sys.stdin.readline

# 컴퓨터의 수
N = int(input())
# 선의 수
M = int(input())

parent = [i for i in range(N+1)]
edges = []
for _ in range(M):
    a, b, cost = map(int, input().split())
    edges.append((cost, a, b))

# 최소길이로 정렬해 놓음
edges.sort()

# 부모 노드를 찾아야함 -> 사이클을 만들지 않기 위해서
# 부모 노드를 찾기 위해서는 union-find를 사용한다.
# 재귀함수를 통해 가장 작은 값을 가리키는 것을 찾아줌
# ex) 1-2-3이 연결되어 있으면 table은 1 1 2 가 될 것임, 3은 2와 연결되어있고 재귀함수를 통해 2의 연결 값인 1을 연결해준다.
def get_parent(parent, x):
    if parent[x] == x:
        return x
    parent[x] = get_parent(parent, parent[x])
    return parent[x]


# 사이클이 없으면 합쳐준다
# 합쳐주는 이유? 작업 후 두 트리를 하나의 트리로 만들어주기 위해서
def union(parent, a, b):
    a = get_parent(parent, a)
    b = get_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


def kruskal(edges):
    result = 0
    for edge in edges:
        cost, a, b = edge

        if get_parent(parent, a) != get_parent(parent, b):
            union(parent, a, b)
            result += cost
    return result
result = kruskal(edges)
print(result)

```

크루스칼 알고리즘을 사용하는 문제, 조만간 벨로그에 정리할 예정임.

## [6. 구간 합 구하기 4(11659번)](https://www.acmicpc.net/problem/11659)

- 수 N개가 주어졌을 때, i번째 수부터 j번째 수까지 합을 구하는 프로그램을 작성하시오.

```python
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
l = list(map(int,input().split()))
sum_list = [0]
total = 0
# sum_list = [sum(l[:(i)])for i in range(len(l)+1)]
for i in range(len(l)):
    total += l[i]
    sum_list.append(total)

for _ in range(M):
    x, y = map(int,input().split())
    print(sum_list[y]-sum_list[x-1])

```

뭐야 엄청 쉽네! 하고 풀었다가 시간초과가 난 문제.  
찾아보니 '구간트리'를 이용하는 것 같았지만 이번 문제는 잘 생각해보니 누적합을 구하고 그 구간을 보여주면 되는 문제라 쉽게 구했다.  
다만 python list comprehension을 이용하니 시간초과가 생겼는데 이유를 잘 모르겠다.  
알아보고 벨로그에 정리해야지.

## [7. 구간 합 구하기 (2042번)](https://www.acmicpc.net/problem/2042)

- 어떤 N개의 수가 주어져 있다. 그런데 중간에 수의 변경이 빈번히 일어나고 그 중간에 어떤 부분의 합을 구하려 한다. 만약에 1,2,3,4,5 라는 수가 있고, 3번째 수를 6으로 바꾸고 2번째부터 5번째까지 합을 구하라고 한다면 17을 출력하면 되는 것이다. 그리고 그 상태에서 다섯 번째 수를 2로 바꾸고 3번째부터 5번째까지 합을 구하라고 한다면 12가 될 것이다.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline
from math import ceil, log

N, M, K = map(int,input().split())

l = []
segment_tree = [0]*(N*4)


# 1. 트리 만들기
def init(start, end, index):
	# start와 end가 같다면 리프노드이다.
    if start == end:
        segment_tree[index] = l[start-1]
        return segment_tree[index]

    # 현재 노드는 왼쪽 아래 노드와 오른쪽 아래 노드를 더한 값이다.
    mid = (start+end) // 2
    segment_tree[index] = init(start, mid, index*2) + init(mid+1, end, index*2+1)
    return segment_tree[index]


# 2. 트리에서 값 찾기
def find(start, end, index, left, right):
	# 찾으려는 범위가 start~end 범위보다 클 경우
    if start > right or end < left:
        return 0

    # 찾으려는 범위가 segment tree 노드안에 구현되어 있을 경우
    if start >= left and end <= right:
        return segment_tree[index]

	# 코드를 동작시키기 위한 기본 코드
    # 현재 노드는 왼쪽아래 + 오른쪽아래 노드이다.
    mid = (start + end) // 2
    sub_sum = find(start, mid, index*2, left, right) + find(mid+1, end, index*2+1, left, right)
    return sub_sum


# 3. 트리 값 바꿔주기
def update(start, end, index, update_idx, update_data):
	# update 하려는 범위가 초과될 경우
    if start > update_idx or end < update_idx:
        return

    segment_tree[index] += update_data

    # 리프노드까지 바꿔주었으면 재귀함수를 끝낸다.
    if start == end:
        return

	# 내가 관여하고 있는 노드들을 찾아서 바꿔준다 -> 재귀함수로 구현
    mid = (start + end) // 2
    update(start, mid, index*2, update_idx, update_data)
    update(mid+1, end, index*2+1, update_idx, update_data)


for _ in range(N):
    l.append(int(input()))

init(1, N, 1)

for _ in range(M+K):
    a, b, c = map(int,input().split())
    if a == 1:
        temp = c - l[b-1]
        l[b-1] = c
        update(1, N, 1, b, temp)

    elif a == 2:
        print(find(1, N, 1, b, c))
```

해설은 벨로그에 상세히 적어뒀다.
아직 find 하는 부분이 손에 익지 않아서 한번 더 쳐 볼 예정이다.

## [8. 폰 호석만 (21275번)](https://www.acmicpc.net/problem/21275)

- 첫번째 줄에 X를 A진법으로 표현한 값과 X를 B진법으로 표현한 값이 공백으로 구분되어 주어진다. 각 자리수는 0 이상 z 이하이다. a부터 z 는 10부터 35 를 의미한다.  
  만약 문제의 조건에 맞는 X, A, B가 유일하게 존재한다면, X를 십진법으로 표현한 수와 A와 B를 공백으로 나누어 출력하라. 만약 만족하는 경우가 2가지 이상이라면 "Multiple"을, 없다면 "Impossible"을 출력하라.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline
A, B = input().split()
x, a, b = 0, 0, 0 # 출력할 값
count = 0 # 조건에 맞는 값이 몇개인지 카운팅해주는 변수


# 1. A를 가지고 2부터 36진수 중 표현이 가능한 값을 찾음
for i in range(2, 37):
    try:
        a_temp = int(A, i)
    except:
        continue
    # 2. B를 가지고 2부터 36진수 중 표현이 가능한 값을 찾음
    for j in range(2, 37):
        try:
            b_temp = int(B, j)
            # 3. 진수 변환한 값들이 같을 떄
            if a_temp == b_temp:
                count += 1
                x = a_temp
                a = i
                b = j
        except:
            continue

if count == 1:
    print(x,a,b)
elif count == 0:
    print("Impossible")
else:
    print("Multiple")

```

`int(i, j)`는 i를 j로 형변환 해주는 명령어다.

## [9. 호석이 두 마리 치킨 (21278번)](https://www.acmicpc.net/problem/21278)(실패)

- 첫 번째 줄에 건물의 개수 N과 도로의 개수 M 이 주어진다. 이어서 M 개의 줄에 걸쳐서 도로의 정보 Ai , Bi 가 공백으로 나뉘어서 주어진다. 같은 도로가 중복되어 주어지는 경우는 없다. 어떤 두 건물을 잡아도 도로를 따라서 오고 가는 방법이 존재함이 보장된다.
- 한 줄에 건물 2개가 지어질 건물 번호를 오름차순으로 출력하고, 그때 모든 도시에서의 왕복 시간의 합을 출력한다.  
  만약 건물 조합이 다양하게 가능하면, 작은 번호가 더 작은 것을, 작은 번호가 같다면 큰 번호가 더 작은 걸 출력한다.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
my_map = [[float('inf')]*N for _ in range(N)]

# 1. 입력받은 값으로 기본 맵 그리기
for i in range(M):
    A, B = map(int,input().split())
    my_map[A-1][B-1] = my_map[B-1][A-1] = 1

# 1-1. 나 자신은 0으로 초기화
for i in range(len(my_map)):
    my_map[i][i] = 0

# 2. 연결할 수 없는 값 중 다른 간선을 탐색하면서 구하기(플로이드와샬)
for k in range(N):
    for i in range(N):
        for j in range(N):
            my_map[i][j] = min(my_map[i][j], my_map[i][k] + my_map[k][j])

# 3. 출력하기
def find_answer():
    for i in range(N-1):
        for j in range(1,N):
            cnt = [float('inf')]*N
            for k in range(N):
                cnt[k] = min(my_map[i][k], my_map[j][k])
                if min(my_map[i][k], my_map[j][k]) == float('inf'):
                    break
                if float('inf') not in cnt:
                    print(i+1,j+1,sum(cnt)*2)
                    return

find_answer()
```

- 플로이드 와샬을 이용하여 구해보았는데, 6문제까지는 맞췄으나 진전이 없음.  
  플로이드 와샬 : 거쳐가는 정점을 기준으로 최단거리를 구하는 방식
- `float('inf')`는 무한대를 의미함
