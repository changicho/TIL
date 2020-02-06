# 타입스크립트 기본

타입스크립트를 컴파일하면 자바스크립트가 된다.

목표는 데이터의 인/아웃의 형태를 갖추는것!

## 설치

Node.js의 npm 패키지들을 손쉽게 사용할 수 있으며,
타입스크립트 컴파일러 자체가 npm 패키지이기도 하다.

```sh
npm install typescript
```

## 타입스크립트 타입 선언

```typescript
let foo: string = "hello";
```

foo라는 변수는 항상 '문자열'임이 보장된다.

### 타입의 종류

자주 사용하는 타입만 열거한다.

|   타입    | 설명                                             |
| :-------: | :----------------------------------------------- |
|  boolean  | true와 false                                     |
|   null    | 값이 없다는 것을 명시                            |
| undefined | 값을 할당하지 않은 변수의 초기값                 |
|  number   | 숫자(정수와 실수, Infinity, NaN)                 |
|  string   | 문자열                                           |
|  object   | 객체형(참조형)                                   |
|   array   | 배열                                             |
|   enum    | 열거형. 숫자값 집합에 이름을 지정한 것이다.      |
|    any    | 어떤 타입의 값이라도 할당 가능.                  |
|   void    | 일반적으로 함수에서 반환값이 없을 경우 사용한다. |
|   never   | 결코 발생하지 않는 값                            |
| Function  | 함수                                             |

#### 참고 링크

[[typescript] 4. typescript 변수](https://doitnow-man.tistory.com/171)

[TypeScript 핸드북 1 - 기본 타입](https://infoscis.github.io/2017/05/14/TypeScript-handbook-basic-types/)
