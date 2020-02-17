# 컴포넌트 설계

> 설계 문서를 개발자가 봤을 때 한눈에 파악하기 위함

리액트 컴포넌트를 설계할 때 중요한 것들은 다음과 같다.

1. Data : props, state, handler
2. function : method, render
3. lifeCycleAPI

따라서 컴포넌트를 설계하거나, 문서화 할 때 다음의 순서에 맞추어 제작한다.

## 예시

RootComponent
Data :

- props
  - callback
  - size
- state
  - index
  - lists
- function
  - handleIndex

Function :

- method

  - changeModal

- render
  - 포함되는 컴포넌트들
  - Header
  - Footer

LifeCycleAPI :

- willUpdate:
  - doSomething

## 다이어 그램

데이터의 흐름을 표현하기 위해 다이어그램을 사용할 수도 있다.

![예시](https://image.slidesharecdn.com/reactjs-1-170310072122/95/react-js-1-21-638.jpg?cb=1489130630)
