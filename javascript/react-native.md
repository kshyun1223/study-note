# React native
## 개발환경 구축
### 1. Android Studio 및 JDK 설치
- Android Studio 환경변수 설정
* ANDROID\_HOME
  * C:\Users\\<사용자 이름>\AppData\Local\Android\Sdk

‐JDK 환경변수 설정
* CLASSPATH
  * %JAVA\_HOME%\lib
* JAVA\_HOME
  * C:\Program Files\Java\jdk-\<jdk 버전>
* Path
  * %JAVA\_HOME%\bin

### 2. 프로젝트 생성

* 자바스크립트: `npx react-native init 프로젝트 이름`
  * \=> 처리가 정상적으로 완료되면 VSCODE 종료

### 3. 안드로이드 스튜디오에서 가상 디바이스 

* 안드로이드 스튜디오 실행하고 앞서 생성된 프로젝트 폴더 열기
* Device Manager -> Create device -> 디바이스 선택 -> 시스템 이미지 선택 -> Finish
  * 이 부분은 단순 시험 구동을 위해서는 아무거나 선택해도 되는듯
  * 나중에 실제 개발에서는 디바이스 종류도 감안해야 할 것으로 예상

### 5. 안드로이드 스튜디오에서 생성된 디바이스 실행

* 디바이스 목록의 재생버튼 같이 생긴 삼각형 아이콘 클릭
* 이 부분은 최초 한번만 필요한 것으로 추정. 재실행시 생략해도 문제 없는 것 확인.

### 6. VSCODE로 프로젝트 폴더 열기

* 콘솔에서 { npm run android } 명령어 입력

### 참고사항

* npm run android -> 안드로이드 에뮬레이터 시작
* npm run ios -> ios 에뮬레이터 시작
* npm start -> Metro 시작
  * Metro는 리액트 네이티브를 위한 자바스크립트 번들러
  * 프로젝트에 사용된 자바스크립트 파일들을 모두 읽어서 올바른 순서의 하나의 파일로 합쳐주고 네이티브 앱에서 실행할 준비를 하는 역할
  * 에뮬레이터를 구동하면 자동으로 실행되기 때문에 직접 실행하는 일은 드물다

### 최초 생성된 컴퓨터가 아닌 다른 컴퓨터에서 원격 저장소(깃허브)의 프로젝트 실행하는 방법

* VSCODE로 원하는 경로의 상위 폴더 열기
* 콘솔에서 `git clone 리포지토리 주소` 입력
* 콘솔에서 `npm run android` 입력

### 플러그인이 제대로 등록되지 않은 경우

1. babel.config.js 파일에 플러그인 등록

   ```javascript
   "module.exports" = {
     "presets": [
       "..."
     ],
     "plugins": [
       "...",
       "react-native-reanimated/plugin",
     ],
   };
   ```

2. 터미널에 npm start -- --reset-cache 입력

### RNSScreen was not found in the UIManager

* 라이브러리가 불완전하게 설치되었으므로 다시 설치

### Task :app:installDebug FAILED

* 안드로이드 스튜디오에서 에뮬레이터(가상 스마트폰)를 포맷
  * \-> 더보기(점 세개) 클릭하고 Wipe Data

### tried to register two views with the same name rncsafeareaview

* 콘솔창에 npm dedupe 입력


### 작동원리

* JavaScriptCore라는 자바스크립트 엔진이 탑재되어 있으며, 이 엔진을 통해 자바스크립트 코드를 앱 내에서 실행
* 페이스북이 개발한 JSX라는 문법으로 .js 파일에 코드를 작성. 리액트 네이티브로 만들어서 빌드한 앱에는 스레드가 내장되어 있음. 여기서 코드를 인식해 어떤 네이티브 컴포넌트가 필요한지 연산한 다음 화면에 출력

### 마크업

* 리액트 네이티브는 마크업 언어로 HTML이 아닌 XML을 사용한다
  * View : 가장 기본적인 컴포넌트. 레이아웃 및 스타일을 넣는 용도
  * Text : 텍스트를 넣는 용도
  
  
