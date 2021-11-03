![스크린샷 2021-11-03 오후 3.49.52.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8741770b-64ff-4951-a4a6-e935c183edf3/스크린샷_2021-11-03_오후_3.49.52.png)
클린 아키텍처의 대표 이미지.

- 서비스 로직 등 중요한 요소들은 원 안쪽에 위치하며 정보가 나타나는 view는 원의 테두리에 존재해야 한다.
- 원 안에 있는 요소들은 독립적이며 다른 요소들에 의존하지 않고 작동할 수 있다.
(바깥 쪽에 있는 요소들은 원 안에 있는 요소에 의존적임)

## 사용이유?

- views : 읽기 어렵고 재사용 어려움
- models : 복잡한 모델 의존성을 야기한다
- forms : UI에 논리 결합이 발생한다.
- 기타 : 유닛 테스트가 어렵고 다른 서비스에서 재사용이 어렵다.

## 해결방법?

- inner layer로부터 비즈니스 로직을 독립시키기
- 사용 사례를 중심으로 계층 재구성하기
- 모든 외부 종속성을 위한 연결들을 사용하기(models)
- 호출자가 어댑터를 use cases layer에 삽입하도록 한다.
    
    

## 클린 아키텍처란?

1. 독립적인 프레임워크 : 라이브러리나 소프트웨어에 종속되지 않는다. 제한된 제약 조건에 시스템을 집어넣는 방법 보다는 프레임워크를 툴로 이용하는 방법이 있음.
2. 테스트 : UI, DB, Web Server 등 외부 요소 없이 business rules를 테스트 할 수 있다.
3. 독립적인 UI : buisness rules에 영향을 주지 않는 UI를 변경할 수 있다.
4. 독립적인 DB : 데이터를 다양한 방식으로 저장할 수 있다.
5. 외부 요소로 부터 독립 : business rules는 어떤 결제 모듈을 사용하는 지 알 필요가 없음
6. 확장성 : 쉽게 확장 가능해짐. CQRS, Event-Sourcing, DDD방식을 사용하여 확장 가능

## 사용 방법

```python
from .entities import Note

class UseCases():
    def __init__(self, storage):
        self.storage = storage
    def create_note(self, title, body):
        note = Note(title, body)
        return self.storage.save_note(note)
```
