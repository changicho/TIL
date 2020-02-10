# npm Module 만들기

## npm 기본 설정

다음과 같은 명령으로 프로젝트의 npm에 대한 기본 설정을 수행할 수 있다.

```sh
npm set init.author.name "이름"
npm set init.author.email "이메일"
npm set init.author.url "페이지주소"
```

npm 정보를 입력한다

```sh
npm adduser
```

npm은 GItHub와 다르게 모든 모듈명이 유일해야 한다.

pageage.json 에 name을 유일하게 설정하자.

## 파일 구조

프로젝트 폴더의 root에서 파일, 디렉토리는 다음과 같다.

- LICENSE
- README.md
- .npmignore
- examples/
- lib/
- node_modules/
- package.json

여기서 LICENSE, README.md, examples, lib는 모두 프로젝트와 관련된 파일들이다.

모듈마다 다른 파일과 구조를 가진다.

## 배포 전 테스트

```sh
mkdir ../install-test
cd ../install-test
npm install ../my-npm-module/
```

## 배포

```sh
npm publish
```
