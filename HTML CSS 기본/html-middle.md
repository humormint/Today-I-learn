# 중급 모듈

## **웹폰트 넣는 법과 안티앨리어싱**

- 웹폰트 첨부방법

`font-family: 'gulim'`

→ 글씨체가 방문자들의 pc에 설치 되어 있어야 이용 가능

커스텀 폰트 넣는법

```css
@font-face {
  font-family: "작명~~";
  src: url(../font/NanumSqurareR.ttf);
}
```

→ 내가 준비한 폰트 파일을 CSS에서 사용가능하게 등록하는 과정

→ 자유롭게 폰트 가져다 쓸 수 있음

→ 한글 폰트는 용량이 너무 커서 1 ~ 2개 만 사용!

- 용량 줄이기

woff 이용하면 현저히 용량 줄어듦 → 트래픽도 줄일 수 있음

→ 굵은 폰트를 따로 등록해야 함!

나눔스퀘어 woff 버전 : [https://github.com/moonspam/NanumSquare](https://github.com/moonspam/NanumSquare)

font-weight 그냥 주면 안이쁨

```css
@font-face {
  font-family: "이쁜폰트";
  font-weight: 800;
  src: url(../font/NanumSquareB.woff);
}

body {
  margin: 0px;
  font-family: "이쁜폰트";
  font-weight: 900;
}
```

- 호환성잡기

- 트래픽 절약
- google Fonts → 트래핑 절약 (구글이 가져오기 때문에)
- 폰트 ant-aliasing

폰트 부드럽게 처리하려면 → 회전시키면 됨

```css
p,
h4,
h3,
span {
  transform: rotate(0.03deg);
}
```

## 레이아웃 만들기 3 : 편리한 Flexbox

float: left

display: inline-block

대신,

display: flex 쓰면 박스 가로 배치가 쉬워짐

가로로 배치하고 싶은 div 박스 부모에 display: flex 주면 가로배치!

```css
.flex-container {
  display: flex;
  justify-content: center;
}
```

- flex 이용시 세로 배치

```css
.flex-container {
  display: flex;
  justify-content: row;
}
```

→ 나중에 반응형으로 디자인 할 때도 유용(PC에서는 가로, 모바일에서는 세로)

- width 크면 밑으로 보내고 싶을 때

```css
.flex-container {
  display: flex;
  flex-wrap: wrap;
}
```

![스크린샷 2022-02-03 오후 6.39.06.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1ed9c89-5879-46fa-bd95-166502b7dab8/스크린샷_2022-02-03_오후_6.39.06.png)

→

![스크린샷 2022-02-03 오후 6.39.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80422d3e-b10e-4b0c-ae17-218fc1afc4bd/스크린샷_2022-02-03_오후_6.39.51.png)

flex-grow → 박스 크기를 비율로 설정 가능!

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1e6efbd-656c-454b-9ed6-2e7010a9a342/Untitled.png)

# **head 태그에 들어갈 내용 정리**

이번 챕터는 간단하게 텍스트로 진행합니다.

```html
<!DOCTYPE html>
<head>
  어쩌구
</head>
<body>
  저쩌구
</body>
```

HTML 문서의 기본 템플릿은 꼭 head와 body 태그를 포함해야합니다.

head태그는 사이트 내에서 눈에는 보이지 않는 중요한 정보들이 들어갈 수 있는데

head태그 내에서 쓸 수 있는 중요한 태그들을 몇개 나열해보겠습니다.

**1. 각종 CSS 파일들**

```html
<head>
  <link href="css/main.css" rel="stylesheet" />
</head>
```

CSS 파일들을 첨부할 때 링크태그를 집어넣을 수 있습니다.

위 경로는 현 HTML 파일과 같은 위치에 있는 css폴더 안에 있는 main.css 파일을 첨부하라고 되어있네요.

1. css/main.css

2. /css/main.css

참고로 위 두개의 경로는 다른 경로입니다.

1번은 현재 HTML파일과 같은 경로에 있는 css라는 폴더 내의 main.css 파일을 의미하고

2번은 현재 사이트의 메인경로 (codingapple.com)부터 시작해서 codingapple.com/css/main.css 파일을 첨부해라 라는 뜻입니다.

슬래쉬 기호가 첨부터 붙어있으면 사이트 메인경로부터 시작해라~ 라는 의미입니다.

멋진 말로 1번은 상대경로, 2번은 절대경로라고 합니다.

