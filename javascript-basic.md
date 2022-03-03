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

## 위에서부터 등장하는 모달창 만들기

애니메이션 만드는 방법

1. 시작화면/최종화면 만들기
2. 자바스크립트로 트리거 하기
3. 스무스한 동작은 animate 함수 잘 안쓰고 CSS 속성 씀 (더 빨라서)

→ transition 이용!

→ 트리거는 자바스크립트로 하고 스무스한 동작은 transition으로!

```jsx
".btn-lg".on("click", function () {
  $(".black-background").fadeIn();
});
```

→

```jsx
$(".btn-lg").on("click", function () {
  $(".black-background").show();
  $(".black-background").animate({ marginTop: "0px" }); //최종화면
});
```

```css
.black-background {
    background: rgba(0,0,0,0.5);
    position: fixed; /* 브라우저 화면에 딱 달라붙음 */
    z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치 */
    width: 100%;
    height: 100%;
    **display: block; /* 모달창이 보여야 하니까 none 대신 block */
    margin-top: -1200px; /* 위에 있다가 내려오도록 */**
}
```

→

```jsx
$('.btn-lg').on('click', function() {
      $('.black-background')**.show().animate**({marginTop : '0px'});
    });
```

→ `show()` 와 `animate` 겹쳐서 사용할 수 있음!

요즘은 animate 대신 CSS 주로 이용함!

```jsx
$('.btn-lg').on('click', function() {
      $('.black-background').**css('margin-top', '0px'**); /* margin-top을 0px로*/
    });
```

```css
.black-background {
  background: rgba(0, 0, 0, 0.5);
  position: fixed; /* 브라우저 화면에 딱 달라붙음 */
  z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치 */
  width: 100%;
  height: 100%;
  display: block;
  transition: all 3s;
  margin-top: -1000px;
}
```

프로의 애니메이션 개발 팁

margin width position left right heght 애니메이션 금지 (건드리지 않는 것이 좋음!)

→ 동작시간이 오래걸릴 수 있음 → transform 이용!

→ margin 대신 transform 사용!

```jsx
$(".btn-lg").on("click", function () {
  $(".black-background").css("transform", "translateY(0px)"); // 0px이 최종 모습
});
```

```css
.black-background {
  background: rgba(0, 0, 0, 0.5);
  position: fixed; /* 브라우저 화면에 딱 달라붙음 */
  z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치 */
  width: 100%;
  height: 100%;
  display: block;
  transition: all 3s;
  transform: translateY(-1000px); /* margin-top 대신 쓰는게 훨씬 좋음 */
}
```

가장 좋은 방법

→ CSS class를 부착하는 방향으로 시작화면/최종화면 개발

`$('.black-background').css('transform', 'translateY(0px)');` 대신, `addClass()` 함수 사용하는 것이 더 좋음!

```jsx
$(".btn-lg").on("click", function () {
  $(".black-background").addClass();
});
```

```css
.slide-down {
  transform: translateY(0px);
}
```

## 정규식으로 이메일 형식 검증해보기

→ 문자를 검사할때 쓰는 정규식(슬래시 2개로 표현)

`/asadqwd/` → 이 문자에 a나 b가 들어가 있나요??

정규식으로 문자를 검사하는 법

`/abc/.test('abcadasdw')` → 지금 `'abcadasdw'` 문자에 abc라는 글자가 있나요??

### 정규식 핵심 문법

`[괄호]` → 알파벳을 표현하고 싶을때 사용함

ex)

`/[A-z]/.test(’s’)` → 대문자 A부터 소문자 z까지(모든 알파벳) 중 `‘s’`가 있냐?

→ `true`

\S : 특수문자 포함 모든 문자 1개

ex)

`/\S/.test('#')`

→ `true`

이메일을 표현하는 정규식

→ asdasda@dadasd.asdasd

`/\S@\S.\S/` → 모는문자@모든문자.모든문자

\S → 모든 문자이긴 한데 문자 하나를 뜻함

→ `\S+` → 모든 문자 하나 뒤에도 계속 찾기

→`/\S+@\S+\.\S+/` → . 은 따로 구분 해줘야함!

→ `/\S+@\S+\.\S+/.test('dasasd@naver.com')` → `true`

### 이메일 input의 값이 이메일 형식이 아니면 폼 전송 X

만약 지금 이메일 input에 입력된 값이 정규식과 비교했을때 false인 경우

폼 전송 막기, 안내창 띄우기

숙제 1 → 제대로된 이메일 정규식 찾아오기

```jsx
var 입력한이메일 = $('#email').val()
        if (/\S+@\S+\.\S+/.test(입력한이메일) == false ) {
            e.preventDefault();
```

모던 브라우저에선 `<input type="email”` 이라고 쓰면 알아서 email검사 해줌!

→ 이메일 검증이 딱히 필요하지 X

주의점 → 다국어 이메일 주소도 존재 ex) 한글 이메일 → 유연하게 검사할 필요가 있음

### 정규식 테스트

숙제2 → 패스워드 입력란에 대문자 들어 있는지 검사

정규식이랑 동일하냐고 물어보는게 아님! 포함되어 있느냐를 물어봄!

ex) `/abc/.test(’abcasdw’)` → `true` 로 나옴!

꼭 `/abc/.test(’abc’)`로 표현할 필요 없음!

`/[A-Z]+/.test('asdasdqw')` → 모든 영어 대문자가 들어가 있나요? → `false`

```jsx
var 입력한패스워드 = $("#psw").val();
if (/[A-Z]+/.test(입력한패스워드) == false) {
  // 패스워드에 대문자가 없으면 form 전송 막아주세요
  e.preventDefault();
}
```

숙제 3 → 이메일 input 공백검사와 이메일 형식 검사 둘 다 하려면??

```jsx
var 입력한이메일 = $("#email").val();
if (/\S+@\S+\.\S+/.test(입력한이메일) == false) {
  e.preventDefault();
} else if (입력한이메일 == "") {
  // 입력한 이메일이 공백이냐
  e.preventDefault(); // 이메일 형식이 맞더라도 공백검사 추가로 진행
}
```

## 이미지 슬라이드 UI 만들기 (Carousel)

- 버튼을 누르면 다음 화면으로 넘어가는 슬라이드

`100vw` → viewport width : 실제 브라우저 화면의 몇 %를 차지할지

```css
.slide-container {
  width: 300vw;
}
.slide-box img {
  width: 100%;
}
```

2라는 버튼을 누르면 다음 사진 보이도록

→ 이미지 3개를 감싸는 큰 div 박스를 왼쪽으로 100vw만큼 움직이도록!

→ 버튼 2를 투르면 해당 CSS 속성 보여주기

```css
.slide-container {
  width: 300vw;
  transform: translateX(-100vw);
}
```

애니메이션 구현하는 법

1. jQuery animate()
2. CSS transition → `transition: all 1s;`

자바스크립트 trigger만 만들면 됨

버튼2 누르면 `transform: translateX(-100vw);` 가 되어야 함!

```jsx
$(".slide-2").click(function () {
  $(".slide-container").css("transform", "translateX(-100vw");
});
```

UI 만드는 법

1. 시작화면 만들기
2. 최종화면 만들기
3. 자바스크립트 Trigger
4. 애니메이션 넣기

버튼 3을 누르면 ?

→ 3번째 사진이 보이도록 → -200vw만큼 움직이도록 만들기

```jsx
$(".slide-3").click(function () {
  $(".slide-container").css("transform", "translateX(-200vw");
});
```

→ 버그 생길 수 있음

페이지 늘이거나 줄였을 때 반응이 느림 → 이미지를 백그라운드 이미지 속성으로 넣으면 됨

→ `background-image: url()`

`transition: all 1s;` 를 → `transition: transform 1s;` 로 변경하면 width 는 변경하지 않고 transform 속성만 변함 !

숙제 → Next버튼 만들기 → 누르면 다음이미지로 넘어가기

`position: absolute;*/* 요소 겹치거나 띄우기 */` →\* 쓰려면 부모 태그에 position relative가 필요함!

만약에 지금 사진1이 보이면 사진2를 보여주고

사진 2가 보이면 사진 3을 보여주고

```css
.slide-next {
position: absolute; */* 요소 겹치거나 띄우기 */*

top: 45%;

right: 0; */* 오른쪽으로 오게 */*

}
```

```jsx
var 지금보이는사진 = 1;
$(".slide-next").click(function () {
  if (지금보이는사진 == 1) {
    $(".slide-container").css("transform", "translateX(-100vw");
    지금보이는사진 = 2; // 지금 보이는 사진이 2라고 알려줘야 함!
  } else if (지금보이는사진 == 2) {
    $(".slide-container").css("transform", "translateX(-200vw");
    지금보이는사진 = 3;
  }
});
```

### 확장성있는 코드로 다시 개발(사진이 무수히 많아지면 그 때마다 if문을 사용할 수는 없음)

`-100vw`, `-200vw` 대신, `-지금보이는사진00vw`

텍스트 더하기 → ‘글자' + ‘글자’ = ‘글자글자’

```jsx
var 지금보이는사진 = 1;
    $('.slide-next'). click(function() {

    **$('.slide-container').css('transform', 'translateX(-'+ 지금보이는사진 +'00vw)');
    지금보이는사진 = 지금보이는사진 + 1;**
```

→ if문 필요없이 작성이 가능!

→ Next 버튼이 끝없이 동작중

지금 보이는 사진이 3이면 Next 버튼 기능제한

## 함수의 return 문법 & 소수점 다루기

function 문법

1. 긴코드 축약해서 쓸 수 있음
2. 파라미터 추가 가능
3. return → 함수 쓰고 그 자리에 뭔가 뱉고 싶을때 사용(반환)

```jsx
function 함수() {
  return 123; // 함수쓰고 123을 뱉어라
}
var 변수 = 함수(); // 함수에 123 저장
console.log(변수); //123
```

return은 함수 종료 기능도 가지고 있음 → return 밑에 있는 코드는 실행X

return 용도 → 자료를 넣으면 다른 자료가 나오는 변환기 만들고 싶을때 사용

ex) 가격이 60000원 일때 부가세 계산할 때

상품이 1개 일때

```jsx
console.log(60000 * 0.1);
```

but 상품이 많아질때 → 부가세 계산기 만드는게 편리함

```jsx
console.log(vat(50000));

function vat(a) {
  return a * 0.1;
}
vat(50000);
```

자바스크립트에서 소수점과 같이 연산할 때 주의점

→ 1.1 곱하니까 작은 오차가 발생함 why? 컴퓨터는 2진법으로 바꿔서 연산하기 때문에

→ 정확한 연산을 하고 싶으면 라이브러리를 쓰던가 반올림하면 됨

```jsx
console.log(vat(55555)); // 61110.50

function vat(a) {
  var num = (a * 1.1).toFixed(2); // 2째자리 지 반올림
  return parseInt(num); // 문자가 숫자로 바뀜
}
```

`toFixed` 는 문자로 변환됨 → 버그 생길 수 있음 → 숫자연산이 숫자와 문자의 연산으로 인식됨

`parseFloat` 또는 `parseInt` 사용

## 스크롤 애니메이션

→ 스크롤 시 변하는 Navbar 만들기

→ 스크롤 내리면 로고의 폰트가 줄어드는 애니메이션

스크롤 기반 애니메이션 → 나중에 용도가 많음!

