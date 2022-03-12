# JSX

Javascript를 확장하여 React를 구현 가능하도록 하는 문법
- JSX는 Element를 생성한다.
- 렌더링 로직이 UI와 연결된다.(?)

React는
- 기술을 분리한다 👉ㅤ별도의 파일에 마크업과 로직을 분리
- 관심사를 분리한다 👉ㅤ "컴포넌트"로 마크업과 로직을 느슨하게 연결함(Unit)

JSX는 객체를 표현한다.
```js
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```
위 예시를 아래와 같이 객체로 만들 수 있다.
```js
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```
이러한 객체를 “React 엘리먼트”라고 하며, 화면에서 보고 싶은 것을 나타내는 표현이다.  
React는 이 객체를 읽어서, DOM을 구성하고 최신 상태로 유지한다.