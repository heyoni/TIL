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