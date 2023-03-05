# 코테 대비 총정리

## 기본 문법

### 즉시실행함수

```javascript
const identifier = ((param) => 'execute')(arg)
```

### for문

```javascript
const repeat = for(let i = 0; i < input.length; i++) {
  return 'repeat'
}
```

### swich문

```javascript
switch (condition) {
  case 'case 1':
    return 'execute 1'
    break
  default:
    return 'execute default'
}
```

### 연산자

- AND : `&&`
- OR : `||`
- 일치 : `===`
- 불일치 : `!==`
- 삼항연산자 : `condition ? true : false`

### 배열

- 맨 뒤에 추가 : `target.push()`
- 마지막 요소 삭제 : `target.pop()`
- 맨 앞에 추가 : `target.unshift()`
- 첫번째 요소 삭제 : `target.unshift()`
- 제거, 교체, 추가 : `target.splice(index, del, add1, add2, add3)`
  - 제거할 개수를 0으로 입력하면 추가만 한다
  - 추가할 내용을 입력하지 않으면 제거만 한다
- 이어붙이기 : `target1.concat(target2)`
- 검색 : `target.indexOf(search, index)`
  - 두번째 매개변수는 시작위치다
  - 음수로 지정하면 맨 뒤를 기준으로 순서를 정한다
- 유사 배열 객체에서 배열을 생성 : `Array.from(target)`

### Math

- 0 이상 1 미만 부동 소수점 난수 : `Math.random()`
- 절대값 : `Math.abs.apply(null, target)`
- 소수점 이하 반올림 : `Math.round.apply(null, target)`
- 소수점 이하 올림 : `Math.ceil.apply(null, target)`
- 소수점 이하 내림 : `Math.floor.apply(null, target)`
- 제곱근 : `Math.sqrt.apply(null, target)`
- 최대값 : `Math.max.apply(null, target)`
- 최소값 : `Math.min.apply(null, target)`

### 문자열

- 글자수 : `target.length`
- 철자 인덱스 : `target.charAt(index)`
- 자르기 : `target.slice(begin, end)`
- 대문자로 변환 : `target.toUpperCase()`
- 소문자로 변환 : `target.toLowerCase()`
- 치환 : `target.replace(old, new)`
- 문자열을 배열로 분리 : `target.split(separator, limit)`
- 배열을 하나의 문자열로 결합 : `target.join(separator)`

### 형변환

- 숫자 → 문자 :  `target.toString()`
- 문자 → 숫자 : `Number(target)`
- 문자 → 정수 : `parseInt(target, 10)`
  - 두번째 매개변수는 진수(radix)다
  - 기본값은 2진수이므로 10진수로 바꾸려면 반드시 10을 입력해야 한다

### 타입 검사

```javascript
const getType = (target) => {
  return Object.prototype.toString.call(target).slice(8, -1);
}
```

## 배열 메서드

### 정렬 : sort

```javascript
/* 사용법 */
target.sort(compare) 

/* 숫자열 오름차순  */
const compare = (a, b) => {
  return a - b
}

/* 숫자열 내림차순 */
const compare = (a, b) => {
  return b - a
}

/* 문자열 오름차순 */
const compare = (a, b) => {
  return a.localeCompare(b);
}

/* 문자열 내림차순 */
const compare = (a, b) => {
  return b.localeCompare(a);
}

/* 객체배열 숫자열 오름차순 */
const compare = (a, b) => {
  return a.key - b.key
}

/* 객체배열 문자열 오름차순 */
const compare = (a, b) => {
  return a.key < b.key ? -1 : a.key > b.key ? 1 : 0
}
```

### 단순 반복 : forEach

```javascript
target.forEach((value, index) => execute(value, index))
```

- 첫번째 매개변수는 반복 시점의 값이다
- 두번째 매개변수는 반복 시점의 인덱스이다
- 반환값을 사용할 수 없다 (무조건 undefined로 나옴)

### 순회 후 결과를 반환 : map

```javascript
// const target = [1, 4, 9, 16]
const mapped = target.map(value => value * 2) // Array [2, 8, 18, 32]
```

### 필터링 결과를 반환 : filter

- 범위 필터링

```javascript
// const target = [1, 2, 3, 4, 5]
const filtered = target.filter(number => {
  if (number > 1 && number < 5) {
      return number
  }
}) // [2, 3, 4]
```

- 중복 제거

```javascript
// const target = [1, 1, 2, 2, 3, 3]
const filtered = target.filter((value, index) => target.indexOf(value) === index) // 1, 2, 3
```

- 객체의 값을 필터링

```javascript
// const target = [{num:1, name:'abc'},{num:2, name:'abc'},{num:3, name:'abc'}]
const filtered = target.filter(obj => obj.key === 'value')
```

### 누적해서 반복 : reduce

- 총 합

```javascript
const sum = target.reduce((prev, cur) => prev + cur, 0)
```

- 평균
```javascript
const avg = (target) => {
  const sum = target.reduce((prev, cur) => prev + cur)
  const div = target.length
  return sum / div
}
```
