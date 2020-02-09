# LifeCycle API

React의 컴포너트는 생명주기(Life cycle)을 가진다.

생명주기란 컴포넌트가 생성되고 사용되고 소멸될 때 까지 일련의 과정을 말한다.

이러한 생명주기 안에서는 특정 시점에 자동으로 호출되는 메서드가 있는데,
이를 라이프 사이클 이벤트라고 한다.

![라이프사이클](https://user-images.githubusercontent.com/6733004/45587740-f8ed0e00-b944-11e8-9c99-7baab37944e8.jpg)

LifeCycle API는 다음과 같을 때 실행된다.

- 컴포넌트가 DOM 위에 생성되기 전&후
- 데이터가 변경되어 상태를 업데이트하기 전&후

사용 예시

- 태그에 기본값을 전달해 줄 때
- 자원 낭비를 줄이고자 할 때

**리액트 16.3 이전과 이후에 차이가 있다.**

변경 이유 [(링크)](https://reactjs.org/blog/2018/03/29/react-v-16-3.html#component-lifecycle-changes)

- 초기 렌더링을 제어하는 방법이 많아져서 혼란이 됨.
- 오류 처리 인터럽트 동작시에 메모리 누수 발생할 수 있음.
- React 커뮤니티에서도 가장 혼란을 야기하는 라이프 사이클

---

## 메도스 실행 시점

![라이프사이클](https://velopert.com/wp-content/uploads/2016/03/Screenshot-from-2016-12-10-00-21-26-1.png)

각 과정에서 어떠한 메소드들이 (순서대로) 실행되는지 정리함.

### 컴포넌트를 생성할 때

1. constructor
2. componentWillMount
3. render
4. componentDidMount

### 컴포넌트를 제거할 때

1. componentWillUnmount

### 컴포넌트의 prop이 변경될 때

1. componentWillReceiveProps
2. shouldComponentUpdate
3. componentWillUpdate
4. render
5. componentDidUpdate

### state가 변경될 떄

prop이 변경될 때와 비슷하다.

1. shouldComponentUpdate
2. componentWillUpdate
3. render
4. componentDidUpdate

## 메소스들 알아보기

### constructor

생성자 메소드로서 컴포넌트가 처음 만들어 질 때 실행됩니다.
이 메소드에서 기본 state 를 정할 수 있습니다.

```typescript
constructor(props){
  super(props);
  console.log("constructor");
}
```

### componentWillMount

컴포넌트가 DOM 위에 만들어지기 전에 실행됩니다.

```typescript
componentWillMount(){
  console.log("componentWillMount");
}
```

### render

컴포넌트 렌더링을 담당합니다.

### componentDidMount

```typescript
componentDidMount(){
  console.log("componentDidMount");
}
```

컴포넌트가 만들어지고 첫 렌더링을 다 마친 후 실행되는 메소드입니다.

이 안에서 다른 JavaScript 프레임워크를 연동하거나,
setTimeout, setInterval 및 AJAX 처리 등을 넣습니다.

### componentWillReceiveProps

```typescript
componentWillReceiveProps(nextProps){
  console.log("componentWillReceiveProps: " + JSON.stringify(nextProps));
}
```

컴포넌트가 prop 을 새로 받았을 때 실행됩니다.

prop 에 따라 state 를 업데이트 해야 할 때 사용하면 유용합니다.

이 안에서 this.setState() 로 스테이트를 변경하더라도,
추가적으로 렌더링하지 않습니다.

### shouldComponentUpdate

```typescript
shouldComponentUpdate(nextProps, nextState){
  console.log("shouldComponentUpdate: " + JSON.stringify(nextProps) + " " + JSON.stringify(nextState));
  return true;
}
```

prop 혹은 state 가 변경 되었을 때, 리렌더링을 할지 말지 정하는 메소드입니다.

위 예제에선 무조건 true 를 반환 하도록 하였지만, 실제로 사용 할 떄는 필요한 비교를 하고 값을 반환하도록 하시길 바랍니다.

```typescript
// ex)
return nextProps.id !== this.props.id;
```

JSON.stringify() 를 쓰면 여러 field 를 편하게 비교 할 수 있답니다.

### componentWillUpdate

```typescript
componentWillUpdate(nextProps, nextState){
  console.log("componentWillUpdate: " + JSON.stringify(nextProps) + " " + JSON.stringify(nextState));
}
```

컴포넌트가 업데이트 되기 전에 실행됩니다.

이 메소드 안에서는 this.setState() 를 사용할 경우 무한루프에 빠져들게 됩니다.

### componentDidUpdate

```typescript
componentDidUpdate(prevProps, prevState){
  console.log("componentDidUpdate: " + JSON.stringify(prevProps) + " " + JSON.stringify(prevState));
}
```

컴포넌트가 리렌더링을 마친 후 실행됩니다.

### componentWillUnmount

```typescript
componentWillUnmount(){
  console.log("componentWillUnmount");
}
```

컴포넌트가 DOM 에서 사라진 후 실행되는 메소드입니다.
