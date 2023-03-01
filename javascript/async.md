# 비동기 처리

## fetch

- 함수
```javascript
const test = async (number) =>{
  const url = `https://jsonplaceholder.typicode.com/todos/${number}`
  try{      
    const response = await fetch(url)
    const data = await response.text()
    return data
  } catch(error) {
    console.log(error)
  }
}

test('123').then(data => alert(data))
```

- 생성자함수
```javascript
function TestConstructor(){
  this.test = async(number) => {
  const url = `https://jsonplaceholder.typicode.com/todos/${number}`
    try {      
      const response = await fetch(url)
      const data = await response.text()
      return data
    } catch(error) {
      console.log(error)
    }
  }
}
  
const test1 = new TestConstructor()

test1.test('123').then(data => alert(data))
```

- 클래스
```javascript
class TestClass {
  async test(number){
    const url = `https://jsonplaceholder.typicode.com/todos/${number}`
    try {      
      const response = await fetch(url)
      const data = await response.text()
      return data
    } catch(error) {
      console.log(error)
    }
  }
}

const test1 = new TestClass()

test1.test('123').then(data => alert(data))
```

- 정적 메서드
```javascript
class TestClass {
  static async test(number){
    const url = `https://jsonplaceholder.typicode.com/todos/${number}`
    try {      
      const response = await fetch(url)
      const data = await response.text()
      return data
    } catch(error) {
      console.log(error)
    }
  }
}

TestClass.test('123').then(data => alert(data))
```

## fs/promises

```javascript
import fs from 'fs/promises'

const test = async(path, encode) => {
  try {
    const data = await fs.readFile(path, encode)
    const parse = await JSON.parse(data)
    return parse
  } catch (error) {
    console.log(error)
  }
}

test('./db.json', 'utf-8').then(parse => {
  console.log(parse)
})
```

## callback
```javascript
const test = (arg, callback) => {
  const param = `콜백 처리 된 ${arg}`
  callback(param)
}

test("매개변수", (callback) => {
  console.log(callback) // 콜백 처리 된 매개변수
})
```
