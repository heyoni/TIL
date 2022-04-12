# 백준 알고리즘 - Bronze III

https://solved.ac/problems/level/3

## [1. 분산처리(1009번)](https://www.acmicpc.net/problem/1009)

입력의 첫 줄에는 테스트 케이스의 개수 T가 주어진다. 그 다음 줄부터 각각의 테스트 케이스에 대해 정수 a와 b가 주어진다.  
각 테스트 케이스에 대해 마지막 데이터가 처리되는 컴퓨터의 번호를 출력한다.

```python
a=int(input())
r=[]
for i in range(a):
    x,y=map(int,input().split())
    x=int(str(x)[-1])
    if x==1 or x==5 or x==6:
        r.append(x)
    elif x==2:
        r.append([2,4,8,6][(y-1)%4])
    elif x==3:
        r.append([3,9,7,1][(y-1)%4])
    elif x==4:
        r.append([4,6][(y-1)%2])
    elif x==7:
        r.append([7,9,3,1][(y-1)%4])
    elif x==8:
        r.append([8,4,2,6][(y-1)%4])
    elif x==9:
        r.append([9,1][(y-1)%2])
    elif x==0:
        r.append(10)

for i in r:
    print(i)
```

처음에는 제곱을 사용했는데 시간초과 오류가 나서 패턴들을 분석해봤다.  
제곱근의 끝 자리가 일정 패턴으로 반복되는 것을 확인할 수 있었고 이를 토대로 그냥 막 만들어봄.  
최적화는 다음에...

## [2. 8진수 2진수(1212번)](https://www.acmicpc.net/problem/1212)

8진수가 주어졌을 때, 2진수로 변환하는 프로그램을 작성하시오.

```python
print(bin(int(input(),8))[2:])
```

- 2진수 bin()
- 8진수 oct()
- 16진수 hex()
- n진수에서 10진수로 바꾸기 : int('숫자',n)

## [3. 부호(1247번)](https://www.acmicpc.net/problem/1247)

8진수가 주어졌을 때, 2진수로 변환하는 프로그램을 작성하시오.

```python
import sys
input=sys.stdin.readline
a=[]
for i in range(3):
    n = int(input())
    s = [int(input()) for _ in range(n)]
    print([['-','+'][sum(s)>0],'0'][sum(s)==0])
```

- input : 입력받은 값의 개행 문자를 삭제시켜서 리턴함.
- sys.stdin.readline : 값을 불러오는 명령어, 개행 문자 포함하여 리턴.
  👉 삭제작업이 있기 때문에 input이 더 느림

## [4. 핸드폰 요금(1267번)](https://www.acmicpc.net/problem/1267)

- 영식 요금제 : 30초 마다 20원 씩 청구
- 민식 요금제 : 60초 마다 15원 씩 청구

통화 시간 목록이 주어지면 어느 요금제를 사용 하는 것이 저렴한지 출력하는 프로그램을 작성하시오.  
영식은 Y로, 민식은 M으로 출력한다.

```python
import math
n=input()
k=list(map(int,input().split()))
y=sum([math.ceil((k[i]+1)/30)*10 for i in range(len(k))])
m=sum([math.ceil((k[i]+1)/60)*15 for i in range(len(k))])
print([['M '+str(m),'Y '+str(y)][y<m],'Y M '+str(y)][y==m])
```

n은 의미없음.  
k로 통화 시간을 받아오고, y와 m을 list comprehension을 이용하여 계산해주었다.

## [5. 집 주소(1284번)](https://www.acmicpc.net/problem/1284)

- 0일 경우 +4, 1일 경우 +2, 나머지 +3
- 각 숫자사이에 간격과 양 옆의 여백도 더해야함
  입력은 마지막에 0이 들어오기 전까지 계속해서 줄 단위로 주어진다.  
  또한, 마지막의 0은 처리하지 않는다.

