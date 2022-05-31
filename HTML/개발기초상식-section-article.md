## 1. 개발 기초 상식

| www.naver.com | 이름 | 제주코딩베이스캠프 | 도메인, URL |
| --- | --- | --- | --- |
| 222.130.200.104 | 주소 | 동광로 137 대동빌딩.. | IP |
| 22, 23, 80, 443 .. | 문 |  | PORT |

`도메인`→ 도메인은 사람이 편하게 보기 위해서 만들어진 것입니다. ex) 네이버... 

`IP` → 하지만, 컴퓨터가 알아듣기 쉬운 것이 IP주소 입니다.(숫자로 이루어져 있는 이유입니다)

`PORT` → `https`, `http` 는 웹페이지에 접근하는 경로이며, 다른 경로라고 하더라도 웹페이지에 영향을 줄 수는 없습니다. 

### `lang="ko”`로 변경하기

`cmd + shift +p` 단축키로 명령팔레트에서  `snippets` 입력 후→ html 엔터 → `html.json` 에 아래의 코드를 복붙하면 됩니다.

```json
{
    "Print to console": {
        "prefix": "htmlko",
        "body": [
            "<!DOCTYPE html>",
            "<html lang=\"ko\">",
            "<head>",
            "    <meta charset=\"UTF-8\">",
            "    <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge\">",
            "    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">",
            "    <title>$1</title>",
            "</head>",
            "<body>",
            "    $2",
            "</body>",
            "</html>"
        ],
        "description": "한국어 페이지용 html 템플릿"
    }
}
```

→ 복붙 이후`htmlko` 탭 누르면 `en`이 `ko`로 변경됩니다.

### emmet

`h1+h2`

→ `+` 를 통해 여러가지 태그를 연이어 사용할 수 있습니다.

```html
<h1></h1>
<h2></h2>
```

`lorem` → lorem을 vs code에서 바로 생성해 줍니다.

```html
Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolores quisquam similique consequatur nemo quos laudantium sed amet vitae a alias! Temporibus nemo ad voluptas officiis laudantium est voluptates! Aliquam, quos.
```

`h${hello}*6` → `{}` 는 태그 내부에 입력할 내용입니다.

```html
<h1>hello</h1>
<h2>hello</h2>
<h3>hello</h3>
<h4>hello</h4>
<h5>hello</h5>
<h6>hello</h6>
```

**주요 emmet 총정리**

```html
h1
h1+h2
h1>p
h1+h2+p
h1{hello}
h1>p+p
h1.one
h1#one
.one
#one
h${hello}*6
lorem
lorem*2
lorem5
img
img:z
p[a="value1" b="value2"]
a[href="[www.naver.com](http://www.naver.com/)"]
h1.one.two#three
table>(tr>td*4)*3
```

## 2. HTML living standard

### HTML 레이아웃


→ `div` 태그 남발을 지양하고 `section`, `article` 등의 태그를 최대한 활용하는 것이 좋습니다. `div` 태그를 남발하는 것은 web 접근성을 떨어뜨리기 때문입니다. 
<br>

## 3. Grouping Content

## `<section>`

일반적으로 연관성 있는 문서의 구획을 나누고자 할 때 사용하는 요소입니다.

<aside>
💡 section vs article

* article 요소는 독립적 콘텐츠(다른 서비스에 가져다 놔도 이상하지 않음)
* section 요소는 사이트 내 연관 콘텐츠(다른 서비스에 가져다 놓으면 이상함)
* article과 section 요소는 heading 요소와 함께 사용하는 것을 권장(높이 없이 비워두기도 함)

</aside>

### section

→ Introduction과 Criteria은 흐름상 단독으로 쓰이기 어렵습니다. 

### article


→ 날짜별 날씨는 독립적으로 구분해 배포하거나 재사용할 수 있습니다.

## `<dl>, <dt>, <dd>`

