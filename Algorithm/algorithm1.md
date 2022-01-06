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


## [10. 윤년(2753번)](https://www.acmicpc.net/problem/2752)
연도가 주어졌을 때, 윤년이면 1, 아니면 0을 출력하는 프로그램을 작성하시오.   
윤년은 연도가 4의 배수이면서, 100의 배수가 아닐 때 또는 400의 배수일 때이다.
```python
a=int(input())
if a % 4 == 0 and a % 100 != 0:
    print(1)
elif a % 400 ==0:
    print(1)
else:
    print(0)
```
### 숏코딩
```python
a=int(input())
print(int(a%400==0 or (a%100!=0 and a%4==0)))
```
조건문 없이 논리연산만으로도 가능하다.


## [11. 체스판 조각(3004번)](https://www.acmicpc.net/problem/3004)
상근이는 체스판을 최대 N번 자를 수 있으며, 변에 평행하게만 자를 수 있다. 또, 자를 때는 체스판의 그 변의 한쪽 끝에서 다른쪽 끝까지 잘라야 한다. 자른 후에는 조각을 이동할 수 없다.

이때, 최대 몇 조각을 낼 수 있는지 구하는 프로그램을 작성하시오.
```python
import math
n = int(input())
print(int((math.ceil(n/2))+1)*(n//2+1))
```
처음에는 round 함수를 썼는데 1/2를 했을 때 1이 아닌 0이 나왔다.  
> 파이썬의 반올림은 반올림 하려는 수가 올림, 내림했을 때 동일하게 차이가 나는 경우에는 *짝수* 값으로 반올림 합니다.  

python에서 0은 짝수로 치니.. 제대로 된 답이 나오지 않음!


## [12. 방학 숙제(5532번)](https://www.acmicpc.net/problem/5532)
방학은 총 L일이다. 수학은 총 B페이지, 국어는 총 A페이지를 풀어야 한다. 상근이는 하루에 국어를 최대 C페이지, 수학을 최대 D페이지 풀 수 있다.

상근이가 겨울 방학동안 숙제를 하지 않고 놀 수 있는 최대 날의 수를 구하는 프로그램을 작성하시오.
```python
import math
n = int(input())
a = int(input())
b = int(input())
c = int(input())
d = int(input())

k = n-math.ceil(b/d)
l = n-math.ceil(a/c)
if k<l:
    print(k)
else:
    print(l)
```
### 숏코딩
```python
l,a,b,c,d=map(int,open(0))
print(l+min(-a//c,-b//d))
```
여기서 map을 이용할 수 있을 줄은 몰랐다.  
open(0)에 관해서는 이터레이터 공부가 좀 필요할 것 같다.  
  
우선 국어, 수학을 푸는데 걸리는 시간 중 가장 작은 값을 찾기 위해서 -를 사용하고 min 함수를 사용한 듯 하다. 두개의 값 중 작은 값을 l에 더해주면 되므로 매우 간단한 코드 완성..


## [13. 상근날드(5543번)](https://www.acmicpc.net/problem/5543)
햄버거와 음료의 가격이 주어졌을 때, 가장 싼 세트 메뉴의 가격을 출력하는 프로그램을 작성하시오.
```python
a,b,c,d,e=map(int,open(0))
print(min(a,b,c)+min(d,e)-50)
```
어제 배운 숏코딩을 이용해서 풀었다.


## [14. 타임 카드(5575번)](https://www.acmicpc.net/problem/5575)
직원 A 씨, B 씨, C 씨의 출근 시간과 퇴근 시간이 주어 졌을 때 각 직원의 근무시간을 계산하는 프로그램을 작성하라.
```python
for _ in range(3):
    a = list(map(int,input().split()))
    r = (a[3]*60*60 + a[4]*60 + a[5]) - (a[0]*60*60 + a[1]*60 + a[2])
    h = r//60//60 % 24
    m = r//60 % 60
    s = r % 60
    print(h, m, s)
```
단순한 사칙연산 문제였지만 time문을 쓰려다가 더 복잡하게 되었다.  
문제의 답이 잘 안보일 땐 단순하게 생각하는 능력 기르기!


## [15. 시험 점수(5596번)](https://www.acmicpc.net/problem/5596)
민국이의 총점 S와 만세의 총점 T 중에서 큰 점수를 출력하는 프로그램을 작성하시오.
```python
a = sum(list(map(int,input().split())))
b = sum(list(map(int,input().split())))
print(max(a,b))
```


