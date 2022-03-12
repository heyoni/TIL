# Element Rendering

## Element

- React에서 가장 작은 단위
- 화면에 표시될 내용을 기술한다.

```js
const element = <h1>Hello, world</h1>;
```

- React에서의 Element는 일반 객체이며 쉽게 생성 할 수 있다.

## DOM에 엘리먼트 렌더링하기

`ReactDOM.render()`로 전달한다.

```html
<div id="root"></div>
```

```js
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById("root"));
```

위 코드를 실행하면 화면에 'Hello, world'가 보임.

## 렌더링 된 엘리먼트 업데이트 하기

- React 엘리먼트는 **불변객체**로, 엘리먼트 생성 이후에는 자식이나 속성을 변경할 수 없다.
- 업데이트를 하기 위해서는 다시 렌더링해야 함.
- 단, React에서는 변경된 부분만 업데이트 한다
  - React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트함.