**2. 스타일 태그**

```
<head>
  <style>
    .button {
      color : red;
    }
  </style>
</head>
```

CSS 파일을 만들기 귀찮으면 <style> 태그를 열어서 CSS를 작성하기도 합니다.

CSS 파일과 유사하게 동작합니다.

<body> 안에 넣어도 동작하는데 html 파일안의 코드는 **위에 있을 수록 먼저 읽기 때문에**

<body>태그 맨 밑 같은 곳에 두면 사이트 로딩시 스타일이 잠깐 깨질 수 있습니다.

그래서 넣을거면 <head>에 넣는 사람이 많습니다.

**3. 사이트 제목**

```html
<head>
  <title>네이버입니다</title>
</head>
```

사이트 제목을 넣을 수 있습니다. (브라우저 탭에 뜨는 이름입니다)

**4. 여러가지 meta 태그**

```
<head>
  <meta charset="UTF-8">
  <meta name="description" content="자바스크립트 인강 전문 코딩애플입니다.">
  <meta name="keywords" content="HTML,CSS,JavaScript,자바스크립트,코딩">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

1. 사이트의 인코딩 형식을 지정할 때 charset="UTF-8" 이라고 속성을 적을 수 있습니다.

2. 사이트의 검색 결과 화면에 뜨는 글귀를 수정하고 싶으면 이런 속성들을 추가할 수 있습니다. name="description" content="어쩌구"

description은 구글 검색시 파란 제목으로 뜨는 글귀,

keywords는 검색에 도움을 주는 키워드 등입니다.

(이런건 온라인 마케팅 하는 사람들이 잘 압니다)

3. 사이트 초기 zoom 레벨이나 폭을 지정해주려면 name="viewport" 라는 속성을 부여하시면 됩니다.

width=device-width는 모바일 기기의 실제 폭으로 렌더링 해주세요 라는 뜻입니다.

요즘 스마트폰 가로 해상도가 1920px을 넘어가는 폰들이 많죠.

그럼 이것만 보고 1920px 에 해당하는 페이지를 띄워줄 수는 없겠죠?

그래서 실제 접속시 스마트폰 기기의 실제 가로폭을 보고 렌더링하라고 명령하는 부분이라고 보시면 됩니다.

initial-scale=1 이 부분은 접속시의 화면 줌레벨 설정입니다.

그래서 반응형 웹을 만들 때 저 meta 태그를 복붙하시고 시작하시면 되겠습니다.

**5. open graph**

```
<head>
  <meta property="og:image" content="/이미지경로.jpg">
  <meta property="og:description" content="사이트설명">
  <meta property="og:title" content="사이트제목">
</head>
```

facebook이 만든 og 라는 메타태그가 있습니다.

여러분이 가끔 카톡 페북 이런 곳에 링크를 공유하면

![https://codingapple.com/wp-content/uploads/2019/12/%EC%BA%A1%EC%B2%982.png](https://codingapple.com/wp-content/uploads/2019/12/%EC%BA%A1%EC%B2%982.png)

▲ 이런 식으로 박스가 뜨고 사이트 설명, 제목, 이미지가 뜹니다.

이걸 커스터마이징하고 싶으면 저런 meta 태그를 따로 집어넣으면 됩니다.

**6. Favicon**

```html
<head>
  <link rel="icon" href="아이콘경로.ico" type="image/x-icon" />
