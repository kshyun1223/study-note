# React native
## 개발환경 구축
### 1. Android Studio 및 JDK 설치
- Android Studio 환경변수 설정
  1. 안드로이드 스튜디오를 설치한 뒤 File -> Settings 메뉴로 들어간다
  2. Android SDK Location이라는 값을 복사한다 
  3. 윈도우의 시스템 환경변수 편집에서 시스템변수에 Android-SDK라는 변수를 새로 만들고
  4. 2에서 복사했던 경로를 값으로 설정한다
  5. 시스템변수의 Path 항목에 `%Android-SDK%\tools`와 `%Android-SDK%\platform-tools`라는 값을 추가한다
  6. 터미널에서 `adb`라는 명령어를 실행해서 응답이 있으면 정상적으로 설정된 것이다

‐ JDK 환경변수 설정
  1. 시스템 환경변수 편집 -> 시스템 변수에 `JAVA_HOME`이라는 변수를 새로 만들고 값으로 자신의 JDK 폴더 경로를 입력한다 (Oracle/Java 폴더 하위에 있다)
  2. 시스템 변수에 CLASSPATH라는 변수를 새로 만들고 `%JAVA_HOME%\lib`라는 값을 입력한다
  3. 시스템변수의 Path 항목에 `%JAVA_HOME%\bin`이라는 값을 추가한다
  4. 터미널에서 `javac`라는 명령어를 실행해서 응답이 있으면 정상적으로 설정된 것이다

### 2. 프로젝트 생성
- `npx react-native init ${프로젝트 이름} --template  react-native-template-typescript@latest `
  - 타입스크립트를 사용하려면 `--template react-native-template-typescript`를 붙인다
  - 특정 버전을 지정하려면 `@` 뒤에 붙인다

### 3. 안드로이드 스튜디오에서 디바이스 실행
- 안드로이드 스튜디오를 실행하고 미리 생성한 리액트 네이티브 프로젝트 폴더를 연다
- 가상 디바이스를 생성하거나 물리 디바이스를 연결해서 실행한다
- 이 절차를 거치지 않으면 vscode에서 리액트 네이티브가 실행되지 않는다

### 4. vscode에서 프로젝트 실행 및 개발 시작
- `npm run android` -> 안드로이드 에뮬레이터 시작
- `npm run ios` -> ios 에뮬레이터 시작
- `npm start` -> Metro 시작
  - Metro는 리액트 네이티브를 위한 자바스크립트 번들러이다
  - 보통 자동으로 실행되지만 간혹 실행되지 않아서 따로 실행해야 하는 경우가 있다

## 문제 해결
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

- 라이브러리가 불완전하게 설치되었으므로 다시 설치

### Task :app:installDebug FAILED

- 기기에서 앱을 삭제

### tried to register two views with the same name rncsafeareaview

- 콘솔창에 npm dedupe 입력

## 사용방법

### 작동원리

- JavaScriptCore라는 자바스크립트 엔진이 탑재되어 있으며, 이 엔진을 통해 자바스크립트 코드를 네이티브 앱 내부에서 실행한다

### 마크업

- 리액트 네이티브는 마크업 언어로 HTML이 아닌 XML을 사용한다
  - View : 가장 기본적인 컴포넌트. 레이아웃 및 스타일을 넣는 용도
  - Text : 텍스트를 넣는 용도
  
- 모든 컴포넌트는 사용하려면 일일이 호출해야 한다
  
### StyleSheet

- html이 아니라 xml로 마크업을 하기 때문에, 마찬가지로 css가 아닌 고유의 스타일시트가 존재한다

- 사용법
  - react-native 모듈에서 StyleSheet 컴포넌트를 호출
  - StyleSheet.create 함수를 선언하고 그 안에 작성

- CSS와의 주요 차이점
  - 셀렉터라는 개념이 존재하지 않음
  - 모든 스타일 속성은 camelCase로 작성해야 한다
  - display 속성은 기본적으로 flex이며, 다른 값은 none 밖에 없음
  - flexDirection 속성의 기본값이 column이다
  - 숫자 단위는 dp뿐이다
  - background, border와 같은 단축속성이 없으므로 따로따로 설정해야 한다


## 내비게이션 

### 네이티브 스택 내비게이터

- 메인 화면의 버튼으로 화면을 전환하는 내비게이션
- 설치: @react-navigation/native-stack
- react-navigation이 의존하는 라이브러리: 네이티브 스택 뿐만 아니라 다른 것들도 공통임
  - react-native-screens
  - react-native-safe-area-context

### 그 외 내비게이터 종류

- 드로어 내비게이터: @react-navigation/drawer
  - 드로어 내비게이션이 의존하는 라이브러리: react-native-gesture-handler, react-native-reanimated
- 하단 탭 내비게이터: @react-navigation/bottom-tabs
  - 탭 아이콘 라이브러리: react-native-vector-icons
  - 아이콘 목록: https://fonts.google.com/icons?authuser=0
- 상단 탭 내비게이터

### 내비게이션 Hooks

- useNavigation: Screen으로 사용되고 있지 않은 컴포넌트에서도 navigation 객체를 사용할 수 있게 하는 함수
- useRoute: Screen으로 사용되고 있지 않은 컴포넌트에서도 route 객체를 사용할 수 있게 하는 함수
- useFocusEffect: useFocusEffect는 화면에 포커스가 잡혔을 때 특정 작업을 할 수 있게 하는 함수
  - 예를 들어 HomeScreen에서 DetailScreen을 띄운다면 HomeScreen이 화면에서 사라지는 게 아니라, HomeScreen 위에 DetailScreen을 쌓아서 보여주는 것이다
