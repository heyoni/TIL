# JSX

Javascript를 확장하여 React를 구현 가능하도록 하는 문법

- JSX는 Element를 생성한다.
- 렌더링 로직이 UI와 연결된다. 👉ㅤ아래 예제를 보면 이해하기 쉽다.  
  바닐라 자바스크립트에서는 요소 생성, 이벤트 연결 등 단계별로 명령문을 작성해야 하지만, jsx에서는 모든 과정을 한 줄로 작성할 수 있다.

```jsx
// 1. 바닐라 자바스크립트. 요소를 생성하고 이벤트를 연결하기 위해 여러 단계의 명령문을 작성해야합니다.
const button = document.createElement("button");
button.innerText = "click me";
function handleClick() {
  console.log("clicked");
}
button.addEventListener("click", handleClick);

// 2. 리엑트. 간결해보이지만 여전히 자바스크립트 문법입니다.
const btn = React.createElement(
  "button",
  { onClick: () => console.log("clicked") },
  "click me"
);

// 3. JSX. 만들어야하는 요소의 모습을 코드안에서 명확하게 확인할 수 있습니다.
const Button = () => (
  <button onClick={() => console.log("clicked")}>click me</button>
);
```

## React는

- 기술을 분리한다 👉ㅤ별도의 파일에 마크업과 로직을 분리
- 관심사를 분리한다 👉ㅤ "컴포넌트"로 마크업과 로직을 느슨하게 연결함(Unit)
- 표현해보기

  ```jsx
  const name = "REACT";
  const element = <h1>Hello, {name}</h1>;

  ReactDOM.render(element, document.getElementById("root"));
  ```

  jsx는 표현식이다.

## JSX는 객체를 반환한다.

리액트는 어떻게 JSX를 JS로 변환? 👉ㅤBabel이라는 라이브러리를 통해서 변환해줌.

```jsx
const element = <h1 className="greeting">Hello, world!</h1>;
```

위 예시를 아래와 같이 객체로 만들 수 있다.

```jsx
const element = {
  type: "h1",
  props: {
    className: "greeting",
    children: "Hello, world!",
  },
};
```

이러한 객체를 “React 엘리먼트”라고 하며, 화면에서 보고 싶은 것을 나타내는 표현이다.  
React는 이 객체를 읽어서, DOM을 구성하고 최신 상태로 유지한다.