![https://codingapple.com/wp-content/uploads/2019/09/navanimation.gif](https://codingapple.com/wp-content/uploads/2019/09/navanimation.gif)

→ jQuery 필요함

navbar가 초기에 투명하다가 스크롤 내리면 검정색으로 변함

UI 애니매이션 만드는 법

1. 시작화면 제작 : 투명한 navbar
2. 최종화면 제작
3. 자바스크립트로 트리거

4. 시작화면 제작 : 투명한 navbar

```css
.nav-menu {
    display: flex;
    justify-content: space-between;
    align-items: center;
    **background-color: transparent;
    position: fixed;/* fixed를 줘야 스크롤 돼도 nav가 보임*/
    z-inedx: 5;
    width: 100%;
}**
```

1. 스크롤바를 내리면 불투명 navbar

`스크롤바를 내리면 .nav-menu이 background: black;`

`window` → viewport

```jsx
/* 스크롤바를 내리면 
      .nav-menu이 background: black; */

$(window).on("scroll", function () {
  $(".nav-menu").css("background", "black"); // 대신 클래스를 부착하는 addClass()를 쓰면 더 좋음
}); // viewport가 scroll되었을 때 코드를 실행해 주세요
```

```html
<div class="nav-menu nav-scroll"></div>
```

→ `nav-scroll` 이라는 새로운 class를 만듦(최종화면을 만들어 주는 class)

```jsx
$(window).on("scroll", function () {
  $(".nav-menu").addClass("nav-scroll"); // 스크롤하면 nav-menu클래스에 nav-scroll클래스를 붙여 주세요
}); // viewport가 scroll되었을 때 코드를 실행해 주세요
```

스크롤을 어느정도 내렸을 때 동작하게 하려면?

but 우리는 스크롤 내리자마자 동작

→ 스크롤 `요만큼` 내리면 동작하도록

→ 스크롤바를 100px 내렸을 때 동작하게 하려면?

→ 만약에 지금 스크롤을 100px 했을 때

`$(window).scrollTop()` → 스크롤된 높이(px)를 알려주는 제이쿼리 함수

```jsx
$(window).on("scroll", function () {
  if ($(window).scrollTop() > 100) {
    // 만약에 지금 스크롤을 100px 했을 때
    $(".nav-menu").addClass("nav-scroll"); // 스크롤하면 nav-menu클래스에 nav-scroll클래스를 붙여 주세요
  }
}); // viewport가 scroll되었을 때 코드를 실행해 주세요
```

숙제 1 : 스크롤 내리면 폰트사이즈 서서히 작아지게

scroll 이벤트 리스너 많이쓰면 안됨 → 스크롤 내릴때마다 코드 실행해야 해서 버벅일 수 있음

h1태그에 클래스 주기

```jsx
<div class="nav-menu">
      <h1 **class="nav-logo"**>Shirts Studio</h1>
      <a id="nav-sub-btn">Products</a>
```

최종화면에서 폰트사이즈 줄이기

```css
.scroll-nav-logo {
  font-size: 30px;
}
.nav-menu h1 {
  /* h1 태그에 적용해야 스크롤 올릴때도 애니메이션 적용됨*/
  transition: all 1s;
}
```

자바스크립트 트리거

```jsx
$(window).on('scroll', function() {
        if ($(window).scrollTop() > 100) { // 만약에 지금 스크롤을 100px 했을 때
      $('.nav-menu').addClass('nav-scroll') // 스크롤하면 nav-menu클래스에 nav-scroll클래스를 붙여 주세요
      **$('.nav-menu h1').addClass('scroll-nav-logo')**  }
    }) // viewport가 scroll되었을 때 코드를 실행해 주세요
```

숙제 2 : 다시 스크롤 올리면 원상태로! (애니메이션 제거)

기존 작성했던 코드는

스크롤바를 100px이상 내렸을 경우 애니메이션을 동작

→ `else` 문을 사용해서 100px 미만일 경우 원상태로 되돌릴 코드를 추가

## 탭 기능 만들기

→ 탭의 html, css는 강의 하단에 첨부

→ 탭으로 탭 기능 만들기

→ 버튼 누르면 주황색 하이라이트 되도록 디자인 + 해당 탭의 내용이 보이도록

UI 만드는법

```css
/* 강의 복사 내용*/
ul.list {
  list-style-type: none;
  margin: 0;
  padding: 0;
  border-bottom: 1px solid #ccc;
}
ul.list::after {
  content: "";
  display: block;
  clear: both;
}
.tab-button {
  display: block;
  padding: 10px 20px 10px 20px;
  float: left;
  margin-right: -1px;
  margin-bottom: -1px;
  color: grey;
  text-decoration: none;
  cursor: pointer;
}
.active {
  border-top: 2px solid orange;
  border-right: 1px solid #ccc;
  border-bottom: 1px solid white;
  border-left: 1px solid #ccc;
  color: black;
  margin-top: -2px;
}
.tab-content {
  display: none;
  padding: 10px;
}
.show {
  display: block;
}
/* 강의 복사 내용*/
```

```html
<div class="container mt-5">
  <ul class="list">
    <li class="tab-button">Products</li>
    <li class="tab-button **active**">Information</li>
    <li class="tab-button">Shipping</li>
  </ul>

  <div class="tab-content">
    <p>상품설명입니다. Product</p>
  </div>
  <div class="tab-content **show**">
    <p>상품정보입니다. Info</p>
  </div>
  <div class="tab-content">
    <p>배송정보입니다. Shipping</p>
  </div>
</div>
```

→ `show` 클래스를 부착하면 원하는 내용을 보여줄 수 있도록! `active` 클래스를 부착하면 버튼을 주황색으로 표시할 수 있도록

→ 첫번째 버튼을 누르면 첫번째 버튼 하이라이트 + 첫번째 내용 보여줄 수 있도록!

→ javscript파일 첨부 → tab.js 파일 만들기

`<script src="tab.js"></script>`

버튼 0(products)을 누르면 ..

1. 버튼0 버튼 1과 버튼2에 붙은 주황색 제거 (모든 탭 안보이게)
2. 내용0 내용1 내용2 안보이게
3. 버튼 0이 주황색으로 하이라이트 되어야함
4. 내용0이 보여야함

5. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
6. 다른 탭내용들 숨기는 기능도 추가해야함

```jsx
$(".tab-button")
  .eq(0)
  .click(function () {
    $(".tab-button").removeClass("active"); // 모두 주황색 제거
    $(".tab-content").removeClass("show"); // 모든 탭내용 제거
    $(".tab-button").eq(0).addClass("active");
    $(".tab-content").eq(0).addClass("show");
  }); // tab 3개 중에 0번째 버튼만 선택!
```

## 탭 기능 만들기: for반복문으로 코드 줄이기

우선, 버튼1, 버튼2도 똑같이 개발하기

```jsx
$(".tab-button")
  .eq(1)
  .click(function () {
    $(".tab-button").removeClass("active");
    $(".tab-content").removeClass("show");
    $(".tab-button").eq(1).addClass("active");
    $(".tab-content").eq(1).addClass("show");
  });

$(".tab-button")
  .eq(2)
  .click(function () {
    $(".tab-button").removeClass("active");
    $(".tab-content").removeClass("show");
    $(".tab-button").eq(2).addClass("active");
    $(".tab-content").eq(2).addClass("show");
  });
```

`eq(0)` 을 각각 → `eq(1)` , `eq(2)` 로 변경

→ 버튼1, 버튼2 기능 완성

but 코드가 너무 길어짐 → 확장성 있는 코드로 바꿀 수 있음

→ 반복문을 통해서

```jsx
**for (let i = 0; i < 3; i++) { // var 말고 let 써야함**
  $(".tab-button")
    .eq(i)
    .click(function () {
      $(".tab-button").removeClass("active");
      $(".tab-content").removeClass("show");
      // 1. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
      // 2. 다른 탭내용들 숨기는 기능도 추가해야함
      $(".tab-button").eq(i).addClass("active");
      $(".tab-content").eq(i).addClass("show");
    }); // tab 3개 중에 0번째 버튼만 선택!
**}**
```

`var` 대신 `let` 써야 함(존재 범위가 중괄호 내부) →

`for (let i = 0; i < 3; i++)` 대신 `for (let i = 0; i < 버튼의 개수; i++)` 로 하면 더 확장성 있는 코드가 됨

`버튼의 개수` 대신 `$('.tab-button').length` 입력

## 이벤트 버블링과 이벤트 함수

모달창에 배경을 누르면 모달창 닫히는 기능 추가

이벤트 버블링 : 이벤트가 상위요소로 퍼지는 현상

→ 이벤트리스너 달때 주의 해야함

검은배경 누르면 모달창이 닫히는 기능

```jsx
$(".black-background").click(function () {
  $(".black-background").hide(); // display:none과 유사함
});
```

→ 모달창 내 다른 요소 눌러도 모달창이 닫히는 버그 발생

`(".black-background")` 아래에 있는 요소 클릭해도 이벤트 버블링으로 `(".black-background")` 를 클릭했다고 브라우저가 인식함

이벤트리스너 안에서 쓸 수 있는 이벤트 함수 → 함수안에 파라미터 쓸 수 있음 ex) `function(e)`

```jsx
$(".black-background").click(function(e) {
        e.target; // 지금 실제로 클릭한 요소
				e.currentTarget; // 지금 이벤트리스너가 달린 곳
				$(this); // 지금 이벤트리스너가 달린 곳
				e.preventDefault(); // 기본 동작 막기
```

→ 버그 해결하기

```jsx
$(".black-background").click(function(e) {
       **if(e.target == e.currentTarget) {** **// 지금 실제로 클릭한게 검은배경일 때만**
      $(".black-background").hide(); // display:none과 유사함
       **}**
      })
```

`e.currentTarget` 은 `$(".black-background")`와 같은 의미

but, `e.currentTarget` 대신, `$(".black-background")` 사용하면 안됨

why? → `[e.target](http://e.target)` 은 JS문법이고 `$(".black-background")` 은 jQuery 문법이기 때문에

→ 이벤트 버블링으로 생기는 버그는 if, e.target등으로 대처가 가능하다

## 이벤트 버블링 응용과 Dataset

함수로 코드 깔끔하게 만들 수 있음

```jsx
for (let i = 0; i < $(".tab-button").length; i++) {
  // var 말고 let 써야함
  $(".tab-button")
    .eq(i)
    .click(function () {
      탭열기(i);
    }); // tab 3개 중에 0번째 버튼만 선택!
}
function 탭열기(숫자) {
  $(".tab-button").removeClass("active");
  $(".tab-content").removeClass("show");
  // 1. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
  // 2. 다른 탭내용들 숨기는 기능도 추가해야함
  $(".tab-button").eq(숫자).addClass("active");
  $(".tab-content").eq(숫자).addClass("show");
}
```

→ 함수 축약할 때 함수 안의 변수는 파라미터로 정의 해줌

but 반복문 말고 다른 방법으로 탭기능 만들 수 있음

이벤트리스너를 3개 사용하지 않고 탭의 상위 요소 1개에 써도 기능 구현이 가능함

→ 이벤트 리스너를 적게 사용하면 메모리 절약이 가능함

→ `<ul>` 에 이벤트리스너 달아서 탭기능 만들기

