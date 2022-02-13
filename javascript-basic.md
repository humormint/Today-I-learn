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
  **<button onclick="document.getElementById('alert').style.display = 'block';">
    ** 버튼
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

→ `아무렇게나 작명()` 쓸 때마다 `긴 코드` 가 실행됨

```jsx
function 알림창열기() {
  document.getElementById("alert").style.display = "block";
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

→ HTML 요소 위에 JS 조작하면 에러 발생!

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
document.getElementById("close").addEventListener("click", function () {
  document.getElementById("id").style.display = "none"; //실행할 코드(꺼주세요)
});
```

`close` 요소가 클릭되면 코드실행해 주세요 → JS 안쓰고 기능개발

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
  crossorigin="anonymous"
></script>
```

### jQuery 설치 위치

→ 위에 있으면 브라우저 로딩이 오래걸림

→ 웹 구성요소(html)가 있는 body 태그 다음에 두는게 좋음!

→ body 태그 끝나기 전에 넣는게 좋음!

### jQuery로 HTML 변경하는 법

`document.getElementById("hello").??? = "???";` 에서

`document.getElementById("hello")` = `$("# hello")`

→ id가 hello 인 셀렉트를 찾아주세요

`$(".hello")` → class가 hello인 셀렉트를 찾아주세요(마침표)

`document.getElementById("hello").innerHTML` = `$("#test").html("안녕")`

`$("#hello").css("color", "red")` → HTML 스타일 변경

`$("#hello").attr("src", "~~~")` → HTML 속성 변경 ex) src, href ..

jQuery로 HTML 출력은 그냥 괄호안에 아무 내용도 없이 쓰면 됨!

## Bootstrap으로 모달창 UI 만들기

대문(jumbotron) 만들기

1. HTML로 미리 디자인 해놓고
2. 숨겨 뒀다가
3. 버튼 눌렀을 때 보여줌

모달창 → 보통 body 태그 맨 위에 만듦

```css
.main-background {
  background-image: url(computer.jpeg);
  background-size: cover; /* 이미지가 찌그러지지 않는 한도 내에서 제일 크게 설정 */
  height: 600px;
  color: white;
  margin: auto;
}
.black-background {
  background: rgba(0, 0, 0, 0.5);
  position: fixed; /* 브라우저 화면에 딱 달라붙음*/
  z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치*/
  width: 100%;
  height: 100%;
}
.white-background {
  background: white;
  width: 80%;
  margin: 100px auto; /* top 100px, 나머지 auto */
  padding: 20px;
  border-radius: 10px;
}
```

→ 평상시에 안보여야 하니까 `display: none;` 으로 설정

### 이벤트 리스너와 jQuery를 활용한 모달창

→ 로그인 버튼 누르면 모달창 띄도록 만들기

`addEventListener` 대신에 `on()` (제이쿼리 문법)

```jsx
<script>
      $('.btn-lg').on('click', function(){$(".black-background").fadeIn();});
    </script>

