# 컴포넌트 (class vs function)

리엑트의 컴포넌트는 클래스형, 함수형 두 가지 방법으로 생성할 수 있다.

그중 클래스형을 사용할 때의 특징은 다음과 같다

1. state를 사용한다.
2. LifeCycle API에 민감하게 다룰 수 있다.
3. this바인딩을 이용하는데, 이 this가 바뀔 수 있다 (mutable)

그렇다면 함수형 컴포넌트는 어떤 상황에 사용하는것이 좋을까?

1. state 나 라이프사이클 API 를 전혀 사용하지 않을 때
2. 해당 컴포넌트는 자체 기능은 따로 없고 props의 내용을 보여줄 때

다음과 같은 구조도 고려해 볼 수 있다 (feat. velopert)

1. Redux 를 사용하여 컴포넌트들을 구성
2. Container 컴포넌트 (혹은 Smart, 컴포넌트) 는 클래스형 컴포넌트를 사용
3. Presentational 컴포넌트 (혹은, Dumb 컴포넌트) 는 함수형 컴포넌트를 사용