```jsx
$(".list").click(function (e) {
  if (e.target == document.querySelectorAll(".tab-button")[0]) {
    // 제이쿼리 $와 유사한 셀렉터 사용 가능, 여러개 있을 때 All
    // 0번째 타겟이 내가 클릭한것과 같은지
    탭열기(0); // 함수 숫자에 0이 기입되어 동작
  }
});
```

→ if문을 3개 써야해서 비효율적일 수도 있음

HTML에 몰래 정보심기 (일종의 테크닉)

`data-작명=”값”`

```html
<ul class="list">
  <li class="tab-button" **data-id="0" **>Products</li>
  <li class="tab-button active" **data-id="1" **>Information</li>
  <li class="tab-button" **data-id="2" **>Shipping</li>
</ul>
```

정보 꺼내려면

HTML요소.dataset.작명

→ if문 없이도 기능 구현 가능

```jsx
$(".list").click(function (e) {
  **탭열기(e.target.dataset.id)**; //(내가누른버튼에 숨겨져있던 숫자) 0버튼 누르면 0이됨
});
function 탭열기(숫자) {
  $(".tab-button").removeClass("active");
  $(".tab-content").removeClass("show");
  // 1. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
  // 2. 다른 탭내용들 숨기는 기능도 추가해야함
  $(".tab-button").eq(숫자).addClass("active");
  $(".tab-content").eq(숫자).addClass("show");
}
```

jQuery 문법으로 HTML에 몰래 정보저장하기

`$(’.list’).data(’작명’, ‘값’);`

`$(’.list’).data(’작명’);` → 저장한 정보 가져다 쓸 수 있음

호환성은 jQuery를 이용한 정보저장이 더 좋음!

## 인터렉티브 form 만들기 : input과 change 이벤트

다이나믹한 from UI 만들기

→ 부트스트랩 템플릿, jQuery 설치할 것

```html
<form class="container my-5">
  <div class="form-group">
    <p>상품선택</p>
    <select class="form-control" id="option1">
      <option>모자</option>
      <option>셔츠</option>
    </select>

    <div class="size-select">
      <p class="mt-4">사이즈선택</p>
      <select class="form-control" id="option2">
        <option>95</option>
        <option>100</option>
        <option>105</option>
      </select>
    </div>
  </div>
</form>
```

→ 셔츠를 고르면 셔츠 사이즈를 고르는 셀렉트 폼 보여주기

`<select>` → input과 유사함, 안에 `<option>` 태그 추가하면 여러가지 옵션이 보임

→ `size-select` 클래스는 셔츠 선택될 때 보여야 하니까 `display: none;` 으로 설정하기

→ input 값이 바뀔때마다 이벤트가 발동!

input 이벤트 : input 값이 바뀔때마다 발동(input에 값을 입력하기만 해도 발동)

change 이벤트 : input 값이 바뀔 때 발생 but input 값이 바뀌고 커서를 다른 곳에 찍어야 발생!

`$('select').val()` → select에 입력한 값 가져올 수 있음

ex) input창에 모자 선택하고 `$('#option').val()` → `'모자'` 출력

사용자가 ‘셔츠’ 선택하면 UI 보여주기

```jsx
$("#option1").on("change", function () {
  // select 인풋에서 셔츠라는 값을 선택하면 밑에 그 UI를 보여줌
  if ($("select").val() == "셔츠") {
    // 만약 사용자가 선택한 값이 셔츠인 경우 밑에 그 UI를 보여줌
    // if (사용자가 선택한 겂 == 셔츠) {
    $(".size-select").show(); //    그 UI를 보여줌
  }
});
```

→ 모자를 고르면 셔츠 사이즈를 고르는 select 폼 숨기기

```jsx
$('#option1').on('change', function(){  // select 인풋에서 셔츠라는 값을 선택하면 밑에 그 UI를 보여줌
        if ($('select').val() == '셔츠') { // 만약 사용자가 선택한 값이 셔츠인 경우 밑에 그 UI를 보여줌
        // if (사용자가 선택한 겂 == 셔츠) {
        $('.size-select').show();//    그 UI를 보여줌
        } **else { $('.size-select').hide(); // 모자를 선택하면 UI 숨겨줌**

        **}**
    })
```

## 인터렉티브 form 만들기 : HTML을 동적으로 생성하기

바지를 선택하면 다른 `<option>` 이 나오도록

HTML을 자바스크립트로 짜서넣기

→ 셔츠를 선택하면 `<option>` 세 개를 만들어서 집어 넣도록!

자바스크립트로 HTML 작성하기 : 문자 자료형 안에 담으면 됨

`append()` → 특정 HTML을 안에 넣어주는 jquery문법

`$('#option2').append('<div></div>');` → option2라는 id에 `<div></div>` 태그 추가

→ 변수에 담아서 동적으로 생성도 가능

```jsx
$("#option1").on("change", function () {
  if ($("#option1").val() == "셔츠") {
    // 템플릿을 만들고
    var 템플릿 = "<div></div>";
    $("#option2").append(템플릿);
  }
});
```

셔츠를 선택하면 `<option>` 세 개를 만들어서 집어넣음

```jsx
$("#option1").on("change", function () {
  if ($("#option1").val() == "셔츠") {
    // 템플릿을 만들고
    var 템플릿 = "<option>95</option><option>100</option><option>105</option>";
    $("#option2").append(템플릿);
  }
});
```

```css
.size-select {
  display: block;
}
```

→ `display: none;` 에서 `display: block;` 으로 교체

html에서 `'따옴표'` 는 엔터기가 적용안됨 → 여백인정X

→ `백틱` → 엔터키 적용됨!

```jsx
var 템플릿 = `<option>95</option>
        <option>100</option>
        <option>105</option>`;
```

바지 선택하면 바지 사이즈 태그 추가되는 기능 만들기

```jsx
$('#option1').on('change', function() {
          if( $('#option1').val() == '셔츠') { // 템플릿을 만들고
        **$('#option2').html('')// 얘안에 있는 HTML 다 지우기(input값 변경할 때마다 추가되는 버그제거)**
        var 템플릿 = `<option>95</option>
        <option>100</option>
        <option>105</option>`;
        $('#option2').append(템플릿);
        } **else if ($('#option1').val() == '바지') {
          // 템플릿을 만들고
          $('#option2').html('')// 얘안에 있는 HTML 다 지우기(input값 변경할 때마다 추가되는 버그제거)
          var 템플릿 = `<option>28</option>
          <option>30</option>
          <option>32</option>`;
          $('#option2').append(템플릿);**
            }
          })
```

## **인터랙티브 form 만들기 : forEach 반복문 사용**

`<option>` 이 매우 많으면 하드코딩 하면 코드가 너무 길어짐

for 반복문을 이용한 HTML 생성

`백틱 문자 중간에 `${변수}` 넣는 법` → 최신 JS 문법

일반 따옴표 중간에 변수넣기 : `‘문자’` + 변수 + `’문자’` but 신문법 사용하면 굳이 사용안해도 됨

```jsx
var 사이즈 = [26, 28, 30, 32, 34, 36];
      $('#option1').on('change', function() {
        if( $('#option1').val() == '바지') {
            $('#option2').html('')
        **for(var i = 0; i < 6; i++) {
      var 템플릿 = `<option>${사이즈[i]}</option>`;**
      $('#option2').append(템플릿);
        }
          }
        })
```

`array.forEach()` 로 반복하기

→ 어레이 자료 개수만큼 반복

```jsx
var 사이즈 = [26, 28, 30, 32, 34, 36];

사이즈.forEach(function (i) {
  console.log(i); //사이즈 개수만큼 반복할 코드, i는 저장된 데이터
}); // 26 28 30 32 34 36
```

```jsx
var 사이즈 = [26, 28, 30, 32, 34, 36];

$("#option1").on("change", function () {
  if ($("#option1").val() == "바지") {
    $("#option2").html("");

    사이즈.forEach(function (i) {
      var 템플릿 = `<option>${i}</option>`;
      $("#option2").append(템플릿);
    });
  }
});
```

forEach()용도

1. for 반복문보다 더 쉽게 쓸 수 있음
2. [Array] {Object} 안에 있는 자료 출력

**Arrow Function**

자바스크립트에서 콜백함수를 사용할 때 콜백함수를 조금 더 예쁜 모양으로 사용가능

```jsx
var 사이즈 = [26, 28, 30, 32, 34, 36];
사이즈.forEach(function (i) {
  console.log(i);
});

사이즈.forEach((i) => {
  console.log(i);
});
```

function이라는 키워드 대신 `=>` 라는 화살표를 이용가능

특징

1. 파라미터가 하나면 소괄호를 생략 가능

2. 함수의 중괄호 내에 **return 어쩌구~** 한줄밖에 없으면 {} 중괄호도 생략 가능.

3. function 문법 내에선 this라는 키워드의 값이 새롭게 변합니다. 하지만 arrow function의 경우 그냥 함수 바깥에 있던 this를 그대로 사용

