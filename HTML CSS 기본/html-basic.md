# 기초 모듈

float 이용한 레이아웃 만들기

레이아웃 만들기 전에 박스 전체를 감싸는 박스(container) 만들면 유용함

float: left → 요소를 붕 띄워서 왼쪽정렬

```css
.left-menu {
  width: 30%;
  height: 400px;
  background: blue;
  float: left;
}
.right {
  width: 70%;
  height: 400px;
  background: green;
  float: left;
}
```

-

![스크린샷 2022-01-29 오후 9.47.03.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0bce2d6a-25eb-4ab8-bb85-0944594ab14f/스크린샷_2022-01-29_오후_9.47.03.png)

→ 박스 배치할 때 float 사용하면 유용함

→ 다음에 div는 float 설정한 div 아래에 깔리지 않고 같은 위치에 있음 (float는 공중에 떠 있으니까)

→ 다음 div에 clear: both를 주면 해결할 수 있음

![스크린샷 2022-01-29 오후 9.52.17.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b79bb561-ed06-4f61-acc0-8237ff494ed4/스크린샷_2022-01-29_오후_9.52.17.png)

```css
.footer {
  width: 100%;
  height: 100px;
  background-color: grey;
  clear: both;
}
```

## inline-block

→ 가로로 배치 가능

**display: inline-block; 후에**

```css
.left-menu {
        width: 30%;
        height: 400px;
        background: blue;
        **display: inline-block;**
}
.right {
        width: 70%;
        height: 400px;
        background: green;
        **display: inline-block;**
}
```

left와 right 공백없애면

```html
<div class="left-menu"></div>
<div class="right"></div>
```

![스크린샷 2022-01-29 오후 10.40.25.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d44bfc79-40c1-48d1-b051-93e80a3ebf07/스크린샷_2022-01-29_오후_10.40.25.png)

→ 가로로 정렬

→ 불편함 → float 를 보통 사용함 → 주석을 사용하면 가능하긴함

## CSS selcetor

float → 마진 줘도 안밀려남

→ float 준 다음에 clear: both 를 넣은 <div> 추가하는 것을 선호

### navbar 만들기

→ul, li 태그 활용 하면 편함

→nav태그 →div랑 똑같음 but 한번에 파악하기 쉬움, 특수한 기능은 없음

section, footer도 비슷함!

```html
<nav>
  <ul class="navbar">
    <li>축구</li>
    <li>야구</li>
    <li>농구</li>
    <li>배구</li>
  </ul>
</nav>
```

```css
.navbar li {
  display: inline-block; /* selector 문법 중 공백은  ~ 안에 있는 모든 자식, >는 직계자식 */
}
```

→ 한번의 명령으로 navbar 리스트 들을 가로로 배치할 수 있음

```css
.navbar a {
  font-size: 20px;
  text-decoration: none; /* 클릭하면 생기는 밑줄 제거*/
}
```

→ navbar 안에 있는 모든 a태그 스타일링

![스크린샷 2022-01-30 오후 4.35.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b129a2e6-0e1e-42af-872f-665d3442fc7f/스크린샷_2022-01-30_오후_4.35.07.png)

```css
.main-background {
  width: 80%;
  height: 500px;
  background-image: url(../aa.jpeg);
  background-size: cover; /*꽉 채워라*/
  background-size: contain; /* 이미지가 잘리지 않게 해라*/
  background-repeat: no-repeat;
}
```

→ background 이미지

## Position

1. 좌표이동 가능
2. 공중에 붕 뜸

```css
.box {
  position: static; /* 기준이 없음(좌표 적용 불가)*/
  position: relative; /*기준이 내 원래 위치에서 좌표 이동*/
  position: absolute; /*기준이 내 부모*/
  position: fixed; /* 기준이 브라우저 창, 화면 고정*/
}
```

```css
position: relative;
top: 100px; /*원래 기준에서 마진 100px 만큼*/
```

absolute → 내 부모 태그 중에 position: relative 가진 부모 기준!

버튼 가운데 정렬

```css
position: absolute;
margin: auto;
```

![스크린샷 2022-02-01 오후 5.54.11.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/edff97f5-2b9c-4040-ae4e-6dc43d242dd1/스크린샷_2022-02-01_오후_5.54.11.png)

## 반응형 width & box-sizing

![스크린샷 2022-02-01 오후 6.30.49.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf743e69-db3e-4e5c-a9ad-e92ff6d7d8d6/스크린샷_2022-02-01_오후_6.30.49.png)

