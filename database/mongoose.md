# Mongoose

### 1. 연결하기

```javascript
mongoose.set("strictQuery", false)
mongoose.connect("mongodb://127.0.0.1:27017/task-manager")
.then(() => {
  console.log("Connected to MongoDB")
})
.catch((err) => {
  console.log(err)
})
```

### 2. 스키마 정의

스키마는 컬렉션에 들어가는 문서 내부의 각 필드가 어떤 형식으로 되어 있는지 정의하는 객체이다. 모델을 만드려면 사전에 스키마를 만들어 주어야 한다.

```javascript
const UserSchema = new mongoose.Schema({
  name: String,
  age: Number,
  saveDate: {
    type: Date,
    default: Date.now,
  },
});
```


### 3. 모델 생성

모델은 스키마를 사용하여 만드는 인스턴스로, 데이터베이스에서 실제 작업을 처리할 수 있는 함수들을 지니고 있는 객체이다

```javascript
const User = mongoose.model("User", UserSchema)
```


### 4. 필드 추가


```javascript
const me = new User({
  name: "Mike",
  age: 27,
})

me.save()
  .then(() => {
    console.log(me);
  })
  .catch((err) => {
    console.log("Error : " + err);
  })
```


### 5. 도큐먼트 조회

```javascript
const users = await User.find()
console.log(users)
```