```python
while True:
    n=input()
    r=0
    if n=='0':
        break
    for i in list(n):
        if int(i)==1:
            r+=2
        elif int(i)==0:
            r+=4
        else:
            r+=3
    r+=len(list(n))+1
    print(r)
```

while 조건 : 조건이 참이면 계속 루프를 돈다.

## [6. 공(1547번)](https://www.acmicpc.net/problem/1547)

- 컵을 이동시킬 횟수 M번을 입력받고, X Y 인자값을 입력받아 컵을 이동시킨다.  
  마지막에 공이 있는 컵의 위치를 출력하는 문제.(공은 처음에 1번 컵 아래에 있다.)

```python
a=int(input())
k=1
for i in range(a):
    x,y=map(int,input().split())
    k=[[k,x][y==k],y][x==k]
print(k)
```

리스트형을 잘 이해하니 쉬웠던 문제.

## [7. 꼬리를 무는 숫자 나열(1598번)](https://www.acmicpc.net/problem/1598)

- 두 개의 자연수를 아무거나 생각한다. 그리고 숫자판에서 두 개의 자연수 사이의 직각거리를 구하면 된다.

```python
def four(x):
    if x%4==0:
        return [x//4,4]
    else:
        return [x//4+1,x%4]

x,y=map(int,input().split())

x=four(x)
y=four(y)
print(abs(x[0]-y[0])+abs(x[1]-y[1])+1)
```

## [8. 문어 숫자(1864번)](https://www.acmicpc.net/problem/1864)

- 한 줄에 하나씩 문어 숫자가 입력으로 주어진다. 각 숫자는 최소 한 개, 최대 여덟 개의 문어 숫자 기호로 이루어져있다. 입력으로 '#'이 들어오면 입력을 종료한다.

```python
def find_num(i):
    string='-\(@?>&%'
    return string.find(i)
n=''

while True:
    n = input()
    if n == '#':
        break
    answer = 0
    minus = 1
    l = len(n)-1
    for i in n:
        answer += (find_num(i)*8**l)
        l -= 1
    print(answer)
```

더 쉬운 방법이 있을 것 같다.

## [9. 생장점(1703번)](https://www.acmicpc.net/problem/1703)

- 입력의 각 줄은 하나의 branchorama 나무를 의미합니다.  
  각 줄은 나무의 나이 a(1 ≤ a ≤ 20)로 시작하며, 그 뒤로 2a 개의 정수가 공백을 두고 주어집니다. 2a 개의 정수는 splitting factor와 가지치기 한 가지의 수가 level 별로 나열된 것입니다.  
  마지막 줄로 '0'이 주어지며 더 이상의 입력은 없습니다. '0'은 처리하지 않습니다.

```python
while True:
    l = list(map(int,input().split()))
    if l[0] == 0:
        break
    answer = 1
    for i in range(1,l[0]*2+1):
        if i % 2 ==1:
            answer *= l[i]
        else:
            answer -= l[i]

    print(answer)
```

문제 푸는 시간보다 문제를 이해하는 시간이 더 길었다.  
생장점, 즉 꼭대기의 개수를 구하는 문제인데 연산문제라 매우 쉬웠다.

## [10. 블랙잭(2798번)](https://www.acmicpc.net/problem/2798)

- N장의 카드에 써져 있는 숫자가 주어졌을 때, M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 구해 출력하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N, M = map(int,input().split())
cards = list(map(int,input().split()))
sum = 0

# 1. 모든 수 계산
for i in range(N):
    for j in range(i+1, N-1):
        for k in range(j+1, N):
            if cards[i] + cards[j] + cards[k] > M:
                continue
            else:
                sum = max(sum, (cards[i]+cards[j]+cards[k]))