→ 그래서 function 내에서 this값을 쓰고 싶을 때 arrow function을 쓸지 말지를 잘 생각!

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

  ## 위에서부터 등장하는 모달창 만들기

  애니메이션 만드는 방법

  1. 시작화면/최종화면 만들기
  2. 자바스크립트로 트리거 하기
  3. 스무스한 동작은 animate 함수 잘 안쓰고 CSS 속성 씀 (더 빨라서)

  → transition 이용!

  → 트리거는 자바스크립트로 하고 스무스한 동작은 transition으로!

  ```jsx
  ".btn-lg".on("click", function () {
    $(".black-background").fadeIn();
  });
  ```

  →

  ```jsx
  $(".btn-lg").on("click", function () {
    $(".black-background").show();
    $(".black-background").animate({ marginTop: "0px" }); //최종화면
  });
  ```

  ```css
  .black-background {
      background: rgba(0,0,0,0.5);
      position: fixed; /* 브라우저 화면에 딱 달라붙음 */
      z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치 */
      width: 100%;
      height: 100%;
      **display: block; /* 모달창이 보여야 하니까 none 대신 block */
      margin-top: -1200px; /* 위에 있다가 내려오도록 */**
  }
  ```

  →

  ```jsx
  $('.btn-lg').on('click', function() {
        $('.black-background')**.show().animate**({marginTop : '0px'});
      });
  ```

  → `show()` 와 `animate` 겹쳐서 사용할 수 있음!

  요즘은 animate 대신 CSS 주로 이용함!

  ```jsx
  $('.btn-lg').on('click', function() {
        $('.black-background').**css('margin-top', '0px'**); /* margin-top을 0px로*/
      });
  ```

  ```css
  .black-background {
    background: rgba(0, 0, 0, 0.5);
    position: fixed; /* 브라우저 화면에 딱 달라붙음 */
    z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치 */
    width: 100%;
    height: 100%;
    display: block;
    transition: all 3s;
    margin-top: -1000px;
  }
  ```

  프로의 애니메이션 개발 팁

  margin width position left right heght 애니메이션 금지 (건드리지 않는 것이 좋음!)

  → 동작시간이 오래걸릴 수 있음 → transform 이용!

  → margin 대신 transform 사용!

  ```jsx
  $(".btn-lg").on("click", function () {
    $(".black-background").css("transform", "translateY(0px)"); // 0px이 최종 모습
  });
  ```

  ```css
  .black-background {
    background: rgba(0, 0, 0, 0.5);
    position: fixed; /* 브라우저 화면에 딱 달라붙음 */
    z-index: 5; /* 부트스트랩은 1 ~ 4까지 이용하므로 모든요소 앞에 위치 */
    width: 100%;
    height: 100%;
    display: block;
    transition: all 3s;
    transform: translateY(-1000px); /* margin-top 대신 쓰는게 훨씬 좋음 */
  }
  ```

  가장 좋은 방법

  → CSS class를 부착하는 방향으로 시작화면/최종화면 개발

  `$('.black-background').css('transform', 'translateY(0px)');` 대신, `addClass()` 함수 사용하는 것이 더 좋음!

  → 복잡한 애니메이션 만들 때 관리가 쉬워짐

  ```jsx
  $(".btn-lg").on("click", function () {
    $(".black-background").addClass();
  });
  ```

  ```css
  .slide-down {
    transform: translateY(0px);
  }
  ```

  ## 정규식으로 이메일 형식 검증해보기

  → 문자를 검사할때 쓰는 정규식(슬래시 2개로 표현)

  `/asadqwd/` → 이 문자에 a나 b가 들어가 있나요??

  정규식으로 문자를 검사하는 법

  `/abc/.test('abcadasdw')` → 지금 `'abcadasdw'` 문자에 abc라는 글자가 있나요??

  ### 정규식 핵심 문법

  `[괄호]` → 알파벳을 표현하고 싶을때 사용함

  ex)

  `/[A-z]/.test(’s’)` → 대문자 A부터 소문자 z까지(모든 알파벳) 중 `‘s’`가 있냐?

  → `true`

  \S : 특수문자 포함 모든 문자 1개

  ex)

  `/\S/.test('#')`

  → `true`

  이메일을 표현하는 정규식

  → asdasda@dadasd.asdasd

  `/\S@\S.\S/` → 모는문자@모든문자.모든문자

  \S → 모든 문자이긴 한데 문자 하나를 뜻함

  → `\S+` → 모든 문자 하나 뒤에도 계속 찾기

  →`/\S+@\S+\.\S+/` → . 은 따로 구분 해줘야함!

  → `/\S+@\S+\.\S+/.test('dasasd@naver.com')` → `true`

  ### 이메일 input의 값이 이메일 형식이 아니면 폼 전송 X

  만약 지금 이메일 input에 입력된 값이 정규식과 비교했을때 false인 경우

  폼 전송 막기, 안내창 띄우기

  숙제 1 → 제대로된 이메일 정규식 찾아오기

  ```jsx
  var 입력한이메일 = $('#email').val()
          if (/\S+@\S+\.\S+/.test(입력한이메일) == false ) {
              e.preventDefault();
  ```

  모던 브라우저에선 `<input type="email”` 이라고 쓰면 알아서 email검사 해줌!

  → 이메일 검증이 딱히 필요하지 X

  주의점 → 다국어 이메일 주소도 존재 ex) 한글 이메일 → 유연하게 검사할 필요가 있음

  ### 정규식 테스트

  숙제2 → 패스워드 입력란에 대문자 들어 있는지 검사

  정규식이랑 동일하냐고 물어보는게 아님! 포함되어 있느냐를 물어봄!

  ex) `/abc/.test(’abcasdw’)` → `true` 로 나옴!

  꼭 `/abc/.test(’abc’)`로 표현할 필요 없음!

  `/[A-Z]+/.test('asdasdqw')` → 모든 영어 대문자가 들어가 있나요? → `false`

  ```jsx
  var 입력한패스워드 = $("#psw").val();
  if (/[A-Z]+/.test(입력한패스워드) == false) {
    // 패스워드에 대문자가 없으면 form 전송 막아주세요
    e.preventDefault();
  }
  ```

  숙제 3 → 이메일 input 공백검사와 이메일 형식 검사 둘 다 하려면??

  ```jsx
  var 입력한이메일 = $("#email").val();
  if (/\S+@\S+\.\S+/.test(입력한이메일) == false) {
    e.preventDefault();
  } else if (입력한이메일 == "") {
    // 입력한 이메일이 공백이냐
    e.preventDefault(); // 이메일 형식이 맞더라도 공백검사 추가로 진행
  }
  ```

  ## 이미지 슬라이드 UI 만들기 (Carousel)

  - 버튼을 누르면 다음 화면으로 넘어가는 슬라이드

  `100vw` → viewport width : 실제 브라우저 화면의 몇 %를 차지할지

  ```html
  <div class="slide-box" >
          <img src="img/car1.png" alt="">
        </div>
        <div class="slide-box">
          <img src="img/car2.png" alt="">
        </div>
        <div class="slide-box">
          <img src="img/car3.png" alt="">
        </div>
      </div>
  ```

  ```css
  .slide-container {
    width: 300vw;
  }
  .slide-box img {
    width: 100%;
  }
  ```

  2라는 버튼을 누르면 다음 사진 보이도록

  → 이미지 3개를 감싸는 큰 div 박스를 왼쪽으로 100vw만큼 움직이도록!

  → 버튼 2를 투르면 해당 CSS 속성 보여주기

  ```css
  .slide-container {
    width: 300vw;
    transform: translateX(-100vw);
  }
  ```

  애니메이션 구현하는 법

  1. jQuery animate()
  2. CSS transition → `transition: all 1s;`

  자바스크립트 trigger만 만들면 됨

  버튼2 누르면 `transform: translateX(-100vw);` 가 되어야 함!

  ```jsx
  $(".slide-2").click(function () {
    // on은 생략 가능
    $(".slide-container").css("transform", "translateX(-100vw");
  });
  ```

  ![스크린샷 2022-02-25 오후 7.33.49.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c7678eb2-1035-44ad-b81c-6f95da3e10da/스크린샷_2022-02-25_오후_7.33.49.png)

  UI 만드는 법

  1. 시작화면 만들기
  2. 최종화면 만들기
  3. 자바스크립트 Trigger
  4. 애니메이션 넣기

  버튼 3을 누르면 ?

  → 3번째 사진이 보이도록 → -200vw만큼 움직이도록 만들기

  ```jsx
  $(".slide-3").click(function () {
    $(".slide-container").css("transform", "translateX(-200vw");
  });
  ```

  → 버그 생길 수 있음

  페이지 늘이거나 줄였을 때 반응이 느림 → 이미지를 백그라운드 이미지 속성으로 넣으면 됨

  → `background-image: url()`

  `transition: all 1s;` 를 → `transition: transform 1s;` 로 변경하면 width 는 변경하지 않고 transform 속성만 변함 !

  숙제 → Next버튼 만들기 → 누르면 다음이미지로 넘어가기

  `position: absolute;*/* 요소 겹치거나 띄우기 */` →\* 쓰려면 부모 태그에 position relative가 필요함!

  만약에 지금 사진1이 보이면 사진2를 보여주고

  사진 2가 보이면 사진 3을 보여주고

  ```css
  .slide-next {
  position: absolute; */* 요소 겹치거나 띄우기 */*

  top: 45%;

  right: 0; */* 오른쪽으로 오게 */*

  }
  ```

  ```jsx
  var 지금보이는사진 = 1;
  $(".slide-next").click(function () {
    if (지금보이는사진 == 1) {
      $(".slide-container").css("transform", "translateX(-100vw");
      지금보이는사진 = 2; // 지금 보이는 사진이 2라고 알려줘야 함!
    } else if (지금보이는사진 == 2) {
      $(".slide-container").css("transform", "translateX(-200vw");
      지금보이는사진 = 3;
    }
  });
  ```

  ### 확장성있는 코드로 다시 개발(사진이 무수히 많아지면 그 때마다 if문을 사용할 수는 없음)

  `-100vw`, `-200vw` 대신, `-지금보이는사진00vw`

  텍스트 더하기 → ‘글자' + ‘글자’ = ‘글자글자’

  ```jsx
  var 지금보이는사진 = 1;
      $('.slide-next'). click(function() {

      **$('.slide-container').css('transform', 'translateX(-'+ 지금보이는사진 +'00vw)');
      지금보이는사진 = 지금보이는사진 + 1;**
  ```

  → if문 필요없이 작성이 가능!

  → Next 버튼이 끝없이 동작중

  지금 보이는 사진이 3이면 Next 버튼 기능제한

  ## 함수의 return 문법 & 소수점 다루기

  function 문법

  1. 긴코드 축약해서 쓸 수 있음
  2. 파라미터 추가 가능
  3. return → 함수 쓰고 그 자리에 뭔가 뱉고 싶을때 사용(반환)

  ```jsx
  function 함수() {
    return 123; // 함수쓰고 123을 뱉어라
  }
  var 변수 = 함수(); // 함수에 123 저장
  console.log(변수); //123
  ```

  return은 함수 종료 기능도 가지고 있음 → return 밑에 있는 코드는 실행X

  return 용도 → 자료를 넣으면 다른 자료가 나오는 변환기 만들고 싶을때 사용

  ex) 가격이 60000원 일때 부가세 계산할 때

  상품이 1개 일때

  ```jsx
  console.log(60000 * 0.1);
  ```

  but 상품이 많아질때 → 부가세 계산기 만드는게 편리함

  ```jsx
  console.log(vat(50000));

  function vat(a) {
    return a * 0.1;
  }
  vat(50000);
  ```

  자바스크립트에서 소수점과 같이 연산할 때 주의점

  → 1.1 곱하니까 작은 오차가 발생함 why? 컴퓨터는 2진법으로 바꿔서 연산하기 때문에

  → 정확한 연산을 하고 싶으면 라이브러리를 쓰던가 반올림하면 됨

  ```jsx
  console.log(vat(55555)); // 61110.50

  function vat(a) {
    var num = (a * 1.1).toFixed(2); // 2째자리 지 반올림
    return parseInt(num); // 문자가 숫자로 바뀜
  }
  ```

  `toFixed` 는 문자로 변환됨 → 버그 생길 수 있음 → 숫자연산이 숫자와 문자의 연산으로 인식됨

  `parseFloat` 또는 `parseInt` 사용

  ## 스크롤 애니메이션

  → 스크롤 시 변하는 Navbar 만들기

  → 스크롤 내리면 로고의 폰트가 줄어드는 애니메이션

  스크롤 기반 애니메이션 → 나중에 용도가 많음!

  ![https://codingapple.com/wp-content/uploads/2019/09/navanimation.gif](https://codingapple.com/wp-content/uploads/2019/09/navanimation.gif)

  → jQuery 필요함

  navbar가 초기에 투명하다가 스크롤 내리면 검정색으로 변함

  UI 애니매이션 만드는 법

  1. 시작화면 제작 : 투명한 navbar
  2. 최종화면 제작
  3. 자바스크립트로 트리거

  4. 시작화면 제작 : 투명한 navbar

  ```css
  .nav-menu {
      display: flex;
      justify-content: space-between;
      align-items: center;
      **background-color: transparent;
      position: fixed;/* fixed를 줘야 스크롤 돼도 nav가 보임*/
      z-inedx: 5;
      width: 100%;
  }**
  ```

  1. 스크롤바를 내리면 불투명 navbar

  `스크롤바를 내리면 .nav-menu이 background: black;`

  `window` → viewport

  ```jsx
  /* 스크롤바를 내리면 
        .nav-menu이 background: black; */

  $(window).on("scroll", function () {
    $(".nav-menu").css("background", "black"); // 대신 클래스를 부착하는 addClass()를 쓰면 더 좋음
  }); // viewport가 scroll되었을 때 코드를 실행해 주세요
  ```

  ```html
  <div class="nav-menu nav-scroll"></div>
  ```

  → `nav-scroll` 이라는 새로운 class를 만듦(최종화면을 만들어 주는 class)

  ```jsx
  $(window).on("scroll", function () {
    $(".nav-menu").addClass("nav-scroll"); // 스크롤하면 nav-menu클래스에 nav-scroll클래스를 붙여 주세요
  }); // viewport가 scroll되었을 때 코드를 실행해 주세요
  ```

  스크롤을 어느정도 내렸을 때 동작하게 하려면?

  but 우리는 스크롤 내리자마자 동작

  → 스크롤 `요만큼` 내리면 동작하도록

  → 스크롤바를 100px 내렸을 때 동작하게 하려면?

  → 만약에 지금 스크롤을 100px 했을 때

  `$(window).scrollTop()` → 스크롤된 높이(px)를 알려주는 제이쿼리 함수

  ```jsx
  $(window).on("scroll", function () {
    if ($(window).scrollTop() > 100) {
      // 만약에 지금 스크롤을 100px 했을 때
      $(".nav-menu").addClass("nav-scroll"); // 스크롤하면 nav-menu클래스에 nav-scroll클래스를 붙여 주세요
    }
  }); // viewport가 scroll되었을 때 코드를 실행해 주세요
  ```

  숙제 1 : 스크롤 내리면 폰트사이즈 서서히 작아지게

  scroll 이벤트 리스너 많이쓰면 안됨 → 스크롤 내릴때마다 코드 실행해야 해서 버벅일 수 있음

  h1태그에 클래스 주기

  ```jsx
  <div class="nav-menu">
        <h1 **class="nav-logo"**>Shirts Studio</h1>
        <a id="nav-sub-btn">Products</a>
  ```

  최종화면에서 폰트사이즈 줄이기

  ```css
  .scroll-nav-logo {
    font-size: 30px;
  }
  .nav-menu h1 {
    /* h1 태그에 적용해야 스크롤 올릴때도 애니메이션 적용됨*/
    transition: all 1s;
  }
  ```

  자바스크립트 트리거

  ```jsx
  $(window).on('scroll', function() {
          if ($(window).scrollTop() > 100) { // 만약에 지금 스크롤을 100px 했을 때
        $('.nav-menu').addClass('nav-scroll') // 스크롤하면 nav-menu클래스에 nav-scroll클래스를 붙여 주세요
        **$('.nav-menu h1').addClass('scroll-nav-logo')**  }
      }) // viewport가 scroll되었을 때 코드를 실행해 주세요
  ```

  숙제 2 : 다시 스크롤 올리면 원상태로! (애니메이션 제거)

  기존 작성했던 코드는

  스크롤바를 100px이상 내렸을 경우 애니메이션을 동작

  → `else` 문을 사용해서 100px 미만일 경우 원상태로 되돌릴 코드를 추가

  ## 탭 기능 만들기

  → 탭의 html, css는 강의 하단에 첨부

  → 탭으로 탭 기능 만들기

  → 버튼 누르면 주황색 하이라이트 되도록 디자인 + 해당 탭의 내용이 보이도록

  UI 만드는법

  ```css
  /* 강의 복사 내용*/
  ul.list {
    list-style-type: none;
    margin: 0;
    padding: 0;
    border-bottom: 1px solid #ccc;
  }
  ul.list::after {
    content: "";
    display: block;
    clear: both;
  }
  .tab-button {
    display: block;
    padding: 10px 20px 10px 20px;
    float: left;
    margin-right: -1px;
    margin-bottom: -1px;
    color: grey;
    text-decoration: none;
    cursor: pointer;
  }
  .active {
    border-top: 2px solid orange;
    border-right: 1px solid #ccc;
    border-bottom: 1px solid white;
    border-left: 1px solid #ccc;
    color: black;
    margin-top: -2px;
  }
  .tab-content {
    display: none;
    padding: 10px;
  }
  .show {
    display: block;
  }
  /* 강의 복사 내용*/
  ```

  ```html
  <div class="container mt-5">
    <ul class="list">
      <li class="tab-button">Products</li>
      <li class="tab-button **active**">Information</li>
      <li class="tab-button">Shipping</li>
    </ul>

    <div class="tab-content">
      <p>상품설명입니다. Product</p>
    </div>
    <div class="tab-content **show**">
      <p>상품정보입니다. Info</p>
    </div>
    <div class="tab-content">
      <p>배송정보입니다. Shipping</p>
    </div>
  </div>
  ```

  → `show` 클래스를 부착하면 원하는 내용을 보여줄 수 있도록! `active` 클래스를 부착하면 버튼을 주황색으로 표시할 수 있도록

  → 첫번째 버튼을 누르면 첫번째 버튼 하이라이트 + 첫번째 내용 보여줄 수 있도록!

  → javscript파일 첨부 → tab.js 파일 만들기

  `<script src="tab.js"></script>`

  버튼 0(products)을 누르면 ..

  1. 버튼0 버튼 1과 버튼2에 붙은 주황색 제거 (모든 탭 안보이게)
  2. 내용0 내용1 내용2 안보이게
  3. 버튼 0이 주황색으로 하이라이트 되어야함
  4. 내용0이 보여야함

  5. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
  6. 다른 탭내용들 숨기는 기능도 추가해야함

  ```jsx
  $(".tab-button")
    .eq(0)
    .click(function () {
      $(".tab-button").removeClass("active"); // 모두 주황색 제거
      $(".tab-content").removeClass("show"); // 모든 탭내용 제거
      $(".tab-button").eq(0).addClass("active");
      $(".tab-content").eq(0).addClass("show");
    }); // tab 3개 중에 0번째 버튼만 선택!
  ```

  ## 탭 기능 만들기: for반복문으로 코드 줄이기

  우선, 버튼1, 버튼2도 똑같이 개발하기

  ```jsx
  $(".tab-button")
    .eq(1)
    .click(function () {
      $(".tab-button").removeClass("active");
      $(".tab-content").removeClass("show");
      $(".tab-button").eq(1).addClass("active");
      $(".tab-content").eq(1).addClass("show");
    });

  $(".tab-button")
    .eq(2)
    .click(function () {
      $(".tab-button").removeClass("active");
      $(".tab-content").removeClass("show");
      $(".tab-button").eq(2).addClass("active");
      $(".tab-content").eq(2).addClass("show");
    });
  ```

  `eq(0)` 을 각각 → `eq(1)` , `eq(2)` 로 변경

  ![스크린샷 2022-02-26 오후 5.57.09.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5f0f3756-99fe-4663-8ef1-dce35134497e/스크린샷_2022-02-26_오후_5.57.09.png)

  ![스크린샷 2022-02-26 오후 5.57.17.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9fefb7f6-2f87-4c54-ae89-f223e264d47b/스크린샷_2022-02-26_오후_5.57.17.png)

  → 버튼1, 버튼2 기능 완성

  but 코드가 너무 길어짐 → 확장성 있는 코드로 바꿀 수 있음

  → 반복문을 통해서

  ```jsx
  **for (let i = 0; i < 3; i++) { // var 말고 let 써야함**
    $(".tab-button")
      .eq(i)
      .click(function () {
        $(".tab-button").removeClass("active");
        $(".tab-content").removeClass("show");
        // 1. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
        // 2. 다른 탭내용들 숨기는 기능도 추가해야함
        $(".tab-button").eq(i).addClass("active");
        $(".tab-content").eq(i).addClass("show");
      }); // tab 3개 중에 0번째 버튼만 선택!
  **}**
  ```

  `var` 대신 `let` 써야 함(존재 범위가 중괄호 내부) →

  `for (let i = 0; i < 3; i++)` 대신 `for (let i = 0; i < 버튼의 개수; i++)` 로 하면 더 확장성 있는 코드가 됨

  `버튼의 개수` 대신 `$('.tab-button').length` 입력

  ## 이벤트 버블링과 이벤트 함수

  모달창에 배경을 누르면 모달창 닫히는 기능 추가

  이벤트 버블링 : 이벤트가 상위요소로 퍼지는 현상

  → 이벤트리스너 달때 주의 해야함

  검은배경 누르면 모달창이 닫히는 기능

  ```jsx
  $(".black-background").click(function () {
    $(".black-background").hide(); // display:none과 유사함
  });
  ```

  → 모달창 내 다른 요소 눌러도 모달창이 닫히는 버그 발생

  `(".black-background")` 아래에 있는 요소 클릭해도 이벤트 버블링으로 `(".black-background")` 를 클릭했다고 브라우저가 인식함

  이벤트리스너 안에서 쓸 수 있는 이벤트 함수 → 함수안에 파라미터 쓸 수 있음 ex) `function(e)`

  ```jsx
  $(".black-background").click(function(e) {
          e.target; // 지금 실제로 클릭한 요소
  				e.currentTarget; // 지금 이벤트리스너가 달린 곳
  				$(this); // 지금 이벤트리스너가 달린 곳
  				e.preventDefault(); // 기본 동작 막기
  ```

  → 버그 해결하기

  ```jsx
  $(".black-background").click(function(e) {
         **if(e.target == e.currentTarget) {** **// 지금 실제로 클릭한게 검은배경일 때만**
        $(".black-background").hide(); // display:none과 유사함
         **}**
        })
  ```

  `e.currentTarget` 은 `$(".black-background")`와 같은 의미

  but, `e.currentTarget` 대신, `$(".black-background")` 사용하면 안됨

  why? → `[e.target](http://e.target)` 은 JS문법이고 `$(".black-background")` 은 jQuery 문법이기 때문에

  → 이벤트 버블링으로 생기는 버그는 if, e.target등으로 대처가 가능하다.

  ## 이벤트 버블링 응용과 Dataset

  함수로 코드 깔끔하게 만들 수 있음

  ```jsx
  for (let i = 0; i < $(".tab-button").length; i++) {
    // var 말고 let 써야함
    $(".tab-button")
      .eq(i)
      .click(function () {
        탭열기(i);
      }); // tab 3개 중에 0번째 버튼만 선택!
  }
  function 탭열기(숫자) {
    $(".tab-button").removeClass("active");
    $(".tab-content").removeClass("show");
    // 1. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
    // 2. 다른 탭내용들 숨기는 기능도 추가해야함
    $(".tab-button").eq(숫자).addClass("active");
    $(".tab-content").eq(숫자).addClass("show");
  }
  ```

  → 함수 축약할 때 함수 안의 변수는 파라미터로 정의 해줌

  but 반복문 말고 다른 방법으로 탭기능 만들 수 있음

  이벤트리스너를 3개 사용하지 않고 탭의 상위 요소 1개에 써도 기능 구현이 가능함

  → 이벤트 리스너를 적게 사용하면 메모리 절약이 가능함

  → `<ul>` 에 이벤트리스너 달아서 탭기능 만들기

  ```jsx
  $(".list").click(function (e) {
    if (e.target == document.querySelectorAll(".tab-button")[0]) {
      // 제이쿼리 $와 유사한 셀렉터 사용 가능, 여러개 있을 때 All
      // 0번째 타겟이 내가 클릭한것과 같은지
      탭열기(0); // 함수 숫자에 0이 기입되어 동작
    }
  });
  ```

  → if문을 3개 써야해서 비효율적일 수도 있음

  HTML에 몰래 정보심기 (일종의 테크닉)

  `data-작명=”값”`

  ```html
  <ul class="list">
    <li class="tab-button" **data-id="0" **>Products</li>
    <li class="tab-button active" **data-id="1" **>Information</li>
    <li class="tab-button" **data-id="2" **>Shipping</li>
  </ul>
  ```

  정보 꺼내려면

  HTML요소.dataset.작명

  → if문 없이도 기능 구현 가능

  ```jsx
  $(".list").click(function (e) {
    **탭열기(e.target.dataset.id)**; //(내가 누른 버튼에 숨겨져있던 숫자) 0버튼 누르면 0이됨
  });
  function 탭열기(숫자) {
    $(".tab-button").removeClass("active");
    $(".tab-content").removeClass("show");
    // 1. 다른 버튼에 붙은 주황색 제거하는 기능 추가해야함
    // 2. 다른 탭내용들 숨기는 기능도 추가해야함
    $(".tab-button").eq(숫자).addClass("active");
    $(".tab-content").eq(숫자).addClass("show");
  }
  ```

  jQuery 문법으로 HTML에 몰래 정보저장하기

  `$(’.list’).data(’작명’, ‘값’);`

  `$(’.list’).data(’작명’);` → 저장한 정보 가져다 쓸 수 있음

  호환성은 jQuery를 이용한 정보저장이 더 좋음!

  # level 3

  ## Array와 Object 자료형 기초

  자료형 정리

  문자, 숫자, array, object

  array, object → 여러가지 자료를 한곳에 저장하고 싶을 때

  array → [대괄호]로 생성, 자료들은 콤마로 구분

  object → {중괄호}로 생성, 자료들은 콤마로 구분, 자료 왼쪽에 이름을 써야함, key와 value로 형성됨

  ```jsx
  var 어레이 = ["BMW", "520"];
  console.log(어레이);
  ```

  array 내의 상품 데이터를 꺼내 HTML에 넣어보자(데이터 바인딩)

  자바스크립트를 활용해서 `상품제목` 에 `BMW` 가 뜨도록, `상품내용` 에 `520` 이 뜨도록

  →

  ```html
  <h4 id="title">상품제목</h4>
  <p id="text">상품내용</p>
  ```

  ```jsx
  var 어레이 = ["BMW", 520];
  console.log(어레이); // ["BMW", "520"]
  console.log(어레이[0]); // BMW

  var 오브젝트 = { brand: "BMW", model: 520 };
  console.log(오브젝트.brand); // 오브젝트에서 원하는 자료 뽑을 수 있음(키값)
  document.getElementById("title").innerHTML = 어레이[0]; // JS 문법
  $("#title").html(어레이[0]); // Jquery문법
  document.getElementById("text").innerHTML = 어레이[1];
  $("#text").html(어레이[1]);
  ```

  →

  → 오브젝트로도 데이터 바인딩 가능

  but, index대신 이름을 불러서 자료를 뽑음

  ```jsx
  $("#text").html(**오브젝트.model);**
  ```

  복잡한 데이터가 출현할 때

  상품내용을 `자료` 라는 변수에 저장된 `520`이란 데이터를 뽑아서 데이터 바인딩

  ```jsx
  var 자료 = [{ brand: "BMW" }, { model: **520** }];
  $("#text").**html(자료[1].model**);
  ```

  ## 인터렉티브 form 만들기 : input과 change 이벤트

  다이나믹한 from UI 만들기

  → 부트스트랩 템플릿, jQuery 설치할 것

  ```html
  <form class="container my-5">
    <div class="form-group">
      <p>상품선택</p>
      <select class="form-control" id="option1">
        <option>모자</option>
        <option>셔츠</option>
      </select>

      <div class="size-select">
        <p class="mt-4">사이즈선택</p>
        <select class="form-control" id="option2">
          <option>95</option>
          <option>100</option>
          <option>105</option>
        </select>
      </div>
    </div>
  </form>
  ```

  → 셔츠를 고르면 셔츠 사이즈를 고르는 셀렉트 폼 보여주기

  `<select>` → input과 유사함, 안에 `<option>` 태그 추가하면 여러가지 옵션이 보임

  → `size-select` 클래스는 셔츠 선택될 때 보여야 하니까 `display: none;` 으로 설정하기

  → input 값이 바뀔때마다 이벤트가 발동!

  input 이벤트 : input 값이 바뀔때마다 발동(input에 값을 입력하기만 해도 발동)

  change 이벤트 : input 값이 바뀔 때 발생 but input 값이 바뀌고 커서를 다른 곳에 찍어야 발생!

  `$('select').val()` → select에 입력한 값 가져올 수 있음

  ex) input창에 모자 선택하고 `$('#option').val()` → `'모자'` 출력

  사용자가 ‘셔츠’ 선택하면 UI 보여주기

  ```jsx
  $("#option1").on("change", function () {
    // select 인풋에서 셔츠라는 값을 선택하면 밑에 그 UI를 보여줌
    if ($("select").val() == "셔츠") {
      // 만약 사용자가 선택한 값이 셔츠인 경우 밑에 그 UI를 보여줌
      // if (사용자가 선택한 겂 == 셔츠) {
      $(".size-select").show(); //    그 UI를 보여줌
    }
  });
  ```

  → 모자를 고르면 셔츠 사이즈를 고르는 select 폼 숨기기

  ```jsx
  $('#option1').on('change', function(){  // select 인풋에서 셔츠라는 값을 선택하면 밑에 그 UI를 보여줌
          if ($('select').val() == '셔츠') { // 만약 사용자가 선택한 값이 셔츠인 경우 밑에 그 UI를 보여줌
          // if (사용자가 선택한 겂 == 셔츠) {
          $('.size-select').show();//    그 UI를 보여줌
          } **else { $('.size-select').hide(); // 모자를 선택하면 UI 숨겨줌**

          **}**
      })
  ```

  ## 인터렉티브 form 만들기 : HTML을 동적으로 생성하기

  바지를 선택하면 다른 `<option>` 이 나오도록

  HTML을 자바스크립트로 짜서넣기

  → 셔츠를 선택하면 `<option>` 세 개를 만들어서 집어 넣도록!

  자바스크립트로 HTML 작성하기 : 문자 자료형 안에 담으면 됨

  `append()` → 특정 HTML을 안에 넣어주는 jquery문법

  `$('#option2').append('<div></div>');` → option2라는 id에 `<div></div>` 태그 추가

  → 변수에 담아서 동적으로 생성도 가능

  ```jsx
  $("#option1").on("change", function () {
    if ($("#option1").val() == "셔츠") {
      // 템플릿을 만들고
      var 템플릿 = "<div></div>";
      $("#option2").append(템플릿);
    }
  });
  ```

  셔츠를 선택하면 `<option>` 세 개를 만들어서 집어넣음

  ```jsx
  $("#option1").on("change", function () {
    if ($("#option1").val() == "셔츠") {
      // 템플릿을 만들고
      var 템플릿 =
        "<option>95</option><option>100</option><option>105</option>";
      $("#option2").append(템플릿);
    }
  });
  ```

  ```css
  .size-select {
    display: block;
  }
  ```

  → `display: none;` 에서 `display: block;` 으로 교체

  ![스크린샷 2022-02-28 오후 3.22.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a890d34-fb68-48b5-a91a-8fc8878cb98b/스크린샷_2022-02-28_오후_3.22.23.png)

  html에서 `'따옴표'` 는 엔터기가 적용안됨 → 여백인정X

  → `백틱` → 엔터키 적용됨!

  ```jsx
  var 템플릿 = `<option>95</option>
          <option>100</option>
          <option>105</option>`;
  ```

  바지 선택하면 바지 사이즈 태그 추가되는 기능 만들기

  ```jsx
  $('#option1').on('change', function() {
            if( $('#option1').val() == '셔츠') { // 템플릿을 만들고
          **$('#option2').html('')// 얘안에 있는 HTML 다 지우기(input값 변경할 때마다 추가되는 버그제거)**
          var 템플릿 = `<option>95</option>
          <option>100</option>
          <option>105</option>`;
          $('#option2').append(템플릿);
          } **else if ($('#option1').val() == '바지') {
            // 템플릿을 만들고
            $('#option2').html('')// 얘안에 있는 HTML 다 지우기(input값 변경할 때마다 추가되는 버그제거)
            var 템플릿 = `<option>28</option>
            <option>30</option>
            <option>32</option>`;
            $('#option2').append(템플릿);**
              }
            })
  ```

  ## **인터랙티브 form 만들기 : forEach 반복문 사용**

  `<option>` 이 매우 많으면 하드코딩 하면 코드가 너무 길어짐

  for 반복문을 이용한 HTML 생성

  `백틱 문자 중간에 `${변수}` 넣는 법` → 최신 JS 문법

  일반 따옴표 중간에 변수넣기 : `‘문자’` + 변수 + `’문자’` but 신문법 사용하면 굳이 사용안해도 됨

  ```jsx
  var 사이즈 = [26, 28, 30, 32, 34, 36];
        $('#option1').on('change', function() {
          if( $('#option1').val() == '바지') {
              $('#option2').html('')
          **for(var i = 0; i < 6; i++) {
        var 템플릿 = `<option>${사이즈[i]}</option>`;**
        $('#option2').append(템플릿);
          }
            }
          })
  ```

  `array.forEach()` 로 반복하기

  → 어레이 자료 개수만큼 반복

  ```jsx
  var 사이즈 = [26, 28, 30, 32, 34, 36];

  사이즈.forEach(function (i) {
    console.log(i); //사이즈 개수만큼 반복할 코드, i는 저장된 데이터
  }); // 26 28 30 32 34 36
  ```

  ```jsx
  var 사이즈 = [26, 28, 30, 32, 34, 36];

  $("#option1").on("change", function () {
    if ($("#option1").val() == "바지") {
      $("#option2").html("");

      사이즈.forEach(function (i) {
        var 템플릿 = `<option>${i}</option>`;
        $("#option2").append(템플릿);
      });
    }
  });
  ```

  forEach()용도

  1. for 반복문보다 더 쉽게 쓸 수 있음
  2. [Array] {Object} 안에 있는 자료 출력

  **Arrow Function**

  자바스크립트에서 콜백함수를 사용할 때 콜백함수를 조금 더 예쁜 모양으로 사용가능

  ```jsx
  var 사이즈 = [26, 28, 30, 32, 34, 36];
  사이즈.forEach(function (i) {
    console.log(i);
  });

  사이즈.forEach((i) => {
    console.log(i);
  });
  ```

  function이라는 키워드 대신 `=>` 라는 화살표를 이용가능

  특징

  1. 파라미터가 하나면 소괄호를 생략 가능

  2. 함수의 중괄호 내에 **return 어쩌구~** 한줄밖에 없으면 {} 중괄호도 생략 가능.

  3. function 문법 내에선 this라는 키워드의 값이 새롭게 변합니다. 하지만 arrow function의 경우 그냥 함수 바깥에 있던 this를 그대로 사용

  → 그래서 function 내에서 this 값을 쓰고 싶을 때 arrow function을 쓸지 말지를 잘 생각!

  ## 쇼핑몰 상품진열 기능 만들기

  카드형식 레이아웃

  웹 개발 방식

  1. 서버가 HTML 파일 완성해서 유저에게 보내는 방식
  2. 서버가 빈 HTML파일 + 데이터 보냄 → 그 후 JS를 이용해서 채워넣기

  서버에서 데이터 가져오는 법은 Ajax 배우면 가능

  서버가 보낸 쇼핑몰 상품데이터

  ```jsx
  <script>
          var products = [
            { id : 0, price : 70000, title : 'Blossom Dress' },
            { id : 1, price : 50000, title : 'Springfield Shirt' },
            { id : 2, price : 60000, title : 'Black Monastery' }
          ]
        </script>
  ```

  → var products = `[{}, {}, {}]` 형태

  → array 자료형인데 object가 3개 들어있는 array

  ```jsx
  $(".title").eq(0).html(products[0].title);
  $(".title").eq(1).html(products[1].title);
  $(".title").eq(2).html(products[2].title);

  $(".price")
    .eq(0)
    .html("가격 : " + products[0].price);
  $(".price")
    .eq(1)
    .html("가격 : " + products[1].price);
  $(".price")
    .eq(2)
    .html("가격 : " + products[2].price);
  ```

  가격순 정렬 버튼 만들기

  array 정렬할 때 `sort()`

  ```jsx
  var 어레이 = [7, 3, 5, 2];
  어레이.sort(); // [2, 3, 5, 7]
  ```

  array 가나다순 정렬할 땐 sort() → sort()는 문자 정렬

  ```jsx
  var 어레이 = [7, 3, 5, 2, 40];
  어레이.sort(); // [2, 3, **40**, 5, 7], 숫자정렬X
  ```

  sort()로 숫자 정렬 할 때

  ```jsx
  var 어레이 = [7, 3, 5, 2, 40]
         어레이.sort(function(a,b){
             **return a - b**
         }) // [2, 3, 5, 7, 40]
  ```

  → 이해하지말고 암기 할 것

  1. a, b는 array 안의 데이터들
  2. 양수를 return 하면 a를 오른쪽, b를 왼쪽으로
  3. 음수를 return 하면 b를 오른쪽, a를 왼쪽으로

  내림차순 정렬은 ?

  ```jsx
  var 어레이 = [7, 3, 5, 2, 40]
         어레이.sort(function(a,b){
             **return b - a**
         })
  // [40, 7, 5, 3, 2]
  ```

  abc 순이 아니라 cba 순으로 구현

  → 문자는 부등호 비교 가능 ‘ㄱ’ < ‘ㄴ’

  products라는 array 가격순 정렬

  a, b는 각각 {},{},{} 하나하나의 object임

  → return a - b하면 {}-{} 형태임 → a.price - b.price

  ```jsx
  $("#sortPrice").click(function () {
    products.sort(function (a, b) {
      return a.price - b.price;
    });
  });
  ```

  → 가격순으로 정렬됨

  but 화면은 그대로 (코드를 짜주지 않았기 때문에)

