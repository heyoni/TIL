# 조건부 렌더링

- 원하는 동작을 컴포넌트로 만들어 상태에 따라 컴포넌트 중 몇개만을 렌더링 할 수 있음.

- 컴포넌트 상태값은 자바스크립트 문법을 따라 중괄호{}로 묶어줘야 함

- &&으로 if문을 inline으로 표현 가능

- 다른 컴포넌트에 의해 렌더링 될 때 특정 컴포넌트를 숨기고 싶으면 null을 반환하여 숨길 수 있다.

```jsx
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }
  return <div className="warning">Warning!</div>;
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = { showWarning: true };
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState((state) => ({
      showWarning: !state.showWarning,
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? "Hide" : "Show"}
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Page />, document.getElementById("root"));
```

- 리액트 구조상 자동 실행되는 문법들이 문제없이 실행되고 return 시 null값이 아닌 DOM만 표현해준다.
