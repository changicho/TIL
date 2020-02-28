# ContextAPI (Typescript)

> 전역적으로 데이터를 관리하는 용도로 사용

Context 는 Provider 와 Consumer로 나뉜다.

각각의 Context를 생성하고, 모든 Context의 Provider를 합친 ContextProvider가 존재한다고 하자.

최 상단 컴포넌트에 ContextProvider로 감사고, 사용할 곳에서 Consumer 컴포넌트를 이용해 사용.

## Context

선언은 다음과 같이 한다.

```tsx
interface Props {}

interface State {
  // 사용할 state 정의
}

type Context = {
  state: Readonly<State>;
  actions: {
    // 사용할 action들 정의
  };
};

// 초기값 설정 문제로 undefined를 사용하지만, 직접 초기값을 넣어주어도 된다.
const Context = createContext<Partial<Context> | undefined>(undefined);
```

생성한 Context에서 Provider와 Consumer를 추출할 수 있다.

```tsx
const { Provider, Consumer: SampleConsumer } = Context;
```

Context를 사용하기 위한 wrapper 컴포넌트를 만든다

```tsx
class SampleProvider extends React.Component<Props, State> {
  constructor(props: Props) {
    super(props);

    this.state = {
      // 원하는 초기 값  입력
    };
  }

  actions = {
    // 원하는 action을 지정.
    // state의 변경은 setState로
  };

  render() {
    const { state, actions } = this;

    const value = { state, actions };
    return <Provider value={value}>{this.props.children}</Provider>;
  }
}
```

Consumer에서는 Provider 컴포넌트의 value를 사용한다.

Provider와 Consumer를 export한다

```tsx
export { SampleProvider, SampleConsumer };
```

## 사용

```tsx
(
  <SampleConsumer>
    {
      ({state, actions}) => {
        // typescript의 경우 undefined처리를 해주어야 한다.
        if(!state || !actions){
          return null;
        }

        return (
          // 컴포넌트
          // state와 actions로 Context에 직접 접근 가능
        )
      }
    }
  </SampleConsumer>
)
```