→ sort 함수 아래에 기존 코드릴 넣어주면 됨

→ 버튼 누르면 producs가 정렬되고 그다음에 데이터바인딩 해주세요

```jsx
$("#sortPrice").click(function () {
  products.sort(function (a, b) {
    return a.price - b.price;
  });
  $(".title").eq(0).html(products[0].title);
  $(".title").eq(1).html(products[1].title);
  $(".title").eq(2).html(products[2].title);

  $(".price")
    .eq(0)
    .html("가격 : " + products[0].price);
  $(".price")
    .eq(1)
    .html("가격 : " + products[1].price);
  $(".price")
    .eq(2)
    .html("가격 : " + products[2].price);
});
```

→ 버튼 누르면 가격순으로 정렬!

map, filter

array 자료에 필터 기능 주고 싶을 때

ex) `var 어레이 = [7, 3, 5, 2, 40]` 에서 2, 3, 5 만 뽑고 싶을 때

```jsx
var 어레이 = [7, 3, 5, 2, 40];
어레이.filter(function (a) {
  return 조건식;
});
```

→ 조건식에 맞는 데이터만 걸러줌

`filter()` 는 기존 array 자료를 변형 X → 새로운 변수에 담아써야 함

`sort()` 는 기존 array 자료를 변형 O