## [16. 시험 점수(5596번)](https://www.acmicpc.net/problem/5596)
상근이의 여자친구는 항상 이진수에 17을 곱한다. 즉, 이진수 N이 입력으로 들어오면 17을 곱한 다음 이진수로 출력하는 프로그램을 작성하시오.
```python
print(bin(int(input(),2)*17)[2:])
```
2진수 변환 : bin(값,2)


## [17. Contest Timing(5928번)](https://www.acmicpc.net/problem/5928)
 Given the date and time she stops working, please help Bessie compute the total number of minutes she will have spent on the contest.(start time : 11:11 AM on 11/11/11.) (output : minutes)
```python
d,h,m=map(int,input().split())
r = (d*24*60+h*60+m)-(11*24*60+11*60+11)
if r<0:print(-1)
else: print(r)
```
### 숏코딩
```python
d,h,m=map(int,input().split())
print(max((d*24*60+h*60+m)-(11*24*60+11*60+11),-1))
```
-1 조건을 제대로 못봐서 틀렸는데, max를 이용하여 더 짧게 코딩할 수 있었다!


## [18. Speed fines are not fine!(6763번)](https://www.acmicpc.net/problem/6763)
The input will be two integers. The first line of input will be speed limit. The second line of input will be the recorded speed of the car.
```python
a=int(input())
b=int(input())
r=b-a
if r>30:
    print('You are speeding and your fine is $500.')
elif r>20:
    print('You are speeding and your fine is $270.')
elif r>0:
    print('You are speeding and your fine is $100.')
else:
    print('Congratulations, you are within the speed limit!')
```
### 숏코딩
```python
a,b=int(input()),int(input())
d=b-a
print(["Congratulations, you are within the speed limit!",f"You are speeding and your fine is ${[10,[27,50][d>30]][d>20]}0."][b>a])
```
이건 쓸 수 있을 것 같은데 막상 코드로 안뱉어짐.... 여러번 봐야지


## [19. Sounds fishy!(6764번)](https://www.acmicpc.net/problem/6764)
The output is one of four possibilities. If the depth readings are increasing, then the output should be Fish Rising. If the depth readings are decreasing, then the output should be Fish Diving. If the depth readings are identical, then the output should be Fish At Constant Depth. Otherwise, the output should be No Fish.
```python
a,b,c,d=int(input()),int(input()),int(input()),int(input())
print([[['No Fish','Fish At Constant Depth'][a==b==c==d],'Fish Rising'][a<b<c<d],'Fish Diving'][a>b>c>d])
```
숏코딩 형식으로 풀어보았다.


## [20. Sounds fishy!(6764번)](https://www.acmicpc.net/problem/6764)
A goal is only counted if the 4 players, in order, who touched the ball prior to the goal have jersey numbers that are in strictly increasing numeric order with the highest number being the goal scorer.  
Given a jersey number of the goal scorer, indicate how many possible combinations of players can produce a valid goal.
```python
a=int(input())
print((a-3)*(a-2)*(a-1)//6)
```
a-1에서 3개를 고르는 경우이므로 조합공식을 이용하여 구했다.


## [21. Which Alien?(6778번)](https://www.acmicpc.net/problem/6778)
TroyMartian, who has at least 3 antenna and at most 4 eyes;  
VladSaturnian, who has at most 6 antenna and at least 2 eyes;  
GraemeMercurian, who has at most 2 antenna and at most 3 eyes.  
The first line contain the number of antenna that the witness claimed to have seen on the alien. The second line contain the number of eyes seen on the alien.
```python
a,e=int(input()),int(input())
if a>=3 and e<=4:
    print('TroyMartian')
if a<=6 and e>=2:
    print('VladSaturnian')
if a<=2 and e<=3:
    print('GraemeMercurian')
```


## [22. Koszykarz(8710번)](https://www.acmicpc.net/problem/8710)
키, 트레이너가 원하는 키, 때렸을 때 커지는 키 각 3개의 인자가 한 줄로 주어지며 여기서 최소 몇 번을 때려야 트레이너가 원하는 키가 될 수 있는지에 대한 프로그램을 작성하여라.
```python
import math
k,w,m=map(int,input().split())
print(math.ceil((w-k)/m))
```



