# Components & Props

## Component

컴포넌트는 React App을 이루는 최소 단위이자 독립적인 기능을 수행하는 단위 모듈.(엘리먼트 : React에서 가장 작은 단위이며 화면에 표시될 내용을 기술한다.)

컴포넌트를 class 또는 함수로 정의할 수 있는데 JavaScript class, 함수와 유사하며 “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다.

그리고 React 컴포넌트 class를 정의할 때는 `React.Component`를 상속받아야 하며 `render()`라는 메서드를 반드시 정의해야 함.

```jsx
// 함수 컴포넌트
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// 클래스 컴포넌트
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## 컴포넌트 렌더링

React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있다.  
React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달하는데, 이 객체를 'props'라고 한다.

컴포넌트의 이름은 항상 대문자이다.

```jsx
const element = <Welcome name="react" />;
```

## props는 읽기 전용(순수함수)

컴포넌트에서 받아온 props는 수정되어선 안된다.

```jsx
function withdraw(account, amount) {
  account.total -= amount;
}
```

위와 같은 코드는 수정하는 코드, 지양해야 할 코드이다.

props를 변경해버릴 경우, 하나의 자식만이 존재한다면 상관이 없지만 여러개의 자식이 있을 경우 예기치 못한 동작이 발생할 수 있음. 그것을 방지하기 위해 순수 함수로 제한함.