```jsx
var 어레이 = [7, 3, 5, 2, 40]
       **var 뉴어레이 = 어레이.filter(function(a**){
           return a < 4
```

→ 쇼핑몰 만들 때 가격 필터 주고 싶을 때 사용

5만원 이하의 상품만 필터링 하려면

버튼 누르면 products 자료에서 5만원 이하만 남기면 됨

map

`map()` → array 자료에 전부 뭐 해줘서 새로운 어레이를 만들고 싶을 때

```jsx
var 어레이 = [7, 3, 5, 2, 40];
var 뉴어레이 = 어레이.map(function (a) {
  return a * 2; // 2씩 곱해짐
});
```

→ 달러화로 가격 변경할 때 사용 (달러 곱해줌)

숙제 1. 가나다순 정렬버튼 & 기능제작

숙제 2. 5만원이하 필터버튼 & 기능제작

1. 우선 상품 목록 다 비워두고
2. 버튼 누르면 products에서 5만원 이하 상품만 남김
3. products array 개수만큼 HTML 동적 생성

```jsx
$('#abc').click(function() {
        products.sort(function(a,b) {
        **if (a.title < b.title == true)** { // a.title - b.title 은 불가 ! → 문자열의 차는 불가능하기 때문에
            return -1 // 음수를 return 하면 b를 오른쪽, a를 왼쪽으로
        } else {
            return 1 // 양수를 return 하면 a를 오른쪽, b를 왼쪽으로
        }
        })
    $('.title').eq(0).html(products[0].title)
    $('.title').eq(1).html(products[1].title)
    $('.title').eq(2).html(products[2].title)

    $('.price').eq(0).html('가격 : '  + products[0].price)
    $('.price').eq(1).html('가격 : '  + products[1].price)
    $('.price').eq(2).html('가격 : '  + products[2].price)
    }) // products 라는 array가 정렬됨
```

