# React
## 개발환경 구축
### dependencies
- react
- react-dom

### devDependencies
- babel 관련
 - @babel/cli
 - @babel/core
 - @babel/preset-env
 - @babel/preset-react
 - babel-loader

- webpack 관련 
 - webpack
 - webpack-cli
 - webpack-dev-server
 - html-webpack-plugin

- 타입스크립트 관련 
 - @types/react
 - @types/react-dom




## Props

### Props 객체 구조 분해 할당

```javascript
const object = {
a: 1,
b: 2,
c: 3
};
const {a, b, c} = object;
```

### useState Hook으로 상태 관리하기

* Hooks
  * 리액트에는 use로 시작하는 빌트인 함수가 많은데 이 함수들을 Hook이라고 부른다
  * 상태관리 뿐만아니라 다양한 기능이 있다
* 사용자와의 상호작용으로 UI를 변화시키려면 상태를 기준으로 해야 한다
  * 상태를 관리하는 방법은 useState 함수를 사용하는 것이다
  * useState는 불리언을 비롯하여 숫자, 객체, 배열 등 형태로 상태를 정의할 수 있다
* 상태관리 예시
  * Button 컴포넌트를 불러와서 on off 기능을 구현
  * 조건부 렌더링 기능: 특정 조건에 따라 다른 결과물을 보여주는 것
  * 변수와 증감연산자를 사용해서 카운터 구현하기
