# Typescript
## 개발환경 구축
### 기본 구성요소
- 타입스크립트는 개발 단계에서만 사용되기 때문에 devDependencies로 설치한다
  - typescript
  - ts-node

### 프로젝트 생성
1. `tsc --init` 플래그 실행
2. tsconfig.json 작성
```javascript 
{
  "compilerOptions": {
    "module": "commonjs", // 결과물의 모듈 방식
    "target": "es2016", // 결과물의 버전
    "outDir": "dist", // 결과물을 내보낼 위치
    "esModuleInterop":true // CommonJS 모듈을 ES6 방식으로 Import 한다
    "resolveJsonModule":true // JSON 파일을 Import 한다
  },
  "include": ["src/**/*"], // 포함할 대상
}
```

### tsc-watch
- nodemon과 마찬가지로 코드의 변경이 감지되면 자동으로 앱을 재시작 해주는 도구
- npm start 설정: `"tsc-watch --onSuccess \"node dist/index.js\""`

## 사용법
### 타입스크립트의 특징

* 타입을 지정하여 타입 입력 실수로 인한 버그를 방지한다
* 해당 타입에 관련된 메서드를 자동완성으로 보여준다

### 타입

- 자바스크립트와 타입스크립트가 공통으로 지원하는 타입 : Boolean, Null, Undefined, Number, String, Object
  - 자바스크립트만 지원하는 타입 : **BigInt**, **Symbol**
  - 타입스크립트만 지원하는 타입 : **Array, Tuple, Enum, Any, Void, Never**

### 함수
- 리턴이 있는 경우 매개변수 오른쪽에 리턴의 타입을 지정한다
```typescript
function sum1 (a: number, b: number): number {
  return a + b;
}
console.log(sum(1, 2)) // 3
```

- 리턴이 없는 경우 리턴의 타입을 void로 지정한다
```typescript
function sum2 (a: number, b: number): void {
  console.log(a + b) // 3
}
sum(1, 2)
```
