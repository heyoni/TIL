# 백준 알고리즘
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
숏코딩

```python
a,b=map(int,input().split())
print(['><'[a<b],'=='][a==b])
```
앞부분은 리스트, 뒷부분은 인덱스.  
a==b 이라면 참(1)이 되므로 '=='을 나타내며  
a=/=b 이라면 거짓(0)이 되므로 0번째 리스트에서 다시 참거짓을 판단한다!  
_(너무 신기한 문법이군)_