</head>
```

여러분의 웹사이트 제목 옆에 뜨는 아이콘을 커스터마이징하려면

이렇게 link 태그로 첨부하면 됩니다.

![https://codingapple.com/wp-content/uploads/2019/12/%EC%BA%A1%EC%B2%983.png](https://codingapple.com/wp-content/uploads/2019/12/%EC%BA%A1%EC%B2%983.png)

그럼 이렇게 아이콘이 생깁니다.

- ico 대신 png 파일로 넣어도 됩니다. ico가 호환성은 가장 좋습니다.
- 요즘은 32 x 32 사이즈로 제작하면 됩니다.
- 그리고 웹사이트를 바탕화면에 바로가기추가했을 경우 뜨는 아이콘도 커스터마이징 가능합니다.

rel="apple-touch-icon-precomposed"

이런 식으로 rel 속성을 조정하면 되는데 OS마다 요구하는 rel 속성이 달라서 필요해지면 찾아 적용하시거나

favicon generator 이런거 검색해서 한번 써보시면 OS별로 알아서 만들어줍니다.

## 반응형 레이아웃

반응형 사이트를 만들기 위한 태그

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

- CSS 파일

media query 문법

"현재 브라우저의 폭이 1200px 이하일 경우에 안에 있는 class를 적용해주세요~" 라는 뜻입니다.

여러개 원하는 만큼 사용가능합니다.

```css
@media screen and (max-width: 1200px) {
  .main-title {
    font-size: 30px;
  }
}
```

→ 여러 번 사용 가능

```css
@media screen and (max-width: 1200px) {
  .main-title {
    font-size: 30px;
  }
}
@media screen and (max-width: 768px) {
  .main0title {
    font-size: 20px;
  }
}
```

1200px → 여기부터 태블릿

992px, 768px,

576px → 여기부터 모바일

![스크린샷 2022-02-05 오후 6.01.58.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2f0d9e9-f5ba-44e4-8ed2-8f642dbb49b7/스크린샷_2022-02-05_오후_6.01.58.png)

![스크린샷 2022-02-05 오후 6.06.30.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/affcb6d5-6f2a-4d38-83e0-ed527d7ca54a/스크린샷_2022-02-05_오후_6.06.30.png)

```css
.product-container div {
  /* 부모태그 안에 있는 모든 div에 적용 */
  width: 300px;
  height: 300px;
}
```

media query 문법은 항상 맨 밑에 있어야 작동을 잘함

→ 코딩애플은 float으로 반응형 구현! → flex로 반응형 구현한 영상 찾아보기

## CSS 디버깅 하는법

css 짜다가 원하지 않는 방향으로 나타나면

→ 당연히 CSS 파일부터 찾아봐야 함(오래걸림)

→ 크롬 개발자도구 쓰면 빠름 → 우클릭, 검사

순서가 중요함 ! 위에 있을수록 우선적용! → 해당 부분 수정하기!

적용 안되고있는 스타일 → 취소선 적용됨

user agent stylesheet → 브라우저가 기본적으로 제공하는 스타일시트

## Font Awesom

1. CDN

절대경로(http~)로 작성 → 사이트 다운되면 CSS 이용 불가 할 수 있음

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css"
/>
```

1. 직접 다운로드

→ all.min.css → 첨부 (상대경로로)

```html
<link rel="stylesheet" href="fontawesome/css/all.min.css" />
```

→ 아이콘 html 태그 복사 붙여넣기 하면됨!

아이콘 넣은 다음 백그라운드 div의 border-radius 많이 주면 원이 됨!

ex)

```css
.product-container i {
background-color: burlywood;
width: 100px;
height: 100px;
**border-radius: 50px;**
padding-top: 25px;
}
```

![스크린샷 2022-02-07 오후 3.17.37.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea66f374-c287-49db-be63-4b82315c3dcf/스크린샷_2022-02-07_오후_3.17.37.png)

## Transition 속성으로 CSS 애니매이션 구현하기

**숙제해결을 위한 overflow 속성**

```html
<div style="width: 50px; height: 50px; overflow: hidden">
  <p>aaaaaaaaaaaaaaaaaaa</p>
</div>
```

overflow라는 속성은 박스의 폭이나 높이를 초과하는 내부요소를 처리하기 위한 속성입니다.

hidden 값을 주면 넘치는 내부요소를 자동으로 잘라 없애줍니다.

그래서 위 예제는 박스를 넘어가는 글자를 잘라 없애줍니다.

글자 뿐만 아니라 이미지, 박스 이런게 넘쳐 흘러도 똑같이 잘라 없애줍니다.

overflow : visible은 넘치는 부분을 그대로 보여주고

overflow : scroll은 넘치는 요소를 보기 위한 스크롤바가 생길 수 있습니다.

**opacity 속성**

```css
.box {
  opacity: 0;
}
```

현재 HTML 요소의 투명도를 조절할 수 있습니다.

0부터 1까지의 실수를 입력할 수 있습니다.

0.5 이러면 반투명해짐

**transition 속성**

```css
.box {
  opacity: 0; /* 반투명 */
  transition: all 1s;
}
```

transition을 부여하면

여기에 적용된 CSS가 변할 때 서서히 변경해줍니다.

all은 모든 스타일이 변할 때 서서히 변경하라는 뜻이고 (all 대신 opacity 이렇게 하나만 줄 수도 있음)

1s 이건 1초에 걸쳐서 서서히 변경해달라는 뜻입니다.

**transition 세부 속성 살펴보기**