* 사용자 정의 컴포넌트 : 컴포넌트를 조합해서 하나의 컴포넌트를 만들 수 있음

### 사용자 정의 컴포넌트

1. ‘컴포넌트 이름.js’ 파일을 생성한다
2. import React from ‘react’ : 리액트를 호출하는 코드. 컴포넌트에는 반드시 이 코드가 포함되어야 함
3. import {컴포넌트 1, 컴포넌트 2 …} from ‘react-native’ : 사용할 컴포넌트들을 호출
4. 함수를 선언해서 JSX 코드를 반환
5. export default 컴포넌트 이름’ : 컴포넌트를 내보내는 코드

### Props

* properties의 줄임말로 컴포넌트의 속성을 의미
* JSX 내부에서 렌더링

1. 컴포넌트 함수의 매개변수로 props를 입력
2. 원하는 위치에 {props.이름}을 입력

* 컴포넌트를 사용할 때 값 지정

1. html 태그에 속성을 넣는 것처럼 속성=”값”의 형태로 입력

### defaultProps

* 컴포넌트에 Props를 지정하지 않았을 때 사용할 기본값을 설정하려면 defaultProps를 사용

### JSX

* HTML과 달리 스스로 닫는(Self-Closing) 태그를 반드시 사용해야 한다
* 컴포넌트 함수에서 JSX를 반환할 때는 반드시 최상위에 하나의 태그만 있어야 한다 (최상위에 있는 태그는 형제태그를 가질 수 없다)
* JSX Fragment: DOM에 별도의 노드를 추가하지 않고 빈 꺽쇠를 입력해서 여러 자식태그를 그룹화할 수 있다
* JSX 중간에 중괄호로 자바스크립트 표현식을 넣을 수 있다

### StyleSheet

* CSS와의 주요 차이점
  * 셀렉터라는 개념이 존재하지 않음
  * 모든 스타일 속성은 camelCase로 작성해야 한다
  * display 속성은 기본적으로 flex이며, 다른 값은 none 밖에 없음
  * flexDirection 속성의 기본값이 column이다
  * 숫자 단위는 dp뿐이다
  * background, border 단축속성이 없으므로 따로따로 설정해야 한다
* 사용법
  * react-native 모듈에서 StyleSheet 컴포넌트를 호출
  * StyleSheet.create 함수를 선언하고 그 안에 작성

## 내비게이션 

### 네이티브 스택 내비게이터

* 메인 화면의 버튼으로 화면을 전환하는 내비게이션
* 설치: @react-navigation/native-stack
* react-navigation이 의존하는 라이브러리: 네이티브 스택 뿐만 아니라 다른 것들도 공통임
  * react-native-screens
  * react-native-safe-area-context

### 그 외 내비게이터 종류

* 드로어 내비게이터: @react-navigation/drawer
  * 드로어 내비게이션이 의존하는 라이브러리: react-native-gesture-handler, react-native-reanimated
* 하단 탭 내비게이터: @react-navigation/bottom-tabs
  * 탭 아이콘 라이브러리: react-native-vector-icons
  * 아이콘 목록: https://fonts.google.com/icons?authuser=0
* 상단 탭 내비게이터

### 내비게이션 Hooks

* useNavigation: Screen으로 사용되고 있지 않은 컴포넌트에서도 navigation 객체를 사용할 수 있게 하는 함수
* useRoute: Screen으로 사용되고 있지 않은 컴포넌트에서도 route 객체를 사용할 수 있게 하는 함수
* useFocusEffect: useFocusEffect는 화면에 포커스가 잡혔을 때 특정 작업을 할 수 있게 하는 함수
  * 예를 들어 HomeScreen에서 DetailScreen을 띄운다면 HomeScreen이 화면에서 사라지는 게 아니라, HomeScreen 위에 DetailScreen을 쌓아서 보여주는 것이다
