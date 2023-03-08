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

- webpack + css 관련
  - css-loader
  - style-loader

- 타입스크립트 관련
  - @types/react
  - @types/react-dom

### 폴더 구조
```
./
└─src
    App.tsx
    index.tsx
babel.config.js
index.html
webpack.config.js
```

### babel.config.js
```javascript
module.exports = {
  presets: [
    '@babel/preset-env',
    '@babel/preset-react',
  ],
};
```

### webpack.config.js
```javascript
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path')

module.exports = {
  entry: `${path.resolve(__dirname, './src')}/index.tsx`,
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        loader: "babel-loader",
        exclude: /node_modules/,
      },
      {
        test: /\.(ts|tsx)?$/,
        loader: 'ts-loader',
        exclude: /node_modules/,
      },
      {
        test: /\.(css)$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg)$/,
        loader: 'file-loader',
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './index.html', // 번들링 결과물을 주입할 html 파일
    }),
    new webpack.ProvidePlugin({
      React: 'react', // 웹팩에 리액트를 적용
    }),
  ],
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  },
  devServer: { // webpack-dev-server 옵션
    static: path.resolve(__dirname, 'dist'),
    historyApiFallback: true, // 404 페이지 대신 index.html로 이동
    hot: true, // 모듈 전체를 다시 로드하지 않고 변경된 사항만 갱신
  },
  resolve: { // import 할 때 생략할 확장자
    extensions: ['.jsx', '.js','.ts','.tsx'],
  },
}
```

### index.html
```html
<!-- {...} -->
<body>
  <div id="root"></div>
</body>
<!-- {...} -->
```

### ./src/index.tsx
```javascript
import { createRoot } from 'react-dom/client'
import React from 'react'
import App from './App'

const rootNode = document.getElementById('root')
const root = createRoot(rootNode)
root.render (
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```
