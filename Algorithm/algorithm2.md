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