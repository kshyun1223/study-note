# Webpack

## 개요
### 웹팩이란? 
- 웹팩은 자바스크립트의 대표적인 번들러이다

### 번들러란? 
- 웹브라우저는 Node.js와 달리 자바스크립트의 모듈 구조에 접근할 수 없다. 원활한 개발 작업을 위해서는 모듈화가 필수적이지만 최종적인 배포 단계에서는 모든 모듈들을 하나의 자바스크립트 파일로 만들어야 한다. 
- 또한 의존 관계가 없는 독립적인 파일들의 경우에도 일일이 불러오는 것 보다는 하나로 묶는 것이 효율적이다.
- 이러한 작업을 자동적으로 처리해주는 도구가 바로 번들러이다.

### 적용 예시
- 번들러를 사용하지 않는 경우 모든 자바스크립트 파일들을 일일이 불러와야 한다
```html
<head>
  <script src="./number1.js"></script>
  <script src="./number2.js"></script>
  <script src="./number3.js"></script>
  <script src="./number4.js"></script>
  <script src="./number5.js"></script>
</head>
```

- 번들러를 사용하면 하나의 자바스크립트 파일만 불러오면 된다
```html
<head>
  <script src="./number.js"></script>
</head>
```

## 개발환경 구축
### 구성 요소
- 자바스크립트 기본
  - webpack
  - webpack-cli
  - webpack-dev-server
  - html-webpack-plugin 
  - @babel/core
  - @babel/preset-env
  - babel-loader
  
- 타입스크립트를 사용하는 경우 추가로 필요한 것
  - typescript
  - ts-loader
  
### npm scripts 설정
- "start": "webpack serve --open"
- "build": "webpack"

### webpack.config.js 작성
```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.ts", // 번들링 시작 위치
  output: {
    path: path.join(__dirname, "/dist"), // 번들 결과물 위치
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /[\.js]$/, // 자바스크립트 파일에는 babel-loader를 사용
        exclude: /node_module/,
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.ts$/, // 타입스크립트 파일에는 ts-loader를 사용
        exclude: /node_module/,
        use: {
          loader: "ts-loader",
        },
      },
    ],
  },
  resolve: {
    modules: [path.join(__dirname, "src"), "node_modules"], // 모듈 위치
    extensions: [".ts", ".js"],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html", // html 템플릿 위치
    }),
  ],
  devServer: { // webpack-dev-server 설정
    host: "localhost",
    port: 5500,
  },
  mode: "development", // 번들링 모드 설정
};
```