//'btn-lg'라는 클래스를 클릭하면 다음 함수를 실행해라
```

`.fadeIn()` : 서서히 뜨도록 하기

`.fadeOut()` : 서서히 사라지도록 하기

`.slideDown()` : 위에서 아래로 내려가면서 보여줌

`.slideUp()` : 아래에서 위로 올라가면서 보여줌

## nav 메뉴 만들기

- 메뉴바 만들기

버튼 누르면 서브메뉴 출현!

bootstrap → list group

```jsx
$("#nav-sub-btn").on("click", function () {
  $(".nav-sub").slideDown();
});
//'nav-sub-btn' 클릭하면, 'nav-sub' 메뉴바 아래로 내리기
```

`.on(’click’, ~ )` 대신, `.click( ~`으로 대체해도 됨!

버튼 다시 누르면 메뉴바 안보이게 만들기

만약에 지금 list가 안보이면 보이게 해주고

만약에 지금 list가 보이면 안보이게 해주세요

→ 자바스크립트로 하면 코드 5 ~ 6줄을 jQuery를 사용하면 1줄에 끝남

`slideDown()` 대신, `slideToggle()` 사용하면 됨! → 누를 때마다 Up, Down 반복

비슷한 예)

fadeIn/Out을 왔다갔다

### 메뉴바 코드

html 코드

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="black-background">
      <div class="white-background"><p>로그인하세요</p></div>
    </div>
    <div class="nav-menu">
      <h1>Shirts Studio</h1>
      <a id="nav-sub-btn">Products</a>
    </div>
    <div class="nav-sub">
      <ul class="list-group">
        <li class="list-group-item">An item</li>
        <li class="list-group-item">A second item</li>
        <li class="list-group-item">A third item</li>
        <li class="list-group-item">A fourth item</li>
        <li class="list-group-item">And a fifth one</li>
      </ul>
    </div>
    <div class="jumbotron main-background">
      <p style="margin:0;" class="display-4 title ">Shirts Studio</p>
      <p class="lead">
        This is a simple hero unit, a simple jumbotron-style component for
        calling extra attention to featured content or information.
      </p>
      <hr class="my-4" />
      <p>
        It uses utility classes for typography and spacing to space content out
        within the larger container.
      </p>
      <p class="lead">
        <a class="btn btn-primary btn-lg" href="#" role="button">Log In</a>
      </p>
    </div>
    <script
      src="https://code.jquery.com/jquery-3.5.1.min.js"
      integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0="
      crossorigin="anonymous"
    ></script>
    <script>
      $(".btn-lg").on("click", function () {
        $(".black-background").fadeIn();
      });
      $("#nav-sub-btn").on("click", function () {
        $(".nav-sub").slideToggle();
      });
    </script>
  </body>
</html>
```

CSS 코드

```css
.main-background {
  background-image: url(computer.jpeg);
  background-size: cover; /*이미지가 찌그러지지 않는 한도 내에서 제일 크게 설정*/
  height: 600px;
  color: white;
  margin: auto;
}
.black-background {
  background: rgba(0, 0, 0, 0.5);
  position: fixed; /* 브라우저 화면에 딱 달라붙음*/
  z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치*/
  width: 100%;
  height: 100%;
  display: none;
}
.white-background {
  background: white;
  width: 80%;
  margin: 100px auto; /* top 100px, 나머지 auto */
  padding: 20px;
  border-radius: 10px;
  text-align: center;
}
.title {
  font-size: 60px;
  text-align: center;
  padding: 20px;
}
.nav-menu {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.nav-sub {
  display: none;
}
#nav-sub-btn {
  cursor: pointer;
}
```

## if else 문

if 조건문 : 특정 조건이 맞을 때만 코드를 실행하고 싶을 때 사용

모달창에 조건을 줘서 조건이 맞으면 모달창 뜨도록 만들기

`<input>` 창에 입력된 값이 ‘안녕' 일 때만 `Log In` 버튼 누르면 모달창 오픈

jQuery로 input 가져오는 법 → `.val()` 사용하면 됨

```jsx
$('.btn-lg').on('click', function(){
      if($("#test-input").**val()**=="안녕") { $('.black-background').fadeIn();
      }
    });
```

세트로 묶인 if 문 특징

→ 위에서부터 읽어내려가다가 조건이 맞은 하나만 실행함(if이거나 else if 이거나 else이거나)

→ 그 뒤의 if / else는 해석하지 않음

모달창 내에 form태그와 input 태그 추가하기 + 전송/닫기 버튼 추가하기

모달창 내부 복붙용 Form 코드 (bootstrap을 이용한 Email과 Password)

```jsx
<form action="login.php">
  <div class="form-group">
    <input type="email" class="form-control" placeholder="Email" id="email">
  </div>
  <div class="form-group">
    <input type="password" class="form-control" placeholder="Password">
  </div>
  <button type="submit" class="btn btn-primary">전송</button>
</form>
```

이메일 input 빈칸 검사기능 만들기

폼이 전송 될 때

만약에 이메일 input에 입력된 값이 빈칸인 경우,

폼의 전송을 막음, 안내문 띄움

`e.preventDefaul();` → form 의 전송을 막음!

→ 이메일 input이 빈칸인 경우 전송이 안되어야함

→ 빈칸이 아니면 전송(새로고침) 되어야함

이**메일 input에 입력된 값 == 빈칸**

```jsx
$("form").on("submit", function (e) {
  //form을 전송하지 마라
  if ($("#email").val() == 빈칸) {
    e.preventDefault();
  }
});
```

코드

```jsx
$("form").on("submit", function (e) {
  if ($("#email").val() == "") {
    // 이메일 input에 입력된 값이 빈칸이면
    e.preventDefault(); //form을 전송하지 마라
  }
});
```

안내문 띄우기

비밀번호 입력란도 공백검사

→ 폼이 전송될 때

만약에 이메일 input에 입력된 값이 빈칸인 경우,

폼의 전송을 막음, 안내문 띄움

만약에 패스워드 input에 입력된 값이 빈칸인 경우,

폼의 전송을 막음, 안내문 띄움

```jsx
$("form").on("submit", function (e) {
  //form을 전송하면 이벤트 함수를 실행하라
  if ($("#email").val() == "") {
    // 이메일 input에 입력된 값이 빈칸이면
    e.preventDefault(); //form을 전송하지 마라
    $("#email-alert").show(); // 안내창을 보여줌
  }

  if ($("#psw").val() == "") {
    e.preventDefault();
    $("#psw-alert").show();
  }
});
```

form과 관련된 이벤트들

`input` → input에 값을 입력할때 이벤트 발생(값이 변경될 때 바로)

`change` → input에 값이 변할때 이벤트 발생( 값이 변경되고 focus를 잃을 때)

## 변수와 변수 활용법

`var 변수 이름 = 저장하고 싶은 값`

ex) `var 이름 = ‘john’;`

