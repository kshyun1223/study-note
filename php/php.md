# PHP 공부

## 개발환경 구축

### 아파치 웹서버 설치

1. 아파치 웹서버를 다운받고 폴더를 C드라이브에 이동 후 Apache24로 이름 변경
2. `C:\Apache24\bin` 경로에서 터미널을 열고 `httpd.exe -k install` 실행
3. `ApacheMonitor.exe`를 실행한 뒤 서버 가동
4. 로컬호스트 접속 시 It works! 라는 문구가 나오면 정상 설치 완료

### PHP 설치

1. Thread Safe 버전으로 다운 받음
2. 폴더를 아파치와 같은 폴더로 이동 후 php8(혹은 해당 버전명)로 이름 변경
3. `php.ini-development` 파일의 이름을 `php.ini`로 변경
4. `php.ini` 설정
    - `extension_dir`
        - ⇒ `extension_dir = "C:\php8\ext"` 혹은 적절한 경로로 변경
    - 다음 설정들을 활성화
        - `extension=curl`
        - `extension=mysqli`
        - `extension=gettext`
        - `extension=mbstring`
        - `extension=openssl`
        - `extension=pdo_sqlite`
    - 시간대 설정
        
        ```
        [Date]
        ; Defines the default timezone used by the date functions
        ; http://php.net/date.timezone
        date.timezone = Asia/Seoul
        ```
        
    - 에러 리포팅 설정
        
        ```
        error_reporting = E_ALL & ~E_NOTICE & ~E_DEPRECATED & ~E_USER_DEPRECATED
        ```
        
5. `Apache24/conf/httpd.conf` 설정
    - 가장 아래 부분에 다음 코드 입력
        
        ```
        PHPIniDir "C:/php8"
        LoadModule php_module "C:/php8/php8apache2_4.dll"
        AddHandler application/x-httpd-php .php
        AddType application/x-httpd-php .php .html
        ```
        
    - `IfModule dir_module` 설정
        
        ```
        <IfModule dir_module>
            DirectoryIndex index.php index.html
        </IfModule>
        ```
        
6. 정상 작동 확인 
    - `Apache24\htodcs` 폴더에 php 파일 생성 후 php 설정 출력 코드를 입력
        
        ```php
        <?php
        phpinfo();
        ?>
        ```
        
- 브라우저에서 `로컬호스트/<php 파일 경로>` 로 접속시 php 설정이 출력되면 정상

## 기본적인 사용법

### 입력 방법

- php 코드
    
    ```php
    <?php
    echo "Hello PHP"; // Hello PHP
    ?>
    ```
    
- html 출력
    
    ```html
    <html>
      <head></head>
      <body>Hello PHP</body>
    </html>
    ```
    

### 코딩컨벤션

- 변수명, 함수명: 카멜 케이스
- 클래스명: 파스칼 케이스

### 변수 및 자료형

- php에서 변수는 `$변수명` 의 형태로 선언한다
- `var_dump`는 표현식의 자료구조를 출력하는 표준함수이다
    
    ```php
    <?php
    $intOne = 1; // int
    $intTwo = 2; // int
    $plus = $intOne + $intTwo; // 연산
    $float = 3.14; // float
    $string = 'hello'; // string
    $array = array(1,2,3,4); // array
    $associativeArray  = array('a'=>1, 'b'=> 2); // associative array (연관배열)
    
    var_dump($intTwo);echo "<br />"; // int(2)
    var_dump($plus);echo "<br />"; // int(3)
    var_dump($float);echo "<br />"; // float(3.14)
    var_dump($string);echo "<br />"; // string(5) "hello"
    var_dump($array);echo "<br />"; // array(4) { [0]=> int(1) [1]=> int(2) [2]=> int(3) [3]=> int(4) }
    var_dump($associativeArray);echo "<br />"; // array(2) { ["a"]=> int(1) ["b"]=> int(2) }
    ?>
    ```
    

### 배열

- 선언
    
    ```php
    // 배열은 array() 혹은 [] 로 선언한다
    $a1 = array(1,2,3,4); // array(4) { [0]=> int(1) [1]=> int(2) [2]=> int(3) [3]=> int(4) }
    $b1 = [1,2,3,4]; // array(4) { [0]=> int(1) [1]=> int(2) [2]=> int(3) [3]=> int(4) }
    ```
    
- 항목 추가
    
    ```php
    // 배열에 항목을 추가할 때는 array_push(배열, 넣을 값) 의 형식으로 사용한다
    array_push($a1, 5);
    var_dump($a1);echo "<br />"; // array(5) { [0]=> int(1) [1]=> int(2) [2]=> int(3) [3]=> int(4) [4]=> int(5) }
    ```
    
- 항목 제거
    
    ```php
    /* 배열에서 항목을 삭제할 때는 변수를 제거하는 구문인 unset 을 사용한다.
    남은 배열의 다른 항목들의 인덱스가 재배치되지 않는다는 점에 유의해야 한다. */
    unset($a1[0]);
    var_dump($a1);echo "<br />"; // array(4) { [1]=> int(2) [2]=> int(3) [3]=> int(4) [4]=> int(5) }
    ```
    

### 연관배열 (Associative Array)

