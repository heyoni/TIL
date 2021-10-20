# 백준 알고리즘 - Bronze IV
https://solved.ac/problems/level/2


## [1. A/B(1008번)](https://www.acmicpc.net/problem/1008)
두 정수 A와 B를 입력받은 다음, A/B를 출력하는 프로그램을 작성하시오.
```python
a, b = list(map(int, input().split()))
print(a/b)
```
### map
- 형과 리스트를 넣으면 형으로 변환 후 다시 리스트로 반환해 줌.
- ```map(int, input().split())``` 는 input을 받은 값을 int형으로 변환 후 리스트로 반환해준다.


## [2. TV 크기(1297번)](https://www.acmicpc.net/problem/1297)
TV의 대각선 길이와, 높이 너비의 비율이 주어졌을 때, 실제 높이와 너비의 길이를 출력하는 프로그램을 작성하시오.
```python
import math

D, H, W = map(int, input().split())
n = math.sqrt(D**2 / (H**2 + W**2))
print(int(n*H),int(n*W))
```
피타고라스의 정리를 이용하여 문제를 풀 수 있음.
$$a^{2}+b^{2}=c^{2}$$
비율은 같으므로 계산 한 뒤 곱해주면 된다.  
- 내가 헷갈렸던 부분 : 만약, 실제 TV의 높이나 너비가 소수점이 나올 경우에는 그 수보다 작으면서 가장 큰 정수로 출력한다. (예) 1.7 -> 1  
- 마지막에 int 형으로만 바꾸면 되는데 소숫점 때 int형으로 변환하여 값이 나오지 않았다.


## [3. 두 수 비교하기(1330번)](https://www.acmicpc.net/problem/1330)
두 정수 A와 B가 주어졌을 때, A와 B를 비교하는 프로그램을 작성하시오.
```python
a, b = list(map(int, input().split()))
if a > b:
    print('>')
elif a < b :
    print('<')
else:
    print('==')
```
### 숏코딩

```python
a,b=map(int,input().split())
print(['><'[a<b],'=='][a==b])
```
앞부분은 리스트, 뒷부분은 인덱스.  
a==b 이라면 참(1)이 되므로 '=='을 나타내며  
a=/=b 이라면 거짓(0)이 되므로 0번째 리스트에서 다시 참거짓을 판단한다!  
_(너무 신기한 문법이군)_


## [4. 사파리월드(2420번)](https://www.acmicpc.net/problem/2420)
두 서브도메인의 유명도가 주어졌을 때, 그 차이를 구하는 프로그램을 작성하시오.
```python
a,b=map(int,input().split())
print(abs(a-b))
```
~~오랜만에 보는~~ 절대값 : abs 함수를 사용하면 된다.


## [5. 주사위 세개(2480번)](https://www.acmicpc.net/problem/2480)
1에서부터 6까지의 눈을 가진 3개의 주사위를 던져서 다음과 같은 규칙에 따라 상금을 받는 게임이 있다. 

1. 같은 눈이 3개가 나오면 10,000원+(같은 눈)×1,000원의 상금을 받게 된다. 
2. 같은 눈이 2개만 나오는 경우에는 1,000원+(같은 눈)×100원의 상금을 받게 된다. 
3. 모두 다른 눈이 나오는 경우에는 (그 중 가장 큰 눈)×100원의 상금을 받게 된다.

3개 주사위의 나온 눈이 주어질 때, 상금을 계산하는 프로그램을 작성 하시오.
```python
a,b,c=map(int,input().split())
if a==b==c:
    print(10000+a*1000)
elif a==b or a==c:
    print(1000+a*100)
elif b==c:
    print(1000+b*100)
else:
    print(max(a,b,c)*100)
```
### 숏코딩
```python
a,b,c=sorted(map(int,input().split()))
print(((1000+100*b,c*100)[a!=b and b!=c],10000+1000*a)[a==c])
```
3번 '두 수 비교하기'에서 봤던 리스트와 인덱스를 이용하여 짧게 코딩할 수도 있다.


## [6. 오븐 시계(2525번)](https://www.acmicpc.net/problem/2525)
훈제오리구이를 시작하는 시각과 오븐구이를 하는 데 필요한 시간이 분단위로 주어졌을 때, 오븐구이가 끝나는 시각을 계산하는 프로그램을 작성하시오.

```python
import datetime
d = datetime.datetime.strptime(input(), '%H %M')
r = d+datetime.timedelta(minutes=int(input()))
print(r.hour, r.minute)
```
우선 입력받은 숫자들을 datetime 형식으로 바꿔준다. 그리고 두번째 줄에서 입력받은 값을 timedelta를 이용하여 연산하고 그 결과를 표시해준다.  
시간 값의 hour, minute은 '.'을 이용하여 접근할 수 있다.
- strftime : 시간을 문자열로 출력하기
- timedelta : 시간 연산/ 주는 week, 일은 days... 여기서는 분으로 입력받으므로 min사용


## [7. 인공지능 시계(2530번)](https://www.acmicpc.net/problem/2530)
훈제오리구이를 시작하는 시각과 오븐구이를 하는 데 필요한 시간이 초 단위로 주어졌을 때, 오븐구이가 끝나는 시각을 계산하는 프로그램을 작성하시오.

```
d = datetime.datetime.strptime(input(), '%H %M %S')
r = d+datetime.timedelta(seconds=int(input()))
print(r.hour, r.minute, r.second)
```
위에서 풀었던 방식과 같다.



## [8. 곱셈(2588번)](https://www.acmicpc.net/problem/2588)
```python
a = int(input())
b = input()
c = list(map(int,list(b)))[::-1]
for i in c:
    print(a*i)
print(a*int(b))
```


## [9. 세 수 정렬(2752번)](https://www.acmicpc.net/problem/2752)
숫자 세 개가 주어졌을 때, 가장 작은 수, 그 다음 수, 가장 큰 수를 출력하는 프로그램을 작성하시오.
```python
a = ' '.join(list(map(str,(sorted(list(map(int,input().split())))))))
print(a)
```
숫자 세 개를 int형으로 변환하여 정렬한 뒤 그걸 다시 string 형으로 변환해준다. 그 다음 join을 이용하여 문자열로 만들어서 print 해줌.
- 더 좋은 방법이 있을 것 같음..