→ 자주 쓰는 코드는 함수화하면 편함

`가나다순` 버튼 누르면 정렬됨

6만원 이하 상품 필터 기능 만들기

products 안의 데이터 개수 만큼 HTML을 생성하기 → 확장성 있음!

1. 버튼 누르면 product를 필터함 → `[{},{}]` → 6만원 이하 상품 2개만 남음!
2. products 개수만큼 HTML 생성

```jsx
"#filter".click(function () {
  var newProducs = products.filter(function (a) {
    return a.price <= 60000;
  });
  newProducs.forEach(function (a) {
    // 데이터 개수만큼 특정 코드 실행, a는 newProducs의 하나하나의 데이터
    var template = `<div>상품<div>`;
    $(".card-group").append(template);
  });
});
```

→ 상품 2개 나옴( 6만원 이하의 상품이 2개니까)

→ `<div>상품<div>` 대신 실제 레이아웃 복붙하면 완성됨

→ 기존에 상품 3개 보이는 건 지우면 됨

var template = `<div>${a.title} ${a.price} <div>`; → 실제 상품명과 가격이 나옴

응용1. 사이트 처음 접속시 상품 3개 띄우려면?

응용2. 필터버튼 말고 <input>은 ?

응용3. 원래대로 버튼

`sort()` → 원본이 변형됨, 한번 하면 되돌릴 수가 없음

→ products 사본을 하나 더 만들어두면 원본 보존이 가능!

### array 자료 사본 만들 때 주의점

```jsx
var 어레이 = [1, 2, 3];
var 어레이2 = 어레이;
```

→ 이렇게 복사하면 따로 사본하는게 아니라 값을 공유함 → 어레이를 수정하면 어레이2도 변경됨

```jsx
var 어레이 = [1, 2, 3];
var 어레이2 = [...어레이];
```

→ 값 공유 안되는 별개의 사본 생성 가능

## Ajax 요청하기

→ 서버에 데이터를 요청해서 받아 오는데 새로고침 없이 받아오기

서버 : 접속자가 요청을 하면 데이터를 갖다줌

GET : URL을 입력해서 페이지/자료 요청함 ex) 네이버에서 검색하면 해당 내용을 보여줌

POST : 내용을 숨겨서 정보를 보여주거나 요청함 ex) 로그인

AJAX : 서버에다가 GET/POST 요청을 할 수 있게 도와주는데 새로고침없이 요청할 수 있음

AJAX 요청하는 법 → jQuery로 요청

```jsx
$.ajax({
  url: "https://codingapple1.github.io/hello.txt",
  type: "GET", // 위 주소에 GET 요청을 해서 보내주는 데이터를 가져와라
}).done(function (데이터) {
  // ajax 요청이 성공했을 때 실행 시켜주는 홤수
  console.log(데이터); // GET 요청으로 받아온 데이터
});
```

→ 새로고침하면 해당 데이터 가져옴

숙제

버튼 누르면 해당 URL로 Ajax요청을 해서 받아온 글자로 바꾸기

```jsx
$(".btn-danger").click(function () {
  $.ajax({
    url: "https://codingapple1.github.io/hello.txt",
    type: "GET", // 위 주소에 GET 요청을 해서 보내주는 데이터를 가져와라
  }).done(function (데이터) {
    // ajax 요청이 성공했을 때 실행 시켜주는 홤수
    $("#hello").html(데이터);
  });
});
```

버튼 누르면 Ajax 데이터로 변경

→

상품 더보기 기능도 Ajax를 쓰면 새로고침 없이 가능

새로고침 없이 데이터가 표시된다 → Ajax 사용

`fail()` 함수 붙이기 (ajax 실패시 실행할 코드)

`always()` 함수 붙이기(ajax 요청시 항상 실행할 코드) ex) 로딩중입니다..

ex)

```jsx
$.ajax({
        url : 'https://codingapple1.github.io/hello.txt',
        type : 'GET' // 위 주소에 GET 요청을 해서 보내주는 데이터를 가져와라
    }).done(function(데이터){ // ajax 요청이 성공했을 때 실행 시켜주는 홤수
        $('#hello').html(데이터)
    })**.fail(function()**{

    })**.always(function()** {})
```

Ajax 요청으로 상품 불러오기

→ 어떤 서버에 요청해서 상품제목, 성명, 가격, 이미지 경로 .. 받아와서 데이터 바인딩

object는 점을 찍어 자료를 출력함

```jsx
$(".btn-danger").click(function () {
  $.ajax({
    url: "https://codingapple1.github.io/data.json",
    type: "GET", // 위 주소에 GET 요청을 해서 보내주는 데이터를 가져와라
  }).done(function (데이터) {
    // ajax 요청이 성공했을 때 실행 시켜주는 홤수
    console.log(데이터); // {brand: 'Hyundai', model: 'Kona', price: 30000, img: 'https://codingapple1.github.io/kona.jpg'}
  });
});
```

```jsx
$(".btn-danger").click(function () {
  $.ajax({
    url: "https://codingapple1.github.io/data.json",
    type: "GET", // 위 주소에 GET 요청을 해서 보내주는 데이터를 가져와라
  }).done(function (데이터) {
    // ajax 요청이 성공했을 때 실행 시켜주는 홤수
    $(".card-title").html(데이터.model);
  });
});
```

```jsx
$('.btn-danger').click(function() {

    $.ajax({
        url : 'https://codingapple1.github.io/data.json',
        type : 'GET' // 위 주소에 GET 요청을 해서 보내주는 데이터를 가져와라
    }).done(function(데이터){ // ajax 요청이 성공했을 때 실행 시켜주는 홤수
        $('.card-title').html(데이터.model)
        **$('.card-text').html(데이터.price)
        $('.card-img-top').attr('src', 데이터.img)**
    })
})
```

가격, 이미지 추가