print(sum)
```

브루스 포트 알고리즘을 이용하는 문제.  
 브루스 포트(brute force) : 답이 나올 때까지 가능한 모든 조합을 다 탐색한다.  
세그먼트 트리로 계산하려 했는데, 풀다보니 세그먼트 트리는 모든 조합 계산이 아니었다..!

## [11. 분해합(2231번)](https://www.acmicpc.net/problem/2231)

- 자연수 N이 주어졌을 때, N의 가장 작은 생성자를 구해내는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())

# 1. 구현하기 -> 입력의 절반부터 올라가면서 모든 수의 분해합을 구해본다.
result = 0
for i in range(N//2,N):
    sum = i
    for j in str(i):
        sum += int(j)

    if sum == N:
        result = i
        break

print(result)
```

'브루스포트'를 이용하여 푸는 문제로, 전부 다 구해보는 코드를 짰다.  
전부 다 구하기에는 시간이 초과될 것 같아서 절반부터 구함.

## [12. 덩치(7568번)](https://www.acmicpc.net/problem/7568)

- 학생 N명의 몸무게와 키가 담긴 입력을 읽어서 각 사람의 덩치 등수를 계산하여 출력하라.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
l = []

for i in range(N):
    x, y = map(int,input().split())
    l.append([x,y])

# 1. 구현하기
for i in l:
    point = 1
    for n in l:
        # 1-1. 몸무게가 같지 않고, 키도 같지 않을 때
        if (i[0] != n[0]) & (i[1] != n[1]):
            # 1-2. 키가 작거나 몸무게가 작으면 순서를 미뤄준다.
            if (i[0] < n[0]) & (i[1] < n[1]):
                point+=1
    # 2. 출력하기 -> 바로 print해줌
    print(point)
```

전부 다 계산하면 비효율적일 것 같아서 몸무게로 정렬을 한 다음 구현하려 했으나, 실력 부족으로..😢 실패했다.  
그래서 그냥 전부 다 탐색하면서 계산했다.

## [13. 영화감독 숌(1436번)](https://www.acmicpc.net/problem/1436)

- 종말의 수는 666이 들어가야 한다. 첫째 줄에 숫자 N이 주어지고, N번째 영화의 제목에 들어간 숫자를 출력하는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
end_number = 666

# 1. 계산하기 -> 666이 있는지 문자열로 확인하고, 있으면 -1을 해줌. 0이되면 종료
while N != 0:
    if '666' in str(end_number):
        N = N-1
        if N == 0:
            break
    end_number += 1

print(end_number)
```

파이썬 문자열함수를 이용하여 666이 들어가있는지를 체크하고, 없을 경우 int형으로 바꿔서 1을 더해준다.

## [14. 팩토리얼(10872)](https://www.acmicpc.net/problem/10872)

- 0보다 크거나 같은 정수 N이 주어진다. 이때, N!을 출력하는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())

# 1. 구현하기
def factorial(f):
    if f == 0:
        return 1
    return f * factorial(f-1)

print(factorial(N))
```

## [15. 수 정렬하기(2750)](https://www.acmicpc.net/problem/2750)

N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
l = []

# 1. 구현하기
for i in range(N):
    l.append(int(input()))

print(*sorted(l))
```

## [16. 수 정렬하기(2108)](https://www.acmicpc.net/problem/2108)

N개의 수가 주어졌을 때, 네 가지 기본 통계값(산술평균, 중앙값, 최빈값, 범위)을 구하는 프로그램을 작성하시오.

```python
# 0. 입력받기
import sys
from collections import Counter
input = sys.stdin.readline

N = int(input())
l = []

# 1. 구현하기
for _ in range(N):
    l.append(int(input()))

l = sorted(l)
k = []

# 산술평균
k.append(round(sum(l)/N))
# 중앙값
k.append(l[N//2])
# 최빈값
cnt = Counter(l).most_common(2)
if len(l) > 1:
    if cnt[0][1] == cnt[1][1]:
        k.append(cnt[1][0])
    else:
        k.append(cnt[0][0])
else:
    k.append(cnt[0][0])
# 범위
k.append(l[-1] - l[0])

print(*k)
```

Counter를 이용하여 최빈값을 쉽게 구할 수 있다.

## [17. 소트인사이드(1427)](https://www.acmicpc.net/problem/1427)