```css
.box {
  transition-delay: 1s; /* 시작 전 딜레이 */
  transition-duration: 0.5s; /* transition 작동 속도 */
  transition-property: opacity; /* 어떤 속성에 transition 입힐건지 */
  transition-timing-function: ease-in; /* 동작 속도 그래프조정 */
}
```

이런 식으로 세부설정도 가능합니다.

애니메이션 종류도 수십가지일텐데

그거 전부 하나하나 설명하려면 100강도 모자르기 때문에 귀찮으니

여러분은 그냥 애니메이션 만드는 법칙을 외워가시길 바랍니다.

이거 외우면 앞으로 혼자 알아서 만들 수 있음

**one-way 애니메이션 혼자 알아서 만드는 법 :**

one-way 애니메이션은 A에서 B로 정지없이 쭉 이동하는 애니메이션을 뜻합니다.

1. 시작스타일 정하기

2. 최종스타일 정하기

3. 언제 최종스타일로 변할지 트리거 주기 (대부분 마우스 올렸을 때임)

4. transition 으로 서서히 동작하게 만들기

이런 스텝으로 CSS 코드 짜면 끝입니다.

3번은 :hover 이런거 쓰면 된다는 소리입니다.

CSS만으로 만들 수 있는 트리거는 마우스 올렸을 때 이 정도가 가장 흔합니다.

나중에 자바스크립트를 배우게 되면

클릭시, 드래그시, 키 입력시 이런걸 전부 애니메이션 발동 트리거로 만들 수 있습니다.

**상품 진열 레이아웃**

```html
<div class="shop-bg">
  <div class="shop-container">
    <div class="shop-item">
      <div>
        <img src="img/product1.jpg" />
      </div>
    </div>
    <div class="shop-item">
      <img src="img/product2.jpg" />
    </div>
    <div class="shop-item">
      <img src="img/product3.jpg" />
    </div>
  </div>
</div>
```

```css
.shop-bg {
  background-color: #eee;
  padding: 20px;
}
.shop-container {
  display: flex;
  width: 90%;
  margin: auto;
}
.shop-item {
  width: 33%;
  padding: 10px;
}
.shop-item img {
  width: 100%;
  display: block;
}
```

```html
<div class="shop-bg">
  <div class="shop-container">
    <div class="shop-item">
      **
      <div style="position: relative">
        <!-- 부모 태그는 relatvie -->
        <div class="overlay"></div>
        <!--  자식은 absolute, 이미지 위에 박스하나 -->** <img ~ />
      </div>
    </div>
  </div>
</div>
```

```css
.overlay {
  position: absolute; /* 자식은 absolute */
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  opacity: 0; /* 애니메이션 시작 */
  transition: all 1s; /* 위에 있는 스타일이 변하면 1초 걸려서 서서히 변화해 주세요 */
}
.overlay:hover {
  opacity: 1;
}
```

검정색이 길게 나오면 img에 display: block; 주면 사라짐!

### 나의 풀이

```html

  <body>
    <div class="shop-bg">
      <div class="shop-container">
        <div class="shop-item">
        <div style="position: relative">
            <div class="overlay">70$</div>
            <img src="../home.jpeg" />
        </div>
          </div>
        <div class="shop-item">
          <img src="../home2.jpeg" />
        </div>
        <div class="shop-item">
          <img src="../home3.jpeg" />
        </div>
      </div>
    </div>
</div>
  </body>
```

```css
.shop-container {
  display: flex;
  justify-content: space-between;
  width: 100%;
  height: 100%;
  margin: auto;
}
.shop-item img {
  width: 200px;
  height: 200px;
}
.overlay {
  position: absolute; /* 자식은 absolute (붕뜬 상태) */
  width: 200px;
  height: 200px;
  background: rgba(0, 0, 0, 0.5);
  opacity: 0; /* 애니메이션 시작 */
  transition: all 1s; /* 위에 있는 스타일이 변하면 1초 걸려서 서서히 변화해 주세요 */
  font-size: 40px;
  text-align: center; /* 좌우 중앙 정렬*/
  color: white;
  line-height: 200px; /* 부모태그 높이랑 같게 해주면 상하도 중앙정렬 */
}
.overlay:hover {
  opacity: 1;
}
```

![스크린샷 2022-02-07 오후 7.37.26.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d6988758-762b-455b-92eb-622679eada58/스크린샷_2022-02-07_오후_7.37.26.png)
