# 모델 관계

## 1. Many-to-one(1:N)

- 하나의 모델에 여러개의 다른 모델이 연관되어 있을 때 사용.
- ForeignKey를 이용하여 N측에 명시해준다.
- `models.ForeignKey(모델명, on_delete='')`
- `on_delete` 속성 : 1측 모델이 삭제되었을 경우, N측 모델을 어떻게 할 것인지에 대해 정해놓음(CASCADE, PROTECT, SET_NULL, SET_DEFAULT, SET, DO_NOTTING)
- 1:N 관계에서 모델에 접근하기(1:N, 1명의 user 여러개의 post)

  - `post.obejcts.filter(user_id=1)`
  - `post.obejcts.filter(user__id=1)`
  - `user = User.objects.first()`
    `post.obejcts.filter(user=user)`
  - `user.comments_set.all()`
  - 모두 같은의미, 마지막 코드가 가장 사용하기 좋음.
  - (추가)  
     `user_id` : post에 외래키로 저장되는 직접적인 필드  
     `user__id` : 실제 user쪽에 있는 id를 의미한다.

### `reverse_name`

- 1:N의 관계에서 1측에서 사용.  
  참조할 이름이 없기 때문에 "모델명소문자\_set"이라는 이름이 default로 생긴다.
- 이름을 변경하고 싶으면 외래키 지정 시 `related_name`사용

### `limit_choices_to`

- admin 페이지에서 보여지는 항목들에 대해 조건을 걸 수있음.
- 외래키 지정시 `limit_choices_to = {'항목':True/False}`로 사용

## 2. one-to-one(1:1)

- 1:N 관계의 models.ForeignKey(unique=True)와 유사함  
  구분되는 점은 `reverse_name`의 차이임. - (1:N) 👉 `profile.user_set.all()` - (1:1) 👉 `profile.user`/ `user.profile`로 접근함
- `models.OneToOneField(모델명, on_delete='')`
- `reverse_name`도 마찬가지로 '모델명소문자'
- (Tip) 사용자 모델을 가져올 때는 아래와 같이 사용해야 함
  ```python
  from django.contrib.auth import get_user_model
  User = get_user_model()
  User.objects.all()
  ```
- (Tip) A모델이 만들어짐과 동시에 B모델을 만들어야 한다면 'signal'을 사용  
  event handler 와 비슷

## 3. Many-to-many(M:N)

- 어느쪽이든 지정할 수 있으나 다른 모델을 활용하는 쪽에다 모델 지정  
  ex) M개의 post에 N개의 tag일 경우, tag를 활용하는 post에 지정
- 쿼리셋을 넣어 추가나 삭제가 가능함.

  ```python
  tag = Tag.objects.get(name="인스타그램")
  post.tag_set.add(tag)
  post.tag_set.remove(tag)

  tag_qs = Tag.objects.all()
  post.tag_set.add(*tag_qs)
  ```
