# View

## View란?

- 1개의 HTTP요청에 대해 응답
- view는 함수가 아닌, '호출 가능한 객체'
- FBV를 제대로 이해해야 CBV를 응용할 수 있다.
- `def 함수(request, 인자)` 형태로 사용함  
   request : HTTPRequest객체이며, 현재 요청에 대한 모든내용이 들어있음
  인자 : url captured values
- 리턴값은 튜플이다.
  ```python
  def test(request, pk):
      ...
      return render(request, 'URL'{ ... })
  ```
- 반드시 HTTPRequest를 리턴해야하며 HTTPRequest는 str, bytes, file객체를 응답해준다.  
   (응답 시 타입 힌트를 주는 게 요즘 트랜드 👉 `def index(request:HTTPRequest, pk:int))`