URL 어디로 요청하는지 어떻게 아는지 ?

→ 서버 개발자들이 api 문서로 만들어 놓음

## position: sticky

왼쪽은 잘 스크롤되는 글자, 오른쪽은 고정된 이미지

스크롤되면 이미지는 화면에 고정 → position: sticky

→ position: fixed와 유사 but, position: sticky는 조건부로 fixed

→ 스크롤 되다가 이미지 등장 했을때 그 때 fixed 동작, 부모박스 넘어서면 해제

```jsx
<body style="background: gray; height: 3000px">
    <div class="gray">
        <div class="image"><img src="appletv.jpeg" width="100%" alt=""></div>
        <div style="clear: both"></div>
        <div class="text" style="margin-top: 300px;">High Frame Rate HDR.2
            It’s a game changer.
            With support for high dynamic range (HDR) video at 60 frames per second, Apple TV 4K delivers brighter, more realistic colors and greater detail. Fast‑action sports look incredibly smooth. Nature documentaries come alive. And YouTube videos jump off the screen.</div>
            <div style="clear: both"></div>
            <div class="text" style="margin-top: 300px;">High Frame Rate HDR.2
                It’s a game changer.
                With support for high dynamic range (HDR) video at 60 frames per second, Apple TV 4K delivers brighter, more realistic colors and greater detail. Fast‑action sports look incredibly smooth. Nature documentaries come alive. And YouTube videos jump off the screen.</div>
                <div style="clear: both"></div>
                <div class="text" style="margin-top: 300px;">High Frame Rate HDR.2
                    It’s a game changer.
                    With support for high dynamic range (HDR) video at 60 frames per second, Apple TV 4K delivers brighter, more realistic colors and greater detail. Fast‑action sports look incredibly smooth. Nature documentaries come alive. And YouTube videos jump off the screen.</div>
    </div>
```

```css
.gray {
  background: lightgray;
  height: 2000px;
  margin-top: 500px;
}
.image {
  float: right;
  width: 400px;
  position: sticky;
  top: 100px;
}
.text {
  float: left;
  width: 300px;
}
```

![https://codingapple.com/wp-content/uploads/2019/10/Animation3.gif](https://codingapple.com/wp-content/uploads/2019/10/Animation3.gif)

## 스크롤 위치에 따라 변하는 애니메이션

![https://codingapple.com/wp-content/uploads/2019/10/iphoneanimate2.gif](https://codingapple.com/wp-content/uploads/2019/10/iphoneanimate2.gif)

→ 스크롤 내리면 서서히 사라짐

스크롤 위치에 따라 변하는 CSS 속성

ex) 10 만큼 스크롤되면 투명도 0.9, 20만큼 스크롤되면 투명도 0.8 ... 이런식으로 설정해줘야 함!

650쯤 스크롤 하면 opacity: 1

1150쯤 스크롤하면 opacity: 1

y = a X 높이 + b

높이가 650일 때 y는 1

높이가 1150일 때 y는 0

→ a = -1/500, b= 115/50

```jsx
$(window).scroll(function () {
  var 높이 = $(window).scrollTop(); // 현재 높이 알려줌
  console.log(높이);
  // 650 ~ 1150까지 스크롤바 내리면, 첫째카드의 opacity 1~0으로 서서히 변경해주셈
  var y = (-1 / 500) * 높이 + 115 / 50;
  $(".card-box").eq(0).css("opacity", y);
  $(".card-box").eq(0).css("width", y);
});
```

숙제 → 그림의 사이즈가 서서히 작아져서 0.9배 정도로 작아져야 함

## Hammer.js로 이미지 슬라이드 터치 기능만들기

터치 & 드래그하면 이미지가 변하는 슬라이드

`Hammer.js` 라는 라이브러리 설치하면 편함 + jQuery도 설치

```jsx
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/hammer.js/2.0.8/hammer.min.js"
  integrity="sha256-eVNjHw5UeU0jUqPPpZHAkU1z4U+QFBBY488WvueTm88="
  crossorigin="anonymous"
></script>
```

Hammer.js 사용 전 세팅

1. 일단 JS 셀렉터로 기능개발할 요소 찾기
2. new Hammer.Manager()/add()로 요소 등록

Pan : 슬라이드

rotate : 회전

pinch : 이미지 확대 or 축소

Manager : 두 개의 터치를 동시에 검사할 때

threshold: 이벤트 작동 역치

```jsx
var 이미지1 = document.querySelectorAll(".slide-box img")[0];

var 매니저 = new Hammer.Manager(이미지1);
매니저.add(new Hammer.Pan({ threshold: 0 }));

매니저.on("pan", function (e) {
  // pan 될때마다 코드실행해줌
  console.log(e.deltaX); // x축으로 이동한 거리 -> 슬라이드 방향도 알 수 있음
});
```

Hammer.js 안쓰면

touchstart(터치 시작시)

touchmove(터치중)

touched(터치 끝날시)

→ (시작좌표 - 최종좌표) 로 움직인 거리를 직접 계산해야함

슬라이드한만큼 박스를 왼쪽으로 이동시키기

마우스를 떼면 이미지 2가 나오도록

```jsx
var 이미지1 = document.querySelectorAll(".slide-box img")[0];

var 매니저 = new Hammer.Manager(이미지1);
매니저.add(new Hammer.Pan({ threshold: 0 }));

매니저.on("pan", function (e) {
  // pan 될때마다 코드실행해줌
  console.log(e.deltaX);
  if (e.deltaX < -1) {
    // 만약 왼쪽으로 이미지 슬라이드 했을 때
    $(".slide-container").css("transform", "translateX(" + e.deltaX + "px)");
  }
});
```

```css
.slide-container {
  width: 300vw;
  /* transition: transform 1s; */
}
```

이미지 슬라이드하고 떼면 다음 이미지 보여주도록

`e.isFinal` → 터치 끝났는지 알려줌

```jsx
var 이미지1 = document.querySelectorAll('.slide-box img')[0];

      var 매니저 = new Hammer.Manager(이미지1);
      매니저.add(new Hammer.Pan({threshold: 0}))


      매니저.on('pan', function(e){ // pan 될때마다 코드실행해줌
      console.log(e.deltaX)
      **if (e.deltaX < -1 ){ // 만약 왼쪽으로 이미지 슬라이드 했을 때
      $('.slide-container').css('transform', 'translateX('+ e.deltaX +'px)')
      if(e.isFinal) {  // 만약 이사람이 마우스 놓으면
      $('.slide-container').css('transform', 'translateX(-100vw)') // 두번째 사진으로 변하기**
    }
    }
    })
```

→ 슬라이드 하고 떼면 이미지가 너무 한번에 변함

→ `.slide-container` 에 `transition: transform 0.5s;` 추가하면 `Pan` 할때마다 `transition` 작동하는 오류 발생

→ `.transforming` 이라는 다른 클래스 하나 더 생성

`<div class="slide-container transforming" >`

```css
.slide-container {
  width: 300vw;
  /* transition: transform 0.5s; */
}
.transforming {
  transition: transform 0.5s;
}
```

→ 원할 때만 transition 부여하려고 따로 클래스 만듦

→ 터치가 끝난순간에만 transition 속성을 추가하고 싶음, 터치하고 있을 때는 transform이란 클래스가 없어야 됨

```jsx
var 이미지1 = document.querySelectorAll(".slide-box img")[0];

var 매니저 = new Hammer.Manager(이미지1);
매니저.add(new Hammer.Pan({ threshold: 0 }));

매니저.on("pan", function (e) {
  // pan 될때마다 코드실행해줌
  console.log(e.deltaX);
  if (e.deltaX < -1) {
    // 만약 왼쪽으로 이미지 슬라이드 했을 때
    $(".slide-container").css("transform", "translateX(" + e.deltaX + "px)");
    if (e.isFinal) {
      // 만약 이사람이 마우스 놓으면
      $(".slide-container").addClass("transforming"); // transforming class 추가
      $(".slide-container").css("transform", "translateX(-100vw)"); // 두번째 사진으로 변하기(사진이 왼쪽으로 슬라이드)
      setTimeout(function () {
        // 해당 함수를 몇 초 후에 실행하라
        $(".slide-container").removeClass("transforming"); // transforming class 제거
      }, 500); // 0.5초 후에 코드실행해라
    }
  }
});
```

→ 코드가 길기 때문에 그냥 터치가 되는 이미지 슬라이더 라이브러리를 쓰는게 더 좋음

## 한글자씩 출현하는 Typewriting 애니메이션 만들기

타이핑 되는 효과 만들기

0.5초 후에 코드를 실행하려면? → `setTimeout`

```jsx
var h1태그 = document.querySelector("h1");
var 원래글씨 = document.querySelector("h1").innerHTML;
$("button").click(function () {
  // 버튼을 누르면
  h1태그.innerHTML = ""; // h1 빈칸으로 만들고
  setTimeout(function () {
    h1태그.innerHTML = h1태그.innerHTML + 원래글씨[0];
  }, 500); // 0.5초 후에 h1안에 a를 더함

  setTimeout(function () {
    h1태그.innerHTML = h1태그.innerHTML + 원래글씨[1];
  }, 1000); // 0.5초 후에 h1안에 b를 더함

  setTimeout(function () {
    h1태그.innerHTML = h1태그.innerHTML + 원래글씨[2];
  }, 1500); // 0.5초 후에 h1안에 c를 더함
});
```

setTimeout 반복문 돌리기

```jsx
for (var i = 0; i < 원래글씨.length; i++) {
  setTimeout(function () {
    h1태그.innerHTML = h1태그.innerHTML + 원래글씨[i];
  }, 500 * i); // 0.5초 후에 h1안에 a를 더함
}
```

→ `undefined` → 반복문은 0.001초만에 6번 반복 끝냄 but, setTimeout은 0.5초 후에 실행함

→ `let` 으로 고치면 반복문이 잘 돌아감

```jsx
var h1태그 = document.querySelector('h1')
      var 원래글씨 = document.querySelector('h1').innerHTML
      $('button').click(function() { // 버튼을 누르면
      h1태그.innerHTML = ''  // h1 빈칸으로 만들고

      for(let i = 0;  i < 원래글씨.length; i++){
      setTimeout(function() {
          h1태그.innerHTML = h1태그.innerHTML + 원래글씨[i]
      }, 500 * i) // 0.5초 후에 h1안에 a를 더함
    }
```

응용 : 한글 자음모음 타이핑 효과

ex) 안녕하세요

→ ㅇ → 아 → 안 → ㄴ → 녀 → 녕 ...

앞 내용 지우고 더하는 식으로 진행돼야 함

→ 한글 타이핑 효과 라이브러리 쓰는게 편함

함수화하기

변수를 파라미터로 바꿔줘야 다른데도 적용 가능

```jsx
var h1태그 = document.querySelector("h1");
var 원래글씨 = document.querySelector("h1").innerHTML;

$("button").click(function () {
  // 버튼을 누르면
  애니메이션(h1태그, 원래글씨);
});

function 애니메이션(h1태그, 원래글씨) {
  h1태그.innerHTML = ""; // h1 빈칸으로 만들고

  for (let i = 0; i < 원래글씨.length; i++) {
    setTimeout(function () {
      h1태그.innerHTML = h1태그.innerHTML + 원래글씨[i];
    }, 500 * (i + 1)); // 0.5초 후에 h1안에 a를 더함
  }
}
```