수가 주어지면, 그 수의 각 자리수를 내림차순으로 정렬해라.

```python
# 실패
print(*sorted(list(map(int,str(input()[:-1]))),reverse=True),sep='')
# 성공
print(*sorted(list(input()))[::-1],sep='')
```

둘 다 똑같은 결과가 나오는데 왜 틀렸는지 모르겠다.

## [18. 좌표 정렬하기(11650)](https://www.acmicpc.net/problem/11650)

좌표가 입력되면 순서대로 정렬하기.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
l = []
# 1.구현하기 -> 리스트에 붙이고 정렬
for i in range(N):
    t = list(map(int,input().split()))
    l.append(t)

l = sorted(l)
for i in l:
    print(*i)
```

x,y를 입력받고 리스트 형태로 리스트에 저장한다. 그 다음 리스트 정렬을 이용하여 오름차순으로 정렬한다.

## [19. 좌표 정렬하기(11651)](https://www.acmicpc.net/problem/11651)

좌표가 입력되면 y값을 기준으로 순서대로 정렬하기.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
l = []

for i in range(N):
    t = list(map(int,input().split()))
    l.append(t)

#구현하기
l.sort(key=lambda x : (x[1],x[0]))
for i in l:
    print(*i)
```

lambda를 이용하여 구현하였다. x[1]번째를 기준으로 정렬하고, 같을 경우 x[0]을 기준으로 정렬해야 하기 떄문에 x[1]이 아닌 `(x[1],x[0])`을 주었다.

## [20. 좌표 정렬하기(1181)](https://www.acmicpc.net/problem/1181)

알파벳 소문자로 이루어진 N개의 단어가 들어오면 아래와 같은 조건에 따라 정렬하는 프로그램을 작성하시오.

1. 길이가 짧은 것부터
2. 길이가 같으면 사전 순으로
   같은 단어가 여러번 입력된 경우는 한 번만 출력한다.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
l = []

for i in range(N):
    l.append(input().strip())

# 1. 구현하기
l = sorted(list(set(l)))
l.sort(key=lambda x : len(x))
print(*l)
```

마찬가지로 lambda를 이용해서 풀었음. 중복처리 조건을 꼼꼼하게 보지 못해서 잠깐 헤맸다.

## [21. 좌표 압축(18870)](https://www.acmicpc.net/problem/18870)

Xi를 좌표 압축한 결과 X'i의 값은 Xi > Xj를 만족하는 서로 다른 좌표의 개수와 같아야 한다.

```python
# 0. 입력받기
import sys
input = sys.stdin.readline

N = int(input())
l = list(map(int,input().split()))

# 1. 해결하기
# set으로 중복을 제거하고, dic을 만들어서 시간복잡도 1로 좌표를 구하게 함
clear_l = sorted(list(set(l)))
dic = {clear_l[i] : i for i in range(len(clear_l))}

for i in l:
    print(dic[i], end=' ')
```

처음에는 index를 이용해서 풀었는데 시간초과가 났다. index는 시간복잡도가 N인 반면 dictionary 형은 시간복잡도가 1이다.

## [22. AxB(10998)](https://www.acmicpc.net/problem/10998)

AxB를 출력하라.

```python
# 0. 입력받기
A,B = map(int,input().split())
print(A*B)
```

쉬어가기

## [22. 달팽이는 올라가고 싶다 - 실패(2869)](https://www.acmicpc.net/problem/2869)

달팽이는 낮에 A미터 올라갈 수 있다. 하지만, 밤에 잠을 자는 동안 B미터 미끄러진다. 또, 정상에 올라간 후에는 미끄러지지 않는다.

달팽이가 나무 막대를 모두 올라가려면, 며칠이 걸리는지 구하는 프로그램을 작성하시오.

```python
A,B,V = map(int,input().split())
count = 1
while True:
    if V <= A * count - B * (count-1):
        print(count)
        break
    count += 1
```

시간초과 난 문제. 효율적으로 어떻게 풀 수 있을까..?
