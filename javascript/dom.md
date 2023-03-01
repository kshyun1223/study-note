# DOM

### window 객체

* 브라우저의 최상위 디렉토리에 있는 객체이다
* BOM과 DOM은 window의 하위 객체이다
  * 브라우저 객체(BOM; Browser Object Model)
  * 문서 객체(DOM; Document Object Model)

### 식별자(identifier)

*   어떠한 값을 돌려받아 반환하는 종류의 메서드는 이름에 get이나 select가 들어가 있다

    ```javascript
    /* getElementById: ID를 기준으로 접근 */
    document.getElementById("root");

    /* getElementsByTagName: 태그명을 기준으로 모두 수집하여 배열로 반환 */
    document.getElementsByTagName("li");

    /* querySelector: 선택자를 query한다 -> CSS 선택자로 노드에 접근 */
    document.querySelector("#root > section");

    /* querySelectorAll: CSS 선택자로 노드에 접근하여 조건에 부합하는 모든 노드를 반환 */
    document.querySelectorAll("#root > ul > li");

    /* getElementsByClassName: 클래스를 기준으로 모두 수집하여 배열로 반환 */
    document.getElementsByClassName("class-attribute");
    ```

### 속성(property)

*   특정 노드의 내용에 접근하려면 `textContent` 속성으로 들어가야 한다

    * for + textContent

    ```javascript
    for(let i = 1; i <= 200; i++) {
        let doojin = document.createElement("li"); // 선언
        doojin.textContent = "li items" + i; // index
        root.appendChild(doojin); // 할당
      }
    ```
* `length`: 배열이나 문자열의 길이에 접근하려면 `length` 속성으로 들어가야 한다
* `innerHTML`: HTML 마크업 문자열로 간단히 DOM 조작이 가능하다
  * 엘리먼트 노드의 innerHTML 프로퍼티를 참조하면 엘리먼트 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이)에 포함된 모든 HTML 마크업을 문자열로 반환한다
  * 여기에 문자열을 할당하면 문자열에 포함된 HTML 마크업이 파싱되어 엘리먼트 노드의 자식 노드로 DOM에 반영된다

### addEventListener + 클릭 이벤트

```javascript
element.addEventListener("click", function() {
  document.getElementById("demo").innerHTML = "Hello World"; // 처리할 내용
});
```

### 이벤트 객체(event object)

* 이벤트는 상당히 빈번하게 만들기 때문에 자바스크립트에 자동화 기능이 내장되어 있다
* 자동화된 기능을 사용할 때는 예상치 못한 버그가 발생할 수 있기 때문에 반드시 검증이 필요하다
* 이를테면 **조건문으로 데이터타입**을 제한할 수 있다
  * 조건문에서는 `&&`(and)와 `||`(or) 연산자를 사용하면 코드량을 상당히 줄일 수 있다

```javascript
function style(containerElement, operateColor, eventType){
  if(typeof(containerElement) === "object" && 
     typeof (operateColor) === "string" &&
     typeof (eventType) === "string"
    ){
    let colorData = operateColor;
    containerElement.addEventListener(eventType, function(event){
      event.target.style.backgoundColor = colorData;
    });
  } else {
    console.log("첫번째 매개변수 타입이 객체여야 합니다");
  }
}
```

### DocumentFragment

```javascript
const virtualElement = document.createDocumentFragment(); 
const names = ["피카츄", "라이츄", "파이리", "꼬부기", "버터풀"];

names.forEach((value) => { 
  const section = document.createElement('section');
  const textNode = document.createTextNode(value);
  section.appendChild(textNode);
  virtualElement.appendChild(section); // virtualElement에 section을 할당
});

document.body.appendChild(virtualElement); // body에 virtualElement를 할당
```