```css
.box {
  width: 200px;
  margin: auto;
  padding: 30px;
  text-align: center;
  background-color: #eee;
  margin-top: -50px;
  position: relative;
  top: -40px; /* 위로 올리기 */
}
```

z-index

→ 클수록 앞으로 나옴

- max-width

→ 최대 폭 제한

width는 content 영역의 너비를 의미함(보이는 영역의 폭이 아니라 박스 content 기준)

border, padding → width 에 영향을 줄 수 없음!

해결책 → 실제 보이는 부분을 width로 설정할 수 있음!

width가 padding, border 포함함

```css
box-sizing: border-box;
```

브라우저마다 디자인이 다르게 보일 수 있음

→ nomalize.css

## form & input

폼 만들고 싶을 때 → fome 태그로 input 감싸기

```html
<form action="경로" method="get">
  <input />
  <input />
</form>
```

input 타입

```html
<input type="text" />
<input type="email" />
<input type="password" />
<input type="radio" />
<input type="file" />
<input type="checkbox" />
<input type="submit" />
<select>
  <option>옵션1</option>
</select>
<textarea></textarea>
```

<input value=”미리 채워진 값”>

<input placeholder=”배경글자”>

## table

가로 행 만들 땐 <tr>

세로 열 만들 땐 <td>

제목용 세로 열 만들 때 <th>

→ 굵게 만들기!

```css
td,
th {
  border: 1px solid black;
}
```

→ 테두리 만들기

![스크린샷 2022-02-02 오후 2.42.48.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d266db87-17be-40e3-b42b-001f8df5856a/스크린샷_2022-02-02_오후_2.42.48.png)

- <thead>, <tbody>

엑셀 행에 제목같은 역할!

굳이 쓰지 않아도 됨!

- 셀 테두리 만들기

```css
table {
  width: 100%;
  border: 1px solid #444444;
}
th,
td {
  border: 1px solid #444444;
}
```

- 표 사이에 공백을 줄여줌!

```css
table {
  border-collapse: collapse;
}
```

![스크린샷 2022-02-02 오후 2.49.16.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/059a3eb7-41c9-4e32-8399-c8542ffdf79b/스크린샷_2022-02-02_오후_2.49.16.png)

- 셀 안의 요소 상하 정렬

vertical-align

→ 세로 정렬할 때 쓰는데

inline/inline-block 요소 간의 세로 정렬 할때 (상하) 사용

→ top, middle, bottom 으로 나뉨!

display: inline

폭과 너비가 없는 요소

## presudo-class

클릭할 때 스타일 다르게 줄 수 있음

마우스 올릴때 스타일: hover

클릭중 스타일: active

커서 찍혀 있을 때 스타일: focus

동시에 쓸 때 순서가 중요함

: hover

: focus

: active

:link를 붙이면 방문 전 링크

:visited를 붙이면 방문 후 링크에 스타일을 넣을 수 있음

모든 링크의 밑줄제거는 그냥 a태그에 text-decoration : none 붙이면 됨

## class 작명법(OOCSS, BEM)

- Object Oriented CSS

보통 class 작명 → 재사용 하기 어려움

ex)

```css
.main-btn-red {
  font-size: 20px;
  padding: 15px;
  border: none;
  cursor: pointer;
  background: red;
}

.main-btn-blue {
  font-size: 20px;
  padding: 15px;
  border: none;
  cursor: pointer;
  background: blue;
}
```

클래스 10개면 10개의 코드를 짜야함

→ 뼈대용 class, 살점용 class 각각 제작

```css
.main-btn {
  font-size: 20px;
  padding: 15px;
  border: none;
  cursor: pointer;
}

.bg-red {
  background: red;
}
.bg-blue {
  background: blue;
}
```

→

```html
<button class="main-btn bg-red">빨간버튼</button>
<button class="main-btn bg-blue">파란버튼</button>
```

장점

1. CSS 양이 줄어듦
2. 유지 보수(수정) 편리

→ Utility Class

ex)

```css
.f-small {
  font-size: 12px;
}
.f-mid {
  font-size: 16px;
}
.f-lg {
  font-size: 20px;
}
```

class=”덩어리 이름\_역할-세부특징”

→ 이런 식으로하면 쉽게 만들 수 있음!

→ React, Vue 쓰면 덩어리(Component) 단위로 HTML 파일 나눠서 코드 짬

→ 해당 Component에만 사용 가능한 CSS 생성 가능!