특히 이름이 길때 ex) var 이름 =’john sdadasddsda’

일때 `이름;` 만 치면 이름 입력할 수 있음

`$(’#email-alert')`같은 셀렉터 여러번 있을 경우 변수에 담아서 사용하면 좋음 (자바스크립트는 html요소 찾는데 시간이 오래 걸리기 때문에)

`$(’#email-alert').show();` → `var 이메일안내창 = $('#email-alert')` 와 `이메일안내창.show();`

ex)

`var 나이 = 20;` → 선언과 할당을 동시에 할 수 있음

선언 : `val = 이름` → 변수를 만들겠다.

할당 : `나이 = 20` → 값을 집어 넣는것, 여러 번 쓸 수 있음(재할당)

범위 : 변수가 쓰이는 범위, 일반적으로 function 내부

ES6 문법

`var` → 재선언 가능, `범위가 function`

`let` → 재선언이 불가능한 변수를 만들 때, 범위가 중괄호 `{}`

`const` → 재선언 불가능, 재할당도 불가능, 범위가 중괄호 `{}`

## 애니매이션 UI 1 : jQuery Animate 함수

- Javascript는 Css에 비해 사용자의 키입력, 마우스입력 체크 등 다양한 기능을 이용할 수 있음
  ### 왼쪽 슬라이드메뉴 만들기
  `jQuery animate()` 함수
  CSS 속성을 서서히 변경하고플 때
  ```jsx
  $('#hi').click(function() {
        $('#hi').animate({marginLeft : '100px'});
  ```
  → `hi` 태그 클릭하면 margin 왼쪽으로 100px 줄 것 (오른쪽 이동)
  여러 개 적용 할 때 콤마(,) 사용
  `jQuery animate({CSS속성}, 숫자)` → 숫자에 걸쳐서 애니매이션 실행 ex) 5000일 경우, 5초에 걸쳐 실행!
  showMenu 버튼을 누르면 저 메뉴가 왼쪽에서 슬그머니 등장
