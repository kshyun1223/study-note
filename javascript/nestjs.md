# Nest.js - Main

## 개요

### 정의

* Nest는 자바의 스프링, 파이썬의 장고와 마찬가지로 MVC 패턴을 구현할 수 있는 타입스크립트의 풀스택 프레임워크이다
* Model: 어플리케이션이 무엇을 할 것인지 정의하는 부분. DB와 연동하여 사용자가 입력한 데이터나 사용자에게 출력할 데이터를 다룬다.
* View: 사용자에게 시각적으로 보여주는 부분. UI.
* Controller: Model이 데이터를 어떻게 처리할지 알려주는 역할을 한다. 요청이 들어오면 우선 Model을 호출하기전에 적절히 가공을 하고 나서 모델을 호출한다. 그리고 Model이 처리를 완료하면 그 결과를 받아서 다시 View에게 전달한다.

### 기본 구성

* eslintrc.js, prettierrc.js : 코드 포맷팅 관련 라이브러리
* nest-cli.json : Nest 프로젝트 설정 파일
* tsconfig.json, tsconfig.build.json : 컴파일 관련 설정 파일
* src 폴더 : 대부분의 비즈니스 로직이 들어있는 폴더
  * main.ts : 엔트리 파일
  * app.module.ts : 앱 모듈을 정의하는 파일

## module

### 기본 개념

* 기능과 역할을 분리 하면서 컨트롤러와 서비스의 생명주기를 관리하고 필요한 정보를 제공한다
* 처음 프로젝트를 생성하면 루트 모듈만이 존재한다. 이후 하위 모듈을 추가해가며 개발을 한다
* 모듈에는 controller와 provider(서비스)가 필요하다
  * controller : MVC에서의 컨트롤러다
  * service : 비즈니스 로직이 들어있는 부분
  * repository : 네스트 내장은 아니지만 함께 사용하는 경우가 많은 TypeORM에서 지원하는 기능이다. DB 관련 코드를 리포지토리로 따로 분류하면 서비스에 순수한 비즈니스 로직만 남길 수 있다.
* 단일 모듈 : 네스트의 모듈은 기본적으로 단일 모듈 형태이다. 한 모듈에서 다른 모듈을 가져오면 그 모듈의 서비스 공급자를 사용할 수 있다.

### 새로운 모듈을 만드는 순서

1. `nest g module <모듈명> --no-spec` 명령어로 모듈을 만들면 루트 모듈에도 자동으로 호출 된다

```typescript
/* example.module.ts */
@Module({})
export class ExampleModule {}
```

```typescript
/* app.module.ts */
@Module({
  imports: [ExampleModule] // 추가
})
```

1. `nest g controller <모듈명> --no-spec` 명령어로 컨트롤러를 만들면 1에서 만든 모듈에도 자동으로 컨트롤러가 주입된다

```typescript
/* example.controller.ts */
@Controller('example')
export class ExampleController {}
```

```typescript
/* example.module.ts */
@Module({
  controllers: [ExampleController] // 추가
})
```

1. `nest g service <모듈명> --no-spec` 명령어로 서비스를 생성하면 1의 모듈 에도 자동으로 서비스가 주입된다

```typescript
/* example.service.ts */
@Injectable()
export class ExampleService {}
```

```typescript
/* example.module.ts */
@Module({
  controllers: [ExampleController],
  providers: [ExampleService] // 추가
})
```

1. 생성자를 사용하여 컨트롤러에 서비스 프로바이더를 주입한다

```typescript
@Controller('example')
export class ExampleController {
  exampleService : ExampleService // 추가

  constructor(exampleService : ExampleService){ // 추가
    this.exampleService = exampleService // 추가
  }
}
```

1. 루트 모듈에 서비스 프로바이더를 주입한다

```typescript
@Module({
  imports: [ExampleModule],
  providers: [ExampleService] // 추가
})
export class AppModule {}
```

1. 서비스에 비즈니스 로직 작성

```typescript
@Injectable()
export class ExampleService {
  private exampleText = '이것은 예시입니다';

  getExample() {
      return this.exampleText;
  }
}
```

## 파이프
### 개요
- 요청이 라우터 핸들러로 전달되기 전에 요청 객체를 변환할 수 있는 기회를 제공한다

### 미들웨어와의 차이
- 미들웨어는 현재 요청이 어떤 핸들러에서 수행 되는지, 어떤 매개변수를 가지고 있는지에 대한 실행 콘텍스트를 알지 못하기 때문에 애플리케이션의 모든 콘텍스트에서 사용될 수는 없다

### 역할
- 변환(transformation): 입력 데이터를 원하는 형식으로 변환
유효성 검사(validation): 입력 데이터가 사용자가 정한 기준에 유효하지 않은 경우 예외 처리

### @nest/common 패키지의 내장 파이프
* ValidationPipe
* ParseIntPipe
* ParseBoolPipe
* ParseArrayPipe
* ParseUUIDPipe
* DefaultValuePipe
