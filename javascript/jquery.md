# jQuery

### jQuery 객체

* 제이쿼리를 사용하려면 먼저 jQuery 객체를 생성해야 한다.
* `$()` 함수는 선택자에 의해 선택된 요소들을 jQuery 객체로 반환한다. 이렇게 반환된 객체에는 자바스크립트 표준함수를 사용할 수 없으며 제이쿼리 메서드만 사용할 수 있다.
  * 제이쿼리를 배운다는 것은 이 객체에 들어있는 메서드들의 사용법을 익히는 것이다.
*   같은 종류의 요소가 여러개 있을 때 일괄적으로 이벤트를 등록하는 경우 자바스크립트는 개발자가 임의로 순회해서 접근해야 하는 반면, 제이쿼리는 자동적으로 등록된다

    ```jsx
    $('.btn').on('click', function() { }) // 반복문을 사용하지 않았지만 모든 btn 태그에 클릭 이벤트가 적용되었다
    ```
* `$()` 함수는 자기 자신의 노드를 반환하므로 체이닝을 적용할 수 있다

### 선택자

* 기본 선택자
  * `$("*")` : 모든 요소를 선택
  * `$(".class")` : 지정한 클래스를 가지는 모든 요소를 선택
  * `$("element")` : 지정한 태그명을 가지는 모든 요소를 선택
  * `$("#id")` : 지정한 ID 속성을 가지는 하나의 요소를 선택
  * `$("selector1, selecotr2")` : 모든 지정한 선택자들의 결과들을 결합하여 선택
* 자식 선택자
  * `$("div:first-child")` : 부모의 첫 번째 자식인 모든 요소를 선택
  * `$("div:first-of-type")` : 동일한 요소 이름의 형제 중 첫 번째 요소를 모두 선택
  * `$("div:last-child")` : 부모의 마지막 하위 요소인 모든 요소를 선택
  * `$("div:nth-child(n)")` : 부모의 n 번째 자식인 모든 요소를 선택
  * `$("div:last-child(n)")` : 마지막 요소에서 첫 번째 요소까지 계산하여 부모의 n 번째 자식인 모든 요소를 선택
  * `$("div:only-child")` : 부모의 유일한 자식인 모든 요소를 선택
* 계층 선택자
  * `$("parent > child")` : 지정된 부모의 모든 자식 요소 선택
  * `$("ancestor descendant")` : 지정된 조상의 자손인 모든 요소 선택
  * `$("target+filter")` : 대상을 기준으로 조건과 일치하는 첫 번째 형제 요소를 선택
  * `$("#prev~div")` : 대상을 기준으로 조건과 일치하는 모든 형제 요소를 선택

### 이벤트 핸들러

*   `.on()`

    * 여러 요소를 하나의 이벤트 핸들러에 연결

    ```jsx
    // 모든 <button>요소에 mouseenter와 click mouseleave 이벤트를 설정함.
    $("button").on("mouseenter click mouseleave", function() {
      $("#text").append("마우스가 버튼 위로 진입하거나 클릭하거나 빠져나갔어요!<br>")
    })
    ```

    * 하나의 요소에 여러 이벤트 핸들러를 사용하여 여러 이벤트를 연결

    ```jsx
    $("button").on({ // 모든 <button>요소에
    	mouseenter: function() { // mouseenter 이벤트를 설정함.
    	  $("#text").append("마우스가 버튼 위로 진입했어요!<br>")
      },
      click: function() {      // click 이벤트를 설정함.
        $("#text").append("마우스가 버튼을 클릭했어요!<br>")
      },
      mouseleave: function() { // mouseleave 이벤트를 설정함.
        $("#text").append("마우스가 버튼 위에서 빠져나갔어요!<br>")
      }
    })
    ```
*   `.one()`

    * `.on()` 과 거의 같지만 이벤트가 단 한 번만 실행된다는 차이가 있다

    ```jsx
    $("button").one("click", function() {
    	// 모든 <button>요소가 처음 클릭됐을 때에만 실행됨.
      $("#text").append("첫 번째 클릭이에요!<br>")
      
    	// 모든 <button>요소가 두 번째 클릭됐을 때부터는 이 이벤트 핸들러가 실행됨.
      $(this).click(function() {
        $("#text").append("이 버튼을 벌써 클릭했네요!<br>")
      })
    })
    ```
*   `.off()`

    * 이벤트의 연결을 제거한다

    ```jsx
    $("#clickBtn").on("click", function() { // id가 "clickBtn"인 요소를 클릭했을 때 실행됨.
      $("#text").append("버튼을 클릭했어요!<br>")
    })

    $("#removeBtn").on("click", function() {
      $("#clickBtn").off("click"); // id가 "clickBtn"인 요소의 클릭 이벤트와의 연결을 제거함.
    })
    ```

### ajax

*   `$get()`

    ```jsx
    $.get("https://jsonplaceholder.typicode.com/todos/1", function(data) {
    	$(".result").html(alert(JSON.stringify(data)))
    })
    ```
*   `$post()`

    ```jsx
    $.post("https://jsonplaceholder.typicode.com/posts", {
      method: 'POST',
    	body: { title: 'foo', body: 'bar', userId: 1 },
      headers: { 'Content-type': 'application/json; charset=UTF-8' }
    },

    function(data, status) {
      $("#text").html(alert(JSON.stringify(data)))
    })
    ```

    ### `$().index(this)` 메서드

    ```jsx
    $("ul > li").click(function () { // li 요소들 중 하나를 클릭하는 경우
      let num = $("li").index(this); // 형제 요소들 간의 인덱스 순서를 구해서
      $('.result > p > span').text(num + 1) // 반환한다
    });
    ```
