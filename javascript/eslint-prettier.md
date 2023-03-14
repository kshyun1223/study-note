# eslint & pritter
## 개발환경 구축
### VScode Extensions
- ESlint
- Prettier

### devDependencies
- eslint 
- prettier

- eslint에서 prettier를 지원하기 위한 플러그인
  - eslint-config-prettier 
  - eslint-plugin-prettier
 
- eslint preset
  - eslint-config-airbnb-base (리액트 관련 설정 미포함)
  - eslint-config-airbnb (리액트 관련 설정 포함)

- eslint에서 react를 지원하기 위한 플러그인
  - eslint-plugin-react
  - eslint-plugin-react-hooks
  - eslint-plugin-jsx-a11y
  - eslint-plugin-import

### `.prettierrc`
```javascript
{
  "singleQuote": true,
  "parser": "typescript",
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "printWidth": 120,
  "arrowParens": "always"
}
```

### `.eslintrc.js`
```javascript
module.exports = {
  parser: '@typescript-eslint/parser',
  plugins: [
    '@typescript-eslint',
    'react-hooks'
  ],
  extends: [
    'airbnb',
    'plugin:react/recommended',
    'plugin:jsx-a11y/recommended',
    'plugin:import/errors',
    'plugin:import/warnings',
    'plugin:@typescript-eslint/recommended',
    'plugin:prettier/recommended',
  ],
  rules: {
    'prettier/prettier': 0,
    "import/extensions": [
      "error", 
      "ignorePackages", 
      { 
        "js": "never", 
        "jsx": "never", 
        "ts": "never", 
        "tsx": "never" 
      }
    ],
    'react/jsx-filename-extension': [2, { 'extensions': ['.js', '.jsx', '.ts', '.tsx'] }],
  },
  settings: {
    'import/resolver': {
      node: {
        extensions: ['.js', '.jsx', '.ts','.tsx',],
      },
    },
  },
};
```

### eslint에서 webpack.config.js 예외 처리
- `vscode extension > eslint > settings.json`에서 아래 설정 추가
```javascript
"eslint.options": {
    "ignorePattern": "webpack.config.js",
}
```