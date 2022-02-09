# 자바스크립트의 목적과 셀렉터

HTML 조작과 변경을 위해서

- Alert창 띄우고 닫기

```html
<body>
    <h2 id="hello">안녕하세요</h2>
    <script>
      **document.getElementById("hello").innerHTML = "안녕";** 
    </script>
  </body>
```

→ ‘안녕하세요' → ‘안녕’으로 바뀜!

```jsx
document.getElementById("hello").??? = "???";
```

→ 여러가지를 바꿀 수 있음(구글검색)

## onclick

### Alert 창 만들기

버튼 누르면 Alert 등장

- UI 만드는 법
1. 미리 디자인해놓고 숨기기
2. 버튼 누르거나하면 보여주기

```jsx
document.getElementById("hello").??? = "???";
```

이 형식으로 alert 박스를 display: block으로 변경하도록 설정해야 함!

```html
<body>
    <div class="alert-box" id="alert">Alert 박스</div>
    <button onclick="document.getElementById('alert').style.display = 'block';">
      버튼
    </button>
    <script></script>
  </body>
```

→ 버튼을 누르면 Alert 박스 창이 나오도록

닫기 버튼 누르면 Alert 박스 창 사라지게 만들기

```html
<button onclick="document.getElementById('alert').style.display = 'none';">
      닫기
</button>
```

## Function

function을 쓰면 긴 코드를 깔끔하게 한 단어로 축약 가능

```jsx
function 아무렇게나 작명() {
긴 코드 ~
}
```

→ `아무렇게나 작명()`  쓸 때마다 `긴 코드` 가 실행됨

```jsx
function 알림창열기() {
document.getElementById('alert').style.display = 'block';
}
```

→ `알림창열기()` 쓸 때마다 안의 `긴 코드` 가 실행!

```jsx
<body>
    <div class="alert-box" id="alert">Alert 박스</div>
    **<button onclick="알림창열기()">버튼</button>**
    <button onclick="document.getElementById('alert').style.display = 'none';">
      닫기
    </button>
    <script>
      function 알림창열기() {
        document.getElementById("alert").style.display = "block";
      }
    </script>
  </body> 
```

- 초보때 자주 겪는 버그

변경할 HTML 요소는 위에, JS로 조작은 밑에서!

→ HTML 요소 위에  JS 조작하면 에러 발생!

### 함수의 파라미터(구멍)

1. 함수에 구멍 뚫어 노으면
2. 앞으로 함수 쓸 때 () 안에 아무 내용이나 입력 가능

```jsx
function 알림창열기(***구멍***) {
        document.getElementById("alert").style.display = ***구멍***;
      }
```

```jsx
알림창열기(123); // 알림창열기() 실행하는데, 구멍에 123 넣어서 실행 시키기
```

```jsx
**<button onclick="알림창열기('block')">버튼</button>
    <button onclick="알림창열기('none')">닫기</button>**
    <script>
      function 알림창열기(구멍) {
        document.getElementById("alert").style.display = 구멍;
      }
</script>
```

→ ‘알림창 열기’라는 하나의 함수로 ‘열기', ‘닫기' 모두 가능

ex2)

```jsx
function plus() {
        2 + 1;
      }
      plus();

      function plus2() {
        2 + 2;
      }
      plus2();
...
```

함수 여러 개 만들기 대신

```jsx
function plus(구멍) {
        2 + 구멍;
      }
      plus(1); // '구멍' 자리에 1을 넣어 주세요
```

구멍을 콤마로 여러개 사용 가능

```jsx
 function 알림창열기(구멍1, 구멍2 ...) {
}
```

### 과제

```jsx

function 알림창1열기() {
1. 제목바꾸기
document.getElementById("alert").innerHTML = "아이디를 입력하세요";
2. 열기
document.getElementById("alert").style.display = 'block';
}
```

## 이벤트 리스너

`onclick` 안쓰고 개발 가능

EventListener 

(x) 버튼에서 onclick 대신 사용

기존코드

```jsx
<body>
    <div class="alert-id" id="id">
      아이디를 입력하세요<button onclick="아이디('none')">X</button>
    </div>
```

변경된 코드

```jsx
<body>
    <div class="alert-id" id="id">
      아이디를 입력하세요<button id="close">X</button>
    </div>
```

```jsx
document.getElementById('close').addEventListener('click', function(){
   document.getElementById("id").style.display = "none"; //실행할 코드(꺼주세요) 
});
```

`close` 요소가 클릭되면 코드실행해 주세요 → JS 안쓰고 기능개발

![스크린샷 2022-02-08 오후 8.39.54.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5db1e2e1-6a7b-495a-949f-9cc3441199b4/스크린샷_2022-02-08_오후_8.39.54.png)

### Event

click : 클릭

keydown : 키보드 입력

scroll : 스크롤

mouseover : 마우스 갖다댐

## jQuery

자바스크립트를 짧게 사용할 수 있는 라이브러리 → 적게 쓰고도 같은 기능할 수 있음

요즘은 잘 쓰지 않음 why? React가 있어서

but jQuery 없느 웹사이트 없어서 안배울 수는 없음

### jQuery 설치

1. jQuery 파일 받아서 첨부

구글에 다운 받아서 

`<script src="아까 다운받은 그 파일 경로"></script>`

1. CDN

```jsx
<script
  src="https://code.jquery.com/jquery-3.5.1.min.js"
  integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0="
  crossorigin="anonymous"></script>
```

### jQuery 설치 위치

→ 위에 있으면 브라우저 로딩이 오래걸림

→ 웹 구성요소(html)가 있는 body 태그 다음에 두는게 좋음!

→ body 태그 끝나기 전에 넣는게 좋음!

### jQuery로 HTML 변경하는 법

`document.getElementById("hello").??? = "???";` 에서 

`document.getElementById("hello")`  = `$("# hello")` 

→ id가 hello 인 셀렉트를 찾아주세요

`$(".hello")` → class가 hello인 셀렉트를 찾아주세요(마침표)

 `document.getElementById("hello").innerHTML` = `$("#test").html("안녕")`  

`$("#hello").css("color", "red")` → HTML 스타일 변경

`$("#hello").attr("src", "~~~")` → HTML 속성 변경 ex) src, href ..

jQuery로 HTML 출력은 그냥 괄호안에 아무 내용도 없이 쓰면 됨!
