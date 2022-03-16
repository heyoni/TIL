# DRF

## 용어정리

### `HyperlinkedModelSerializer`

- entities(요소들) 사이에서 관계를 표현하는 방법 중 하나.
- id 필드는 기본이 아니다
- HyperlinkedIdentifyField를 사용하는 url 필드가 포함됨
- PrimaryKeyRelatedField를 사용하는 대신에 HyperlinkedIdentifyField를 사용함

### `ViewSets`

- 여러 보기를 작성하는 대신 모든 일반적인 동작을 ViewSets 클래스로 그룹화한다.
- 필요한 경우 이를 Views로 쉽게 나눌 수 있지만 ViewSets을 사용하면 보기 논리가 매우 간결할 뿐만 아니라 멋지게 구성된다.
- 라우터 클래스에 Viewsets을 동록하면, API에 대한 URLconf를 자동으로 설정할 수 있다.

```python
...
router = routers.DefaultRouter()
router.register(r'users', views.UserViewSet)
router.register(r'groups', views.GroupViewSet)
...
```

### `Serializer`

- 직렬화, 역직렬화하는 방법을 제공해줌.

### `suffix`

- format suffix를 사용하면 지정된 형식을 명시적으로 참조하는 URL이 되며 API가 http://.../api/items/4.json 과 같은 URL을 처리할 수 있다. 그러려면 format 키워드를 넣어줘야 함.

## Restful 파이썬 웹 서비스 제작(책)

### 1장

1. POST 요청 시

   - HTTP요청을 작성하여 보내야 함
   - JSON 키 값 쌍으로 필드-이름 값을 제공
   - 유효성 검사/ 후 DB에 저장한다.

2. 직렬화 - 역직렬화

   - 직렬화기(Serializer) 클래스 : JSON으로의 직렬화, 역직렬화를 관리한다.

3. 역할
   - 파이썬프리미티브 - 직렬화기 - 모델인스턴스
   - 파이썬프리미티브 - 파서/렌더러 - HTTP 요청/응답  
     \*여기서 직렬화기는 `ProductSerializer(serialziers.Serializer)`를 의미
4. 예제

   ```python
   product_serializer1 = ProductSerializer(product1)
   print(product_serializer1)
   ```

   `rest_framework.utils.serializer_helpers.ReturnDict` 딕셔너리를 보여줌

   ```json
   // 형태는 다음과 같다
   { "data": "2022-03-17", "category": "phone" }
   ```

5. JSONRenderer

   - JSONRenderer()를 이용하면 data 속성에 저장된 딕셔너리를 JSON으로 쉽게 만들 수 있다.

6. 역직렬화

   1. 문자열을 Byte 형태로 만든다
   2. 변수에 저장한다.
   3. `django.utils.six.BytesIO`를 이용하여 버퍼링된 I/O를 구현한다
   4. JSON Byte로부터 스트림을 만든다
   5. 인스턴스에 저장한다.
   6. 새 변수에 저장한다.

7. 직렬화

   1. `rest_framwork.renderers.JSONRender`를 이용한다
   2. Serializer를 이용한다.

8. Serializer 값에 접근하려면 `is_valid`를 꼭 호출해야 한다.

   - `is_valid`는 접근 가능여부를 True, False형태로 반환함

9. JSONResponse 클래스
   - `HTTPResponse`의 서브 클래스
   - 문자열로 된 HTTP 응답을 나타낸다.
   - 내용을 JSON으로 렌더링한다.
   - `__init__`메서드만 선언한다.
     - (동작 순서) JSONRender 인스턴스를 생성하고 render 메서드를 화출한다. 데이터를 JSON으로 렌더링 하고 반환된 Byte문자열을 content 로컬 변수에 저장한다. application/json 응답헤더에 content_type 키를 값으로 추가한다. 마지막으로 초기자를 호출한다.
10. HTTP요청을 받을 경우
    - django.http.HTTPResponse 객체를 생성한다.
    - 객체에는 HTTP동사와 요청(meta data)가 들어감
    - method 속성으로는 요청에 사용된 메서드(view) 또는 HTTP 동사
    - view 함수는 django.http.HTTPResponse를 반환한다.
    - 예시  
      product_list 함수는 product를 나열하거나 생성한다. 👉ㅤGET/POST 요청 처리 가능  
      method 속성 값을 점검하여 HTTP 동사에 따라 실행코드를 다르게 한다.
      - GET : `request.method == 'GET'`
        이떄, 모든 product 객체를 얻고 productSerializer를 사용하여 모두 직렬화 한다. 그리고 JSONResponse 인스턴스를 반환함. `many=True` 속성이 있으면 여러 인스턴스를 직렬화 할 수 있고 이때 ListSeirialzier를 사용한다.
      - POST: `request.method == 'POST'`
        JSONParser인스턴스를 사용하여 request를 인자로 받는 parse메서드를 호출하여 요청 속에 들어있는 JSON 데이터를 파싱하여 새 변수에 저장한다. ProductSerializer 클래슬르 사용하여 is_valid 메서드를 통해 인스턴스가 유효한지 확인한다. 유효하다면 save로 DB에 저장하고 201 created 상태를 담은 JSONResponse 인스턴스 반환
      - (pk값이 있을 경우) : `Product.objects.get`을 이용하여 DB에서 해당 인스턴스를 호출하여 로컬 변수에 저장해준다. ex) `product = Product.objects.get(pk=pk)`
      - GET : product를 인자로 하여 ProductSerializer 인스턴스 생성 후 JSONResponse에 202 상태코들 넣고 직렬화 된 데이터를 반환한다.
      - PUT : 요청된 JSON 데이터(사용자에게서 받아온 수정할 데이터)값을 새 product를 만들어 기존 product를 대체한다.  
        JSONParser인스턴스를 사용하여 request를 인자로 받는 parse메서드를 호출하여 요청 속에 들어있는 JSON 데이터를 파싱하여 새 변수에 저장한다. ProductSerializer 클래슬르 사용하여 is_valid 메서드를 통해 인스턴스가 유효한지 확인한다. 유효하다면 save로 DB에 저장하고 201 created 상태를 담은 JSONResponse 인스턴스 반환 - DELETE : 앞에서 얻은 product 인스턴스에서 delete 메서드를 호출하고 테이블 내 행을 삭제한다. 정상적으로 삭제되었으면 204 상태코드를 반환함.