- 연관배열은 `[키]⇒"값"` 의 쌍으로 이루어진 자료형이다
    - 연관배열은 `array_push` 가 안 먹히는 것 같다…?
    - 일반배열 또한 키가 숫자열의 형태로 자동으로 붙는 연관배열이다
    
    ```php
    $b = array('one' => 'a');
    var_dump($b);echo "<br />"; // array(1) { ["one"]=> string(1) "a" }
    ```
    

### 연산자

- php는 다른 언어들과 달리 문자열 연결을 `+`가 아니라 `.`로 한다는 것을 유의해야 한다

```php
/* 문자열 연결 */
$first = 'hi ';
$second = "php";
$link = $first . $second;
var_dump($link);echo "<br />"; // string(6) "hi php"

/* 템플릿 스트링 */
$template = "$first nice to meet you. $second";
var_dump($template);echo "<br />"; // string(25) "hi nice to meet you. php"

/* 비교 연산자 */
$a = "aaa";
$b = "bbb";

$compare1 = $a != $b;
var_dump($compare1);echo "<br />"; // bool(true)

$compare2 = $a <> $b;
var_dump($compare2);echo "<br />"; // bool(true)

var_dump($compare1 === $compare2);echo "<br />"; // bool(true)

```

### 조건문

- `date`는 현재 날짜와 시간을 가져오는 표준함수
    - `date('s')` 를 입력하면 현재 초를 가져온다

```php
$second = date('s');
echo $second;
if ($second % 3 == 0) {
    echo " : 나머지가 0임";
}
elseif ($second % 3 == 1) {
    echo " : 나머지가 1임";
}
else {
    echo " : 나머지가 2임";
}
```

### 반복문

```php
$a = array(1,2,3,4,5);
foreach($a as $item){ // 값을 출력
    echo $item;
    echo "<br />";
}

echo "<br />";
$b = array('a'=>10, 'b'=>20, 'c'=> 'hi php');
foreach($b as $key => $value){ // 키와 값을 출력
    echo "$key => $value";
    echo "<br />";
}
```

### 함수

```php
/* function */
function niceToMeet($var)
{
    echo "nice to meet $var";
}
nicetomeet("you"); // nice to meet you

/* default parameter */
echo "<br />";
function defaultfunc($name='yse'){
    echo "my name is $name";
}
defaultfunc(); // my name is yse

echo "<br />";
defaultfunc('30min php'); // my name is 30min php
```

### 익명함수

- php는 함수에서 global로 선언하지 않은 외부 변수를 가져오려면 `use(외부변수명)` 키워드를 사용해야 한다

```php
$datas = [1,2,"3","4","오","률",7];
$checker = 2;

$filter_data = array_filter($datas, 
    function($item) use ($checker) {
        return $item == $checker;
    }
);

var_dump($filter_data); // array(1) { [1]=> int(2) }
```

### 클래스

- 다른 언어에서는 클래스와 생성자의 이름이 동일하지만 php에서는 `__construct`라는 키워드로 생성자를 나타낸다
- 인스턴스의 멤버 변수나 메소드를 참조할 때는 `→` 를 사용한다
- 정적 메소드나 프로퍼티를 호출할 때는 `::` 를 사용한다
- 인스턴스가 자기 자신을 호출할 때는 `$this`를, 클래스가 자기 자신을 호출할 때는 `self`를 사용한다

```php
class Sample // 클래스 선언
{
    // 멤버 변수
    private $name; // 멤버 변수를 정의할 때는 `$`를 붙인다
    private $age;

    // 생성자
    public function __construct()
    {
        $this->name = "yse"; // 멤버 변수에 접근할 때는 `$`를 붙이지 않는다
        $this->age = "10";
    }

    // 메서드
    public function tell()
    {
        echo "my name is {$this->name} .";
        echo " and my age is {$this->age} .";
    }

    // 메서드 체이닝
    public function add_age($age)
    {
        $this -> age += $age; // 멤버변수 참조
        return $this; // 인스턴스 자신을 리턴
    }

    // 정적 메서드
    public static function factory()
    {
        return new Sample();
    }

    public static function factory2()
    {
        return self::factory(); // 정적 메서드 호출
    }    
}

$sample = new Sample(); // `$sample`은 인스턴스, `Sample`은 타입
$sample -> tell(); // my name is yse . and my age is 10 .

echo "<br />";
Sample::factory() -> add_age(3) -> tell(); // my name is yse . and my age is 13 .
```

## 서버 만들기

### GET 요청 접수

```php
$name = $_GET['name']; // URL Parameter
$age = $_GET['age'];

echo "name is $name, age is $age"; // name is yse, age is 22
```

### POST 요청 접수

```php
<form method="post">
    name : <input type="text" name="name" />
    age : <input type="text" name="age" />
    <input type="submit" />
</form>

<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $name = $_POST['name'];
    $age = $_POST['age'];

    echo "name is $name, age is $age";
}
?>
```

### 리다이렉트

```php
header("Location: /<이동시킬 주소>");
exit();
```

### 파일시스템

```php
$data = "hi";
file_put_contents("data.txt", $data); // 파일 쓰기

$load_data = file_get_contents('data.txt'); // 파일 읽기

echo $load_data;
```

### 모듈화
```php
/* main.php */
<?php
require("before.php");

echo "this is main file : ";
echo $var;
echo "<br />";

require("after.php");
?>
```

```php
/* before.php */
<?php
$var = "common";

echo "this is before file : ";
echo $var;
echo "<br />";
?>
```

```php
/* after.php */
<?php
echo "this is after file : ";
echo $var;
echo "<br />";
?>
```
