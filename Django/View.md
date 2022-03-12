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

## FBV(Function Based View)

```python
def AFunc(request, pk): # pk의 이름을 바꾸고 싶으면 아래 '종류'를 바꿔줘야 함
  Model.objects.get(pk=pk) # 값-종류
  ...
  return render(request, '연결해줄url')
```

html에서 django model을 접근 할 떄는 `소문자.속성`으로 접근함.

```django
{{ models.name }}
{{ models.type }}
```

## CBV(Class Based View)

- python은 '일급함수'지원 : 함수를 통해 새로운 함수를 만든다.  
  js의 '하이워드 컴포넌트'

- `model._meta_model_name` : 현재 모델의 모델명 알아내기  
  `model._meta_app_name` : 현재 앱 이름 알아내기

- as_view 구동방식

  ```python
  def as_view(cls, model):
    def view(request, *args, **kwargs):
      self = cls(model)
      return self.dispatch(request, *args, **kwargs)
    return view
  ```

  위와 같은 함수를 '순수함수'라고 부른다.  
  view 함수가 호출될 떄 마다 cls 인스턴스를 만들어서 dispatch 요청한다.

  dispatch 함수의 구동방법은 다음과 같다.

  `self.get_object`를 호출하여 현재 모델 record를 획득하고 render 함수에서 request를 주고 `get_template_name`으로 경로도 얻어낸다. 그 후 dict형태로 반환한다.
