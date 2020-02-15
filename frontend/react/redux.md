# Redux

## 기본 설명

> 리덕스는 가장 사용률이 높은 상태관리 라이브러리

(리덕스는 리액트에 종속되지 않는다.)

1. 리덕스는 글로벌 상태 관리를 하게 될 때 굉장히 효과적
2. 리덕스를 사용하는것이 유일한 솔루션은 아니다
3. Context API 를 통해서도 동일한 작업을 할 수 있다

예를들어 투두리스트 앱을 만든다고 하자

```sh
          APP
      /         \
createForm    TodoList
                |
              TodoItem (여러개)
```

1. CreateForm 에서 우리가 값을 투두 아이템을 추가
2. App 에서 CreateForm 에게 전달해준 handleCreate 함수가 호출
3. 이 함수가 호출 되면 App 의 state 안에 들어있는 todos 값이 업데이트

위 구조에서 CreateForm 와, TodoList 간의 데이터 교류를 하기 위해서
App 이라는 부모 컴포넌트가 중간자 역할을 해주었습니다.

### 컴포넌트 구조가 복잡해질 때

다음과 같은 컴포넌트 구조라고 하자

![복잡한 컴포넌트](https://i.imgur.com/RFjWPuh.png)

onDoSomething something 값에 변화를 줄 때

1. onDoSomething 은 Root -> B -> H 로 전달되고
2. H 에서 이벤트가 발생하여 이 함수가 호출
3. something 이 Root -> A -> E -> F 로 전달됩니다.

(Root가 중간 다리 역할을 수행)

다음과 같은 단점이 있다.

- 실제로는 해당 props 를 사용하지 않는 컴포넌트를 거쳐가야 한다
  - 리렌더링 하게 될 때 비효율적
- 수정시 상위 컴포넌트에서 props 이름을 바꿔준다면 그 아래에도 바꿔야 한다

### 리덕스를 이용하면

![리덕스를 사용할때](https://i.imgur.com/U3S2iJ8.png)

앱이 지니고 있는 상태와, 상태 변화 로직이 들어있는 스토어를 이용한다.

스토어를 통해 우리가 원하는 컴포넌트에 원하는 상태값과 함수를
직접 주입해줄 수 있다.

## 주요 개념

### 액션 (Action)

상태에 어떠한 변화가 필요하게 될 때 발생하는 객체

액션 객체는 다음과 같은 구조이다

```typescript
{
  type: "TOGGLE_VALUE", // 필수로 가지고 있어야 하는 값
  // 나머지는 개발자 마음대로
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}
```

### 액션 생성함수 (Action Creator)

액션을 만드는 함수입니다. 단순히 파라미터를 받아와서 액션 객체 형태로 만듬.

```typescript
function addTodo(data) {
  return {
    type: "ADD_TODO",
    data
  };
}

// 화살표 함수로도 만들 수 있습니다.
const changeInput = text => ({
  type: "CHANGE_INPUT",
  text
});
```

### 리듀서 (Reducer)

리듀서는 변화를 일으키는 함수입니다.

두가지의 파라미터가 필요하다.

```typescript
function reducer(state, action) {
  // 상태 업데이트를 수행한다

  return alteredState; // 변경된 스테이트를 반환
}
```

### 스토어 (Store)

리덕스에서는 한 애플리케이션 당 하나의 스토어를 만들게 됩니다.

스토어는 다음과 같이 구성된다.

- 현재의 앱 상태
- 리듀서
- 추가적으로 몇가지 내장 함수들

### 디스패치 (dispatch)

디스패치는 스토어의 내장함수 중 하나 (액션을 발생 시키는 것)

액션을 파라미터로 전달한다

```typescript
dispatch(action);
```

디스패치를 호출하면 다음을 수행한다.

1. 스토어는 리듀서 함수를 실행시킨다.
2. 해당 액션을 처리하는 로직이 있다면 액션을 참고하여 새로운 상태를 만들어준다.

### 구독 (subscribe)

내장함수 중 하나이다.

함수 형태의 값을 파라미터로 받아온다.

```typescript
subscribe(something: function);
```

subscribe 함수에 특정 함수를 전달해주면,
액션이 디스패치 되었을 때 마다 전달해준 함수가 호출됩니다.
