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
        return [x//4,x%4]

x,y=map(int,input().split())
print(x,y)

x=four(x)
y=four(y)
print(abs(x[0]-y[0])+abs(x[1]-y[1])+1)
```

## [8. 수 정렬하기 3(10989번)](https://www.acmicpc.net/problem/10989)
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