`<dl>`, `<dt>`, `<dd>` 도 목록을 정의할 때 쓰입니다.

차이점이 있다면 `<dl>`, `<dt>`, `<dd>`는 사전처럼 어떠한 것을 정의할 때 쓰이는 목록입니다.
<dl>은 정의 목록(definition list)이며 `<dt>`는 정의할 용어(definition term)을 뜻합니다. `<dd>`는 용
어를 설명(definition description)할 때 쓰입니다.

```html
<dl>
    <dt>HTML</dt>
    <dd>마크업 언어입니다.</dd>
</dl>
```

→ 웹 접근성 고려할때 주로 이용합니다.

## `<div>`

`<article>`, `<section>`, `<header>`, `<nav>`는 기본적으로 `<div>`와 같은 역할을 합니다. 차이점이 있다면  태그에 의미를 부여한 것입니다. `<article>`, `<section>`, `<header>`, `<nav>` 모두 `<div>`로 대신 사용할 수 있으나 보다 적합한 요소를 찾은 후 대용할 태그가 없을 경우 사용하시기 바랍니다. 

## `<figure>, <figcaption>`

웹페이지를 탐색하다보면 가끔 캡션(자막, 설명)이 있는 이미지를 접할 때가 있습니다. 이러한 컨텐츠의 경우 이미지와 캡션이 연결되도록 `<figure>` 요소를 도입할 수 있습니다.


```html
    <figure>
        <img width="'auto" height="100px" src="다운로드.png" alt="자바스크립트">
        <figcaption>
            JS 
        </figcaption>
    </figure>
```

`<figcaption>` 요소는 이미지에 캡션을 추가하기 위해 도입되었으며 `<figure>,` `<figcaption>`요소가 나오기 이전에는 `<img>` 요소와 해당하는 캡션을 연결할 방법이 없었습니다.

## `<pre>`

HTML에 작성한 내용 그대로 화면에 표현합니다. 주로 컴퓨터 코드를 표현할 때 사용합니다.

```html
<pre>
  <code>
    let val= 1;
    function myFunc(value){
      return value;
    }
    myFunc(val);
  </code>
</pre>
```

→ 간격을 그대로 표현하고 싶을 때 사용합니다.

## `<main>`

**HTML `<main>` 요소**는 문서의 주요 콘텐츠를 나타냅니다. → 요즘 `<main>`에 넣는게 일반적입니다.

주요 콘텐츠 영역이란 문서의 핵심 주제나 웹어플리케이션의 핵심 기능에 직접적으로 연결되어 있는 부분을 뜻합니다. 메인 요소안에 들어가는 내용은 문서의 유일한 내용이어야 합니다.  


## `<hr>`

<hr> 태그는 원래는 가로줄을 표현하기 위해 사용했으나 HTML5에 오면서 의미가 생긴 요소입니다. **이야기에서의 장면 전환 혹은 문단 안에서 주제가 변경되었을 때 그 구별을 위해 사용**합니다. 

```html
<h1>hello world</h1>
<hr>
<p>hello <br> world</p>
<hr width="300px" align="center" size="3" color="red" noshade>
```

→ 과거에는 `<hr></hr>` 로 닫는 태그를 추가했으나, 최근에는 닫는 태그 쓸 필요없이 `<hr>`로 단독 표기해도 됩니다.
<br>

## 4. 유용한 Tip

- `opt + cmd + 방향키` → 동일 태그를 여러개 선택할 수 있습니다.
- vs code → `cmd +  n` → `cmd + s` →파일을 빠르게 생성할 수 있습니다.
- 중앙정렬 방법은  `transform`과 `margin: 0 auto` 를 상황에 따라 이용할 수 있습니다.
- 인프런  `스타트업 A to Z` → 스타트업 관련 정보를 알 수 있습니다
- 노션에 기업 리스트, 기술스택 적고, 합불여부를 기입하는 기업서치를 처음부터 꾸준히 해야합니다.