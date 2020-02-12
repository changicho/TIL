# 리액트 디자인 패턴

리액트는 데이터와 이벤트의 흐름 (데이터는 하향식, 이벤트는 상향식)이 단방향이기
때문에 구조를 바로 설계하기 쉽지 않다.

## 컴포넌트 역할 정의하기

1. 컴포넌트 틀 잡기. (props없이 태그로만)
2. 필요한 props와 이벤트 & 콜백 찾기
3. 초기값을 정하기, 연결된 이벤트에 연관된 다른 컴포넌트 찾기
4. 컨테이너 (wrapper) 정의하고 무엇을 가지고 있을지 정하기

## 설계한 컴포넌트 스냅샷 만들기

앞의 4단계를 수행하면 최상의 wrapper에서 가지고 있어야 하는
prop과 state, 그리고 handler가 파악될 것이다.

이를 각각 정의하기 보다는 한 곳에 요약한다면 다음과 같은 장점이 있다.

- 상대방이 구조를 파악하기 용이하다
- 수정과 개선이 필요한 곳을 파악하기 쉽다

데이터와 이벤트의 흐름은 다음과 같이 표시할 수 있다.

상위컴포넌트 > (데이터) > 하위컴포넌트 > (데이터) > 데이터사용컴포넌트

상위컴포넌트 < (이벤트) < 하위컴포넌트 < (이벤트) < 데이터사용컴포넌트

하나의 스테이트, 프롭, 핸들러의 경우 이렇게 표현하면 파악하기 쉽다.

전체적으로 나타내기 좋은 방법은 스켈레톤 코드를 작성하는 것이다.

```jsx
class FilterableProductTable extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      filterText: "",
      inStockOnly: false
    };

    // 부모 컴포넌트인 FilterableProductTable에도 마찬가지로 두 가지 이벤트를 바인드 해주었는데
    // 이번에는 자식 컴포넌트로부터 받은 props들을 통해 state를 업데이트하는 이벤트인 점이 아까와 다르다.
    this.handleFilterTextInput = this.handleFilterTextInput.bind(this);
    this.handleInStockInput = this.handleInStockInput.bind(this);
  }

  // 이제 자식 컴포넌트의 props가 부모 컴포넌트의 state가 되며 SearchBar는 물론 ProductTable에도 유저의
  // 인풋이 전달되며, 개발자가 의도한 대로 작동하는 ProductTable과 SearchBar를 볼 수 있을 것이다.
  handleFilterTextInput(filterText) {
    this.setState({
      filterText: filterText
    });
  }

  handleInStockInput(inStockOnly) {
    this.setState({
      inStockOnly: inStockOnly
    });
  }

  render() {
    return (
      <div>
        <SearchBar
          filterText={this.state.filterText}
          inStockOnly={this.state.inStockOnly}
          onFilterTextInput={this.handleFilterTextInput}
          onInStockInput={this.handleInStockInput}
        />
        <ProductTable
          products={this.props.products}
          filterText={this.state.filterText}
          inStockOnly={this.state.inStockOnly}
        />
      </div>
    );
  }
}
```

이런 구조의 depth를 넓혀가면 전체 구조를 한눈에 파악할 수 있다.

## 컴포넌트 분리하기

화면기준으로 컴포넌트를 구성할 경우 문제

- 컨테이너가 이벤트를 담당할 경우 끌어올려야한다
- 콜백을 넘기고, 넘기고, 넘긴다

해결법

- 라우터를 이용
- 리덕스를 이용

리덕스를 이용할 때의 방법

리덕스 스토어에서 루트컴포넌트와, 이벤트 핸들링 컴포넌트에 state를 부여하고,
이벤트 처리를 위해 dispatch를 수행한다.

혹은 콜백함수 대신 dispatch를 넘긴다.

dispatch를 넘길 경우 리덕스에 의존성이 생기는 문제가 발생한다.
(재사용할 일이 없는경우에는 문제가 없다)

## 재사용 가능한 컴포넌트

프로젝트 내에서 '뷰'를 재사용하고싶다면

- 컴포넌트에서 데이터 로드 역할을 제거한다.

프로젝트 내에서 컨테이너(wrapper)를 재사용하고싶다면

- 기능을 효율적으로 묶고, 아키텍처를 사용해라

다른 프로젝트에서도 사용할 수 있게 하고싶다면

- 데이터 로드 & 아키텍처 의존도를 낮춘다
- 필요하다면 props로 주입받는다.
