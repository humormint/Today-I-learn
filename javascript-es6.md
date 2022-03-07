## this 키워드

```jsx
console.log(this); // Window

function 함수() {
  this; // Window
}
```

this 키워드는 뜻이 3 ~ 4개 정도 됨

1. 그냥 쓰거나 일반 함수 안에서 쓰면 `{window}` , strict mode + 일반 함수 내에서 쓰면 `undefined`

```jsx
"use strict"; // 자바스크립트를 엄격하게 실행
```

ex) `x = 300;` → 평상시에는 가능하지만 `use strict` 모드 에서는 사용 불가 `var x = 300;` 이렇게 해야함!

```jsx
"use strict"; // 자바스크립트를 엄격하게 실행
console.log(this);
function 함수() {
  console.log(this);
}
함수(); // undefined
```

1. this를 오브젝트 내 함수(메서드)에서 쓰면 → 그 함수를 가지고 있는 오브젝트를 뜻함(나를 포함하고 있는 오브젝트)

```jsx
'use strict';  // 자바스크립트를 엄격하게 실행
        console.log(this)

        **var 오브젝트 = {
            data : 'kim',
            함수 : function(){
                console.log(this)
            }**
        }
        오브젝트.함수(); // {data: 'kim', 함수: ƒ}
```

오브젝트 안에 오브젝트를 넣으면

```jsx
'use strict';  // 자바스크립트를 엄격하게 실행
        console.log(this)

        var 오브젝트 = {
            **data : {
            함수 : function(){
                console.log(this)
            }
        }**
    }
        오브젝트.data.함수(); // {함수: ƒ}
```

→ this는 그 함수를 가지고 있는 오브젝트를 뜻함

`function()` 대신 `arrow function`으로 바꾸면

`function()` = `()⇒`

this 값을 함수 밖에 있던거 그대로 씀 (부모, 상위요소 this 값을 물려 받아 씀)

```jsx
'use strict';  // 자바스크립트를 엄격하게 실행
        **console.log(this)**

        var 오브젝트 = {
            data : {
            함수 : **()=>** {
                console.log(this)
            }
        }
    }
        오브젝트.data.함수(); // window
```

상위 요소의 **`console.log(this)` 를 가져와 `window` 를 출력**

오브젝트 안에 함수 넣을 때 신문법

→ 콜론 쓸 필요 없이 그냥 쓰면됨

```jsx
함수 : **()**{
                console.log(this)
            }
```

함수나 변수를 전역공간에서 만들면 `{window}` 에 보관합니다.

`window.함수()` 해도 `window` 출력됨 (global object)

→ 오브젝트 내 함수안에서 쓰면 그 함수가 가지고 있는 오브젝트(window)를 뜻함

1.과 2.는 같은 개념임

**—> this는 나를 담고 있는 오브젝트를 출력한다.**

1. 기계 안에서 쓰면 새로 생성되는 오브젝트를 뜻함

→ 오브젝트 생성기계(construtor)

기계(constructor)에서 오브젝트 생산하는 법

```jsx
var 어쩌구 = {}

        function 기계(){
        **this.이름 = 'kim'** // 새로 생성되는 오브젝트(instance)
        }
        var 오브젝트 = new 기계();
				// 콘솔창에 '오브젝트' 입력하면 -> 기계 {이름: 'kim'}
```

1. this가 이벤트리스너 안에서는 e.currentTarget과 같음

```jsx
document.getElementById("버튼").addEventListener("click", function (e) {
  console.log(this); // 지금 이벤트가 동작하는 곳
  console.log(e.currentTarget); // 지금 이벤트가 동작하는 곳
});
```

→

![스크린샷 2022-03-03 오후 7.51.45.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc13dcf9-69e5-4972-bdb5-3f45aba7b246/스크린샷_2022-03-03_오후_7.51.45.png)

Case study 1

forEach 반복문 내에서 콜백함수를 쓴다면 this는?

```jsx
document.getElementById("버튼").addEventListener("click", function (e) {
  var 어레이 = [1, 2, 3];
  어레이.forEach(function (a) {
    // 함수안에 함수가 들어가는게 콜백함수
    console.log(a); // 내부 코드가 3번 반복
  });
});
```

![스크린샷 2022-03-03 오후 7.58.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dd2e415-9064-4485-8fd1-03cc9cb3aa4d/스크린샷_2022-03-03_오후_7.58.07.png)

```jsx
document.getElementById('버튼').addEventListener('click', function(e){

        var 어레이 = [1, 2, 3];
        어레이.forEach(function(a){
            console.log(**this**) //
        });
        })
```

![스크린샷 2022-03-03 오후 8.02.20.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2b893827-4dd1-4b04-9384-f0589fb1a36b/스크린샷_2022-03-03_오후_8.02.20.png)

→ 일반 함수에서는 window출력

Case study 1

오브젝트 내에서 콜백함수를 쓴다면 this는?

arrow function 특징 → 내부 this값을 변화시키지 않음 → 외부 this값을 그대로 씀

arrow function 안에서의 this?

```jsx
var 오브젝트 = {
            이름들 : ['김', '이', '박'],
            함수 : function(){
                    console.log(this)
                오브젝트.이름들.forEach(**function()**{
                    console.log(this)
                })
            }
        }
        오브젝트.함수();
```

![스크린샷 2022-03-03 오후 8.54.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9b61511e-9f98-4a82-87a5-99bcb4f1dcca/스크린샷_2022-03-03_오후_8.54.07.png)

```jsx
var 오브젝트 = {
            이름들 : ['김', '이', '박'],
            함수 : function(){
                    console.log(this)
                오브젝트.이름들.forEach(**()=>**{ // 애로우펑션 이용시 외부 this 값을 이용
                    console.log(this)
                })
            }
        }
        오브젝트.함수();
```

`funtion()` 대신 `()⇒` 썼을 때 외부 this값 (위에 있는 this) 이용 why? 함수 내부의 this값을 새로 바꿔주지 않기 때문에

![스크린샷 2022-03-03 오후 9.01.26.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d71262b0-83c9-478a-964e-acd3d94b437c/스크린샷_2022-03-03_오후_9.01.26.png)

## Arrow function

`function()` 대신 `()⇒` 사용 가능

함수를 만들때

1. 코드들을 기능으로 묶고 싶을 때 사용
2. 입출력 기계를 만들고 싶을 때 사용

```jsx
var 함수 = (a) => {
  return a + 10;
};
함수(5); // 15
```

`arrow function` 장점

1. 입출력 기계 만들 때 보기 쉬움
2. 소괄호 생략 가능(파라미터 1개 일때), 파라미터 여러개면 소괄호 써야함

`var 함수 = a => { return a + 10 }` 이렇게 작성 가능

1. 코드 한 줄이면 중괄호, return도 생략 가능

```jsx
var 함수 = (a) => a + 10;
```

arrow function 예시

1. forEach 콜백함수

```jsx
function 함수() {}
var 함수 = (a) => {
  return a + 10;
};
함수(5);
[1, 2, 3, 4].forEach((a) => console.log(a));
```

![스크린샷 2022-03-03 오후 11.13.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/22761ee7-2afa-4c37-bac7-d63717b1aa7f/스크린샷_2022-03-03_오후_11.13.51.png)

1. 이벤트 리스너

arrow function 특징 → 바깥에 있던 this 값을 내부에서 그대로 사용!

일단 이벤트리스너에서는 this == e.currentTarget

1. Object 안의 함수

```jsx
var 오브젝트 = {
  함수: () => {
    return this; // window
  },
};
오브젝트.함수();
```

→ 함수의 주인인 오브젝트가 출력되지 않음

why? this 값은 arrow function안에서는 변하지 않고 밖에 있던 this를 그대로 씀

## **this & arrow function 연습문제**

**1. 간단한 메소드 만들기**

**사람**이라는 오브젝트가 하나 있습니다.

이 오브젝트에 sayHi라는 함수를 (메소드를) 하나 추가하고 싶습니다.

```jsx
var 사람 = {
  name: "손흥민",
};

사람.sayHi(); //안녕 나는 손흥민
```

정답

```jsx
var 사람 = {
  name: "손흥민",
  sayHi: function () {
    console.log("안녕 나는 손흥민");
  },
};

사람.sayHi(); //안녕 나는 손흥민
```

이렇게 해도 되지만 실제 오브젝트 안에 있는 name 출력되면 좋음

```jsx
var 사람 = {
            name: '손흥민',
            sayHi : function() {
                console.log(**'안녕 나는' + this.name**)
            }
          }

          사람.sayHi(); //안녕 나는 손흥민
```

`[this.name](http://this.name)` 은 this가 포함된 오브젝트의 `name` 의 값이니까 `손흥민` 을 출력

→ arrow function으로하면

```jsx
var 사람 = {
            name: '손흥민',
            sayHi : **()=>** {
                console.log('안녕 나는' + this.name)
            }
          }

          사람.sayHi(); //**안녕 나는**
```

→ `손흥민` 이라는 글자가 사라짐 → arrow function 사용 불가!

**2. 오브젝트 내의 데이터를 전부 더해주는 메소드만들기**

오브젝트가 하나 있습니다.

```jsx
var 자료 = {
  data: [1, 2, 3, 4, 5],
};
```

그런데 이 오브젝트에 **전부더하기()** 라는 함수를 하나 만들어서 사용하고 싶습니다.

```jsx
var 자료 = {
  data: [1, 2, 3, 4, 5],
};
자료.전부더하기();
```

위처럼 자료.전부더하기()라고 쓰면 **자료.data** 안에 있는 모든 숫자를 더해서 콘솔창에 출력해주어야합니다.

(아마 15가 뜨게 되겠죠?)

**Q. 어떻게 코드를 짜면 될까요?**

**조건) 위에있는 자료라는 object 중괄호 {} 내에 코드 작성 금지**

`[this.data](http://this.data)` → `[1,2,3,4,5]`

합계 저장하는 변수 제작

→ 반복문이 돌 때마다 a값은 1,2,3,4,5 가 됨

→ 반복문 돌때마다 합계에 a를 더함

```jsx
var 자료 = {
  data: [1, 2, 3, 4, 5],
};

자료.전부더하기 = function () {
  // 오브젝트 밖에서 함수 제작
  var 합 = 0;
  this.data.forEach(function (a) {
    합 = 합 + a;
  });
  console.log(합); // 15
};
자료.전부더하기();
```

버튼 누르면 this.innerHTML 1초후에 출력하기

```jsx
<button id="버튼">버튼이에요</button>

<script>

  document.getElementById('버튼').addEventListener('click', function(){
    console.log(this.innerHTML)
  });

</script>
```

![스크린샷 2022-03-02 오후 6.21.57.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cebe1845-cdda-4a5c-968b-62d4bca93237/스크린샷_2022-03-02_오후_6.21.57.png)

`this` → 방금 클릭한 요소 → `document.getElementById(’버튼’)`

1초 후에 실행하려면 → `setTimeout`

→ 버튼 누르면 this.innerHTML을 1초후에 출력하기

```jsx
document.getElementById("버튼").addEventListener("click", function () {
  setTimeout(function () {
    console.log(this.innerHTML);
  }, 1000);
}); // undefined
```

→ this는 function안에서 맨날 바뀜 → 일반함수니까 this가 window가 나옴

→ arrow function 사용하면 해결됨

```jsx
document.getElementById('버튼').addEventListener('click', function(){
        setTimeout(**()=>** { console.log(this.innerHTML)}, 1000) // 버튼
```

→ this가 `document.getElementById('버튼')` 의미로 사용

## 변수 신문법 : var, let, const 선언, 할당, 범위

`var`

→ 재선언 O, 재할당 O, 범위 function

```jsx
var 이름 = "kim";
var 이름 = "park";
이름 = "chae"; // 재할당
```

→ `var 이름` → `이름 = 'kim'` , `이름 = 'park` → 할당

→ `var 이름 = 'kim'` 해놓고 `이름 = 'chae'` → 재할당

→ function안에서만 존재함

```jsx
function 함수() {
  var 이름 = "kim"; // function안에서만 존재
  이름;
}
이름; // 에러
```

`let`

→ 재선언 X, 재할당 O, 범위 중괄호

```jsx
let 나이 = 20;
let 나이 = 30; // 에러, 재선언 불가
```

```jsx
if (true) {
            let 이름 = 'park'
        }
        for(let v = 1){

        }
```

`const`

→ 재선언 X, 범위 중괄호

→ 변하지 않는 값(상수)

const로 오브젝트 만들었을 때 → 오브젝트에 재할당은 가능하지 않을까 ?

→ 오브젝트 내부값 변경해도 에러 안남!

```jsx
const 사람 = { 이름: "kim" };
사람.이름 = "park";
// 사람 -> {이름 : park}
```

변경 불가능한 오브젝트 만들고 싶다면?

```jsx
const 사람 = { 이름: "kim" };
Object.freeze(사람); // 오브젝트 값이 변하지 않음!
사람.이름 = "park"; // {이름: 'kim'}
```

## 변수 신문법 : hoisting, 전역변수, 참조

hoisting 현상

```jsx
function 함수() {
            var 이름 = 'kim';
        }
        if (true) {
            let 이름 = 'park'
        }
        **var 나이 = 30; // 선언과 할당**
```

자바스크립트는 `나이` 라는 변수 쓸 때

→ 위에 `나이` 를 선언하고, 아래에 `나이 = 30;` → 할당한다고 생각함

```jsx
**var 나이; // 선언**
        function 함수() {
            var 이름 = 'kim';
        }
        if (true) {
            let 이름 = 'park'
        }
        **나이 = 30; // 할당**
```

변수를 만나면 선언 부분을 강제로 맨위로 끌어올림 → 호이스팅

```jsx
console.log(나이); // undefined // 아직 변수 선언 안했는데 먼저 출력하면 에러 떠야하지만 여기서는 값을 출력

var 나이 = 30;

console.log(나이); // 30
```

전역변수 : 모든 곳에서 쓸 수 있는 변수

```jsx
var 나이 = 20; //전역변수

function 함수() {
  var 이름 = "kim"; // 지역변수
  console.log(나이);
}
함수();
```

window로 전역변수 만들기 → 전역 변수가 눈에 띄기 때문에 전역변수 만들 때 이 방법을 선호함

```jsx
var 나이 = 20;
window.이름 = "김";
console.log(이름);
```

예제)

```jsx
if (true) {
  let a = 1;
  var b = 2;
  if (true) {
    let b = 3;
  }
  console.log(b); // 2
}
```

→ 첫번째 if문 안은 `var b = 2;` 만 남고, 두번째 if문은 `let b = 3;` 가 중괄호 안에서 쓰이고 끝났기 때문에 외부에서 출력한 b 는 `2`가 된다.

## 연습문제

문제1

```jsx
함수();
function 함수() {
  console.log(안녕);
  let 안녕 = "Hello!";
}
```

→ 에러 출력

→ 함수 만들기 전에 `함수()` 써도됨

`let 안녕 = ‘hello’` 만들기도 전에 `‘안녕’`을 출력하라고 함 → 에러발생

`let 안녕` 은 `Hoisting` 이 됨 하지만, `let`과 `const`는 이런행위 금지 `undefined` 라는 값이 할당되지 X

`var` : `Hoisting`시 `undefined` 할당됨

`let`, `const` : `Hoisting`시 `undefined` 값이 할당X (temporal deadzone / uninitialized)

→ 그냥 빈 공간으로 있는 상태로 인식 → 에러 출력

문제2

```jsx
함수();
var 함수 = function () {
  console.log(안녕);
  var 안녕 = "Hello!";
};
```

→ 에러 출력 (함수가 아닌데요? 라는 에러, 함수가 아닌것에 소괄호를 치면 에러 출력 Why? 아직 할당되지않고 선언만 된 상태이기 때문에)

→ 함수 실행을 함수선언 전에 해도 됨

function 함수() {} : 전부가 Hoisting됨

var 함수 = Function() {} : 선언 부분만 Hoisting됨, 할당은 Hoisting되지 X

문제3

```jsx
let a = 1;
var 함수 = function () {
  a = 2;
};
console.log(a);
```

→ a는 1이 출력됨

a는 1이라는 변수를 만들고

→ 함수를 만들고 함수 안에서 a = 2라고 값을 변경

함수를 정의만 했지 **실행을 안시켜서** a = 2라는 부분은 없는 코드나 마찬가지

→ a 는 그냥 1

문제4

```jsx
let a = 1;
var b = 2; // 전역변수
window.a = 3;
window.b = 4;

console.log(a + b);
```

a는 1, b는 4가 출력

**b가** 4가 되는 이유는 `var b = 2` 와 `window.b = 4` 이 동일한 기능을 하는 코드이기 때문

→ b는 그냥 4로 재할당 되었다고 보면됨

**a는** let 변수로 1을 할당하고 글로벌 변수로 3을 할당

→ 이 경우 우리가 a를 사용했을 때 조금 더 **범위가 작고 가까운 1**을 참조해서 사용

(자바스크립트 변수를 사용할 때 참조할만한 변수가 내 주변에 없으면 계속 상위 중괄호로 시선을 돌리면서 참조함)

문제5

**콘솔창에 1초에 한번씩 1부터 5까지의 정수 출력**

저번 연습문제에서 setTimeout이라는 유용한 함수를 배운 것 같습니다.

그래서 코드를 이렇게 작성했습니다.

```jsx
setTimeout(function () {
  console.log(1);
}, 1000);
setTimeout(function () {
  console.log(2);
}, 2000);
setTimeout(function () {
  console.log(3);
}, 3000);
setTimeout(function () {
  console.log(4);
}, 4000);
setTimeout(function () {
  console.log(5);
}, 5000);
```

→ 반복문 축약

```jsx
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}
```

→ 5가 다섯번 출력됨

**Q. 해결할 방법은 ?**

```jsx
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}
```

내부 코드 → `setTimeout` X초후에 콜백함수 내의 `console.log(i)`를 실행해주세요~ 라는 코드

→ 그 부분은 **반복문과 동시에 실행되지 않음**

반복문을 해석한 후.. 1초가 지나면 setTimeout 내의 console.log(i)가 발동

but, i를 채워넣고싶어서 주변을 살펴보았더니 i값은 5밖에 없음

why? → 아까 반복문이 5번 실행되면서 i값은 0,1,2,3 ... 이렇게 차례로 변하다가 i값이 5가 되어 종료됨

그리고 i 값은 var로 만든 전역변수 → i값을 쓰려고 봤더니 전역변수 i = 5밖에 없어서 5를 집어넣어서 계속 실행해서 콘솔창에 5가 계속 출력

해결책은 for 반복문에서 i변수를 만들 때 `var` 대신 `let`으로 바꾸는 것!

let 변수는 범위가 중괄호이기 때문에 `for 반복문도 중괄호`에 해당됨

→ 1초 후 console.log(i)가 실행될 때 i값을 채우려고 살펴보면

i값이 for 반복문 내에 남아있기 때문에 그걸 가져다 쓰게됨

그래서 아까처럼 계속 5를 출력해주는게 아니라 1,2,3,4,5를 출력

(위의 예제는 0,1,2,3,4가 출력)

**6. 버튼을 누르면 모달창을 띄우기 (이벤트리스너 반복시키기)**

```jsx
<div style="display : none">모달창0</div>
<div style="display : none">모달창1</div>
<div style="display : none">모달창2</div>

<button>버튼0</button>
<button>버튼1</button>
<button>버튼2</button>

<script>
//?
</script>
```

0번째 버튼을 누르면 0번째 모달창,

1번째 버튼을 누르면 1번째 모달창을 보여주기

```jsx
<div style="display : none">모달창0</div>
<div style="display : none">모달창1</div>
<div style="display : none">모달창2</div>

<button>버튼0</button>
<button>버튼1</button>
<button>버튼2</button>

var 버튼들 = document.querySelectorAll('button');
var 모달창들 = document.querySelectorAll('div');

버튼들[0].addEventListener('click', function(){
  모달창들[0].style.display = 'block';
});

버튼들[1].addEventListener('click', function(){
  모달창들[1].style.display = 'block';
});

버튼들[2].addEventListener('click', function(){
  모달창들[2].style.display = 'block';
});

```

`document.querySelectorAll`은 `jQuery의 $('')` 셀렉터와 매우 유사합니다. 동시에 여러 요소를 찾아 어레이 비슷한 자료형에 담아줌

0번째 버튼을 누르면 0번째 모달창,

1번째 버튼을 누르면 1번째 모달창을 보여줌

→ 반복문 안에 담아서 한번 다시 개발

```jsx
var 버튼들 = document.querySelectorAll("button");
var 모달창들 = document.querySelectorAll("div");

for (var i = 0; i < 3; i++) {
  버튼들[i].addEventListener("click", function () {
    모달창들[i].style.display = "block";
  });
}
```

**Q. 위 코드는 왜 의도대로 동작하지 않는 것이죠? 해결할 방법은 무엇일까요?**

→ 방금 전 문제랑 거의 똑같은 경우의 문제

```jsx
for (var i = 0; i < 3; i++) {
  버튼들[i].addEventListener("click", function () {
    모달창들[i].style.display = "block";
  });
}
```

내부 코드는 addEventListener, 클릭 되면 콜백함수 내의 **`모달창들[i].style.display = 'block';`** 을 실행해주세요~ 라는 코드임

→ 그 부분은 **반복문과 동시에 실행되지 X**

누군가 버튼을 클릭하면 addEventListener 내의 **`모달창들[i].style.display = 'block';`**코드가 발동됨

but, i를 쓰고싶어서 주변을 살펴보았더니 i값은 3밖에 없음

why? → 아까 반복문이 3번 실행되면서 i값은 0,1,2,3 ... 이렇게 차례로 변하다가 i값이 3이 되어 종료

i 값은 var로 만든 전역변수 → i값을 쓰려고 봤더니 **전역변수 i = 3밖에 없어서 3을 집어넣어서 계속 에러발생**

해결책은 for 반복문에서 i변수를 만들 때 `var` 대신 `let`으로 바꾸는 것!!

반복문이 돌고 나서도 let i = 어쩌구 값이 {for 반복문} 내에 남아있기 때문에 그걸 **`모달창들[i].style.display = 'block';`** 의 i값으로 가져다 쓰게 됨

## template literals(strings)

문자열을 다르게 제작할 수 있는 ES6 방법

backquote(백틱) 문자열의 장점 :

1. 엔터키 기능 (그냥 따옴표는 엔터키 치면 문자열 깨짐)

```jsx
var 문자 = `손흥민
        ㅁㄴㅇㅁㅇㄴ
        ㅁㄴㅇㅁㅇ
        `; // backtick
```

1. 중간에 변수 넣기 쉬움

이전 방식 → ‘문자' + 변수

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = "안녕하세요 저는 " + 변수;
console.log(문자);
```

→ ES6 방식 `문자 ${변수}`

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 저는 `;
console.log(문자); // 안녕하세요 손흥민 저는
```

→ 특히 HTML 작성시 유용함

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 저는 `;
var 템플릿 = `<div>
엔터키를
자유롭게 
사용할 수
있음
</div>`;
```

backquote 문자열 + 함수

tagged literal

→ `함수()` 대신, 문자열 붙여서 실행할 수 있음

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 입니다 `;
function 함수() {
  return 10;
}
console.log(함수`안녕하세요 ${변수} 입니다 `); // 10
```

→ `문자`를 해체 분석할 수 있음

ex) 단어 순서 변경, 단어 제거 ${변수} 위치 변경...

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 입니다 `;
function 해체분석기(문자들, 변수들) {
  console.log(문자들); // [ '안녕하세요 ', ' 입니다 ' ]
  console.log(변수들); // 손흥민
}
해체분석기`안녕하세요 ${변수} 입니다 `;
```

=

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 입니다 `;
function 해체분석기(a, b) {
  console.log(a); // [ '안녕하세요 ', ' 입니다 ' ]
  console.log(b); // 손흥민
}
해체분석기`안녕하세요 ${변수} 입니다 `;
```

해체분석기 파라미터1. 문자들을 Array화 해줌

해체분석기 파라미터2. ${변수}를 뜻함

→ 중괄호를 기준으로 해체함!

ex) 글자 순서를 변경하고 싶을 때

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 입니다 `;
function 해체분석기(문자들, 변수들) {
  console.log(문자들[1] + 변수들 + 문자들[0]); // 입니다 손흥민안녕하세요
}
해체분석기`안녕하세요 ${변수} 입니다 `;
```

Q1. 문자 중간 ‘양말’과 ‘바지’ 단어 순서를 바꾸고 싶음

→ 해체 분석기 이용할 것

```jsx
var pants = 20;
var socks = 100;
`바지${pants} 양말${socks}`;
function 해체분석기(문자들, 변수들1, 변수들2) {
  // 변수 2개면 파라미터 2개
  console.log(문자들[1] + 변수들1 + 문자들[0] + 변수들2); // 양말20바지100
}
해체분석기`바지${pants} 양말${socks}`;
```

Q2.문자가 있음

→ pants가 0개이면 ‘바지 안팔아요 양말100’이라는 문자로 바꾸는 해체분석기 제작

```jsx
var pants = 0;
var socks = 100;
`바지${pants} 양말${socks}`;
function 해체분석기(글자들, 변수들1, 변수들2) {
  if (변수들1 == 0) {
    console.log(`바지다팔렸어요 양말` + 변수들2);
  }
}
해체분석기`바지${pants} 양말${socks}`;
```

### Spread Operator

`...` → spread operator : 펼쳐놓고 싶을 때 사용

1. Array에 붙이면 대괄호를 제거해줌

```jsx
var 어레이 = ["hello", "world"];
console.log(어레이); // [ 'hello', 'world' ]

var 어레이 = ["hello", "world"];
console.log(...어레이); // hello world
```

1. 문장 붙이면 펼쳐줌

```jsx
var 문자 = "hello";
console.log(...문자); // h e l l o
```

spread operator 사용처

1. 어레이 합치기/복사

```jsx
var a = [1, 2, 3];
var b = [4, 5];
var c = [...a, ...b];
console.log(c); // [ 1, 2, 3, 4, 5 ]
```

→ Deep Copy 할 때 유용함

reference data type (Array, Object)

```jsx
var 어레이 = ["hello", "world"];

var a = [1, 2, 3];
var b = a; // a에 있는 값을 b에 복사하고 싶음 -> a를 할당함, 등호로 복사하면 값을 공유함
a[3] = 4;

console.log(a); // [ 1, 2, 3, 4 ]
console.log(b); // [ 1, 2, 3, 4 ] -> b에 직접 값을 수정한 적이 없는데 4가 추가됨
```

→

```jsx
var a = [1, 2, 3];
var b = [...a]; // a에 있는 값을 b에 복사하고 싶음 -> a를 할당함, 등호로 복사하면 값을 공유함
a[3] = 4;

console.log(a); // [ 1, 2, 3, 4 ]
console.log(b); // [ 1, 2, 3 ]-> b는 바뀌지 않음(독립적인 자료) -> Deep copy
```

1. 오브젝트 합치기

var o2 만들때 o1에 있던거 그대로 넣고 싶음

spread operator

대괄호 벗기기, 중괄호 벗기기 둘다 OK

```jsx
var o1 = { a: 1, b: 2 };
var o2 = { ...o1, c: 3 };
console.log(o2); // { a: 1, b: 2, c: 3 }
```

o1을 o2에 deep copy하려면 → 카피하다가 값 중복 일어나면 → 가장 뒤에 있는걸 적용

```jsx
var o1 = { a: 1, b: 2 };
var o2 = { a: 2, ...o1 };
console.log(o2); // { a: 1, b: 2 }
```

`...` → 중괄호, 대괄호, 소괄호 안에서만 사용 가능!

1. 함수에 파라미터 넣을 때

```jsx
function 더하기(a, b, c) {
  console.log(a + b + c);
}
더하기(1, 2, 3);
// array 내의 모든 데이터를 파라미터로 집어 넣고 싶은 경우
var 어레이 = [10, 20, 30];
더하기(어레이[0], 어레이[1], 어레이[2]);
```

→ array 해체작업 너무 번거로움

```jsx
function 더하기(a, b, c) {
  console.log(a + b + c);
}
더하기(1, 2, 3); // 6
// array 내의 모든 데이터를 파라미터로 집어 넣고 싶은 경우
var 어레이 = [10, 20, 30];
더하기(어레이[0], 어레이[1], 어레이[2]); // 60 //주먹구구식

더하기.apply(undefined, 어레이); // 60 // 옛날방식
더하기(...어레이); // 60 //요즘방식
```

apply 함수 개념설명

```jsx
var person = {
  인사: function () {
    console.log("안녕");
  },
};
person.인사(); // 안녕

var person2 = {
  name: "손흥민",
};
```

→ 위의 `인사 : function(){}` 함수를 `person2` 에도 적용하고 싶음

→ `person.인사()` 를 `person2` 에 적용하고 싶을 때 apply사용

```jsx
var person = {
  인사: function () {
    console.log("안녕");
  },
};
person.인사(); // 안녕

var person2 = {
  name: "손흥민",
};

**person.인사.apply(person2);** // 안녕
```

```jsx
var person = {
  인사: function () {
    console.log(this.name + "안녕");
  },
};
person.인사(); // undefined안녕

var person2 = {
  name: "손흥민",
};

person.인사.apply(person2); // 손흥민안녕
```

→ `apply()` → 그냥 함수를 옮겨와서 실행해주세요!

`apply` / `call` → 비슷함!

→ but 파라미터 실행할 때 차이가 있음

`person.인사.apply(person2, [1,2]);` = `person.인사(1)`

`person.인사.call(person2, 1);` = `person.인사(1)`

차이점은 apply는 array형태로 집어넣기 가능 (기능은 call함수와 같음)

→ 상속기능 구현할 때 많이 사용!

## **자바스크립트 함수 업그레이드하기**

자바스크립트 언어 특징

→ 파라미터 2개 들어가는 함수인데 1개만 써도 에러가 안남 → `NaN` 출력

```jsx
function 더하기(a, b) {
  console.log(a + b);
}
더하기(1); // NaN
```

함수의 default 파라미터 → 파라미터 집어 넣지 않으면 그냥 디폴트로 집어 넣어줄 값을 표기할 수 있음

```jsx
function 더하기(a, b = 10) {
  console.log(a + b);
}
더하기(1); // 11
더하기(1, 2); // 3
```

→ b 자리에 아무 것도 없으면 10을 넣어주세요 ~ (함수의 default 파라미터)

`10` 대신 `2 * 5`, `2 * a` 등 연산자가 포함된 값도 가능!, `함수()` 도 가능!

```jsx
function 임시함수() {
  return 10;
}

function 더하기(a, **b = 임시함수()**) {
  console.log(a + b);
}
더하기(1); // 11
```

함수의 arguments

모든 파라미터를 한꺼번에 다루고 싶을 경우

→ `arguments` 사용

```jsx
function 함수(a, b, c) {
  console.log(arguments[0]);
}
함수(1, 2, 3); // 1
```

입력한 파라미터를 전부 콘솔창에 출력해주는 함수?

```jsx
function 함수(a, b, c) {
  for (
    var i = 0;
    i < arguments.length;
    i++ // 파라미터 개수만큼 반복문 돌리기
  )
    console.log(arguments[i]);
}
함수(2, 3, 4); // 2 3 4
```

## Rest 파라미터

1. spread operator

```jsx
function 함수2(...파라미터들) {
  console.log(파라미터들);
}

함수2(1, 2, 3, 4, 5, 6, 7);
/*
[
  1, 2, 3, 4,
  5, 6, 7
]
*/
```

이 자리에 오는 모든 파라미터를 []에 보관 해줌

arguments → 모든 파라미터를 []에 담아줌

`rest` parameter → `이 자리에 오는` 모든 파라미터를 []에 담아줌

→

```jsx
function 함수2(**a, b, ...파라미터들**) {
  console.log(파라미터들);
}

함수2(1, 2, 3, 4, 5, 6, 7); // [ 3, 4, 5, 6, 7 ]
```

a랑 b를 쓰고 그 뒤에 있는 파라미터를 array에 담아주세요 (arguments와 가장 큰 차이점)

Q.모든 파라미터들을 하나씩 콘솔창에 출력해주는 함수

→ 심플한 방법

```jsx
function 함수2(...rest) {
  console.log(rest[0]);
  console.log(rest[1]);
  console.log(rest[2]);
  console.log(rest[3]);
}

함수2(1, 2, 3, 4); // 1 2 3 4
```

```jsx
function 함수2(...rest) {
  for (var i = 0; i < rest.length; i++) {
    console.log(rest[i]);
  }
}

함수2(1, 2, 3, 4, 231, 32, 23, 12);
/*
1
2
3
4
231
32
23
12
*/
```

→ rest는 파라미터 몇개 들어올지 미리 지정 안해줘도 됨

주의점

→

1. rest 파라미터는 마지막에 써야함!

`function 함수2(...rest, a)` → 불가능!

1. 두번 이상 사용 금지

`function 함수2(...rest, ...rest2)` → 불가능!

## **Spread, rest 파라미터 연습문제 8개**

**1. spread 문제 1**

```jsx
var a = [1, 2, 3];
var b = "김밥";
var c = [...b, ...a];
console.log(c);
```

`['김', '밥', 1, 2, 3 ]` 이라는 array가 출력

글자를 spread → 한글자씩 콤마로 분열

array를 spread → 대괄호를 제거

**2. spread 문제 2** ⭐

```jsx
var a = [1, 2, 3];
var b = ["you", "are"];
var c = function (a, b) {
  console.log([[...a], ...[...b]][1]);
};
c(a, b);
```

c라는 함수에 a와 b라는 자료를 집어넣어서 실행

→ `[ [...a], ...[...b] ][1]`, 여기서 a와 b를 집어넣어보면

→ `[ [1,2,3], ...['you', 'are'] ][1]` , spread를 해치워버리면

→ `[ [1,2,3], 'you', 'are' ][1]`

→ `'you'`라는 글자가 콘솔창에 뜸

**3. default 파라미터 문제 1**

```java
function 함수(a = 5, b = a * 2 ){
  console.log(a + b);
  return 10
}
함수(3);
```

→ b라는 파라미터는 default 파라미터가 발동해서 `a * 2` 라는 값을 가지게 됨

→ a는 3, b는 6

`9`가 출력

**4. default 파라미터 문제 2**

```jsx
function 함수(a = 5, b = a * 2) {
  console.log(a + b);
}
함수(undefined, undefined);
```

함수에 파라미터를 입력하지 않았을 경우 그 파라미터를 출력해보면 `undefined`가 출력됨

```jsx
function 함수(a) {
  console.log(a);
}

함수();
```

이 코드의 실행결과는 `undefined`

자바스크립트 함수에서는 파라미터를 집어넣지 않았을 경우 파라미터가 자동으로 `undefined`가 됨

그럼 일부러 파라미터로 `undefined`를 입력하면?

→ 그냥 파라미터를 입력하지 않은 것과 동일

→ `default 파라미터`가 발동되어 `15` 출력

**5. array를 만들어주는 함수 제작**

파라미터로 자료들을 입력하면 그걸 그대로 array를 만들어주는 함수를 만들기

```jsx
function 어레이(){
  (여기 어떤코드가 들어가면 될까요?)
}

var newArray = 어레이(1,2,3,4,5);
console.log(newArray);
```

→ `[1,2,3,4,5]`가 출력되려면 어레이라는 함수를 어떻게 만들면 될까요? (new 키워드 사용금지)

파라미터를 `전부 array안에 담아주는 방법` 이용

`rest` 파라미터를 이용 → 들어온 파라미터를 전부 어레이화 해서 출력하기 때문에

```jsx
function 어레이(**...rest**){
  return rest
}

var newArray = 어레이(1,2,3,4,5);
console.log(newArray); // [1,2,3,4,5]
```

**6. 최댓값 구하기**

자바스크립트에서 최댓값 구할 때 `Math.max()`라는 기본 내장함수를 쓸 수 있음

```jsx
Math.max(5, 6, 4, 3); // 6
```

→ `6`이라고 최댓값을 출력

최댓값을 검사하고 싶은 숫자들이 많을 때

```jsx
var numbers = [2, 3, 4, 5, 6, 1, 3, 2, 5, 5, 4, 6, 7];
```

numbers 안에 있는 숫자들을 Math.max()에 집어넣어서 쓰면 → 직접 소괄호 안에 10개넘는 숫자를 손수 기입해야함

Math.max() 안에 array 안의 모든 데이터를 담고싶으면

array를 풀어헤쳐서 집어넣으면 됨

```jsx
var numbers = [2,3,4,5,6,1,3,2,5,5,4,6,7];

console.log( Math.max(**...numbers**) );
```

이렇게 작성하면 array데이터들 중에서 최댓값을 구함

**7. 글자를 알파벳순으로 정렬해주는 함수 만들기**

자바스크립트는 array 내의 데이터를 알파벳순으로 정렬하고 싶을 때

→ `sort()`라는 array 내장함수를 붙여 사용 (array에만 적용 가능)

```jsx
console.log(["b", "c", "a"].sort());

//[ 'a', 'b', 'c' ] 출력됨
```

`sort()` 만 붙이면 쉽게 정렬이 가능

but 우리는 **array가 아니라 문자열에도** 적용할 수 있는 알파벳순 정렬함수를 하나 만들고 싶음

```jsx
function 정렬(){
  (여기 어떤 코드가 들어가야할까요?)
}

정렬('bear');
```

정렬('bear')라고 사용하면

콘솔창에 a b e r 이렇게 입력한 문자를 알파벳 순으로 출력되게 만들고 싶으면? (sort() 함수 사용가능)

sort는 안 array에만 붙일 수 있음.

그럼 그냥 문자를 array화 시켜버리면 sort함수 사용 가능!

→ bear라는 문자를 ['b', 'e', 'a', 'r'] 이렇게 array에 담아서 알파벳을 정렬

```jsx
function 정렬(글자) {
  console.log([...글자].sort());
}

정렬("bear"); // [ 'a', 'b', 'e', 'r' ]
```

→ 여기서 대괄호 벗기고 싶다면

→

```jsx
function 정렬(글자) {
  console.log(...[...글자].sort());
}

정렬("bear"); // a b e r
```

**8. 데이터마이닝 기능 만들기**

알파벳들의 출현 갯수를 세어주는 함수

**`글자세기('aacbbb')`** 라고 입력하면 콘솔창에

**`{ a : 2, b : 3, c : 1 }`**

→ 이렇게 출력해주는 글자세기() 라는 함수를 만들기

→ 입력한 단어에 들어있는 알파벳의 갯수를 세어서 오브젝트에 기록해주고 출력까지 해주는 함수

→ 글자에다가 반복문을 돌려서 해결 가능!

그냥 반복문을 써도 되고 조금 더 간단하게 사용하려면 `forEach()` 반복문을 쓸 수 있음

but, `forEach()`는 `array에만` 붙일 수 있는 함수

글자에 붙이려면.. `글자를 array화` → `[...글]` (해체하고 대괄호)

→ `‘abc’` → `[ 'a', 'b', 'c’ ]` 로 바뀜 (array로 바뀜)

```jsx
function 글자세기(글){
  var 결과 = {}; // 결과는 오브젝트로 출력되어야 함
  **[...글]**.forEach(function(a){  });
}

```

그래서 함수안에 글자를 집어넣으면 spread를 이용해서 하나하나의 알파벳들을 array에 저장

그리고 거기에 forEach 반복문을 돌림

→ 글자안에있던 하나하나의 알파벳들 갯수 만큼 반복문이 돌게 되고,

반복문이 돌면서 a라는 값은 **하나하나의 알파벳**이 됨

→ 이제 하나하나의 알파벳만큼 반복문이 돌게 되니 반복문 안에다가 기능개발하면 됨

결과라는 object에 **결과[a]** (결과.a) 라는 항목이 있으면 값을 1을 더해주고

없으면 1로 등록해주세요~ (a : 1 이렇게) 라고 코드작성

```jsx
function 글자세기(글) {
  var 결과 = {};
  [...글].forEach(function (a) {
    if (결과[a] > 0) {
      결과[a]++;
    } else {
      결과[a] = 1;
    }
  });
  console.log(결과);
}
글자세기("ddqdsqeqt"); // { d: 3, q: 3, s: 1, e: 1, t: 1 }
```

(결과[a]는 오브젝트 내에서 데이터를 뽑는 법)

## **Reference data type**

그냥 숫자와 문자는 → Primitive data type : 변수에 값이 그대로 저장됨

```jsx
var 변수 = 1234;
var 어레이 = [1, 2, 3];
var obj = { name: "kim" };
```

→ Array, Object는 변수에 값이 저장되지 X

→ 변수에 reference가 저장됨

reference → `[1,2,3]` 이 저쪽에 있다고 가리키는 화살표

primitive data type 다루기 : 복사

```jsx
var 이름1 = "김";
var 이름2 = 이름1;
이름1 = "박";

console.log(이름1); // 박
console.log(이름2); // 김 // 할당하고 바꾼적이 없기 때문에
```

reference data type 다루기 : 복사

```jsx
var 이름1 = { name: "김" };
var 이름2 = 이름1;
이름1.name = "박";
console.log(이름1); // { name: '박' }
console.log(이름2); // { name: '박' } // 바꾼적이 없는데 '박'으로 바뀌어 있음
```

→ 이름1에 직접 `{ name: '박' }` 저장 되는 것이 아님!

`{ name: '김' }` 이 저기 있다는 화살표(reference)가 저장됨

`이름1`에는 오브젝트가 들어가 있는게 아니라 화살표가 들어있음 → `var 이름2 = 이름1;` 은
화살표를 복사한 것임 → 중괄호 생성할 때마다 화살표 만드는 것임

→ array, object 함부로 복사하면 안됨!

→ 오브젝트 복사 기계를 이용해서 복사함

ex)

```jsx
var 이름1 = { name: "김" };
var 이름2 = { name: "김" };
이름1 == 이름2; // flase
이름1 === 이름2; // flase
```

→ 각각 다른 화살표이기 때문에 다른 자료를 가리킴

오브젝트를 변경해주는 함수

```jsx
var 이름1 = { name: "김" };

function 변경(obj) {
  obj.name = "park";
}
변경(이름1);
console.log(이름1); // { name: 'park' }
```

값이 변경됨

오브젝트를 재할당해주는 함수

→ 오브젝트 변경말고 재할당 → 값이 변경되지 X

why? → 파라미터는 변수생성 & 할당과 같음! `var = obj` 와 같은 개념

```jsx
var 이름1 = { name: "김" };

function 변경(obj) {
  obj = { name: "park" };
}
변경(이름1);
console.log(이름1); // { name: '김' }
```

`변경(이름1);` 은 `변경(var obj = 이름1);` 와 같음

→ `var obj = {name: '김'}`

→ 이 변수에다가 새로운 오브젝트 `{ name: "park" };` 할당

→ `var obj = { name: "park" };` , 이름1은 그대로 `var 이름1 = { name: "김" };`

## **객체지향1. Object 생성기계인 constructor**

constructor 문법의 용도

→ object를 마구 복사하고 싶을 때 사용! (object 생성 기계)

예시) 출석부를 만든다고 가정

constructor

```jsx
var 사람 = { name: "kim", age: 15 };
function Student() {
  // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
  this.name = "kim";
  this.age = 15;
}
```

→ object 마구 뽑기 가능

→ 기계 사용하려면 `this` 라는 키워드가 필요함

→ this는 새로 생성되는 object를 뜻함 → `this.name = 'kim'` 은 새로 생성되는 오브젝트의 name 속성에 ‘kim’이라는 값을 대입

→

```jsx
var 사람 = { name: "kim", age: 15 };
function Student() {
  // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
  this.name = "kim";
  this.age = 15;
}

var 학생1 = new Student();
console.log(학생1); // Student { name: 'kim', age: 15 }
```

Q 기계로 생성되는 모든 학생 object에 `sayHi()` 함수 추가하고 싶다면?

```jsx
var 학생1 = {
  name: "kim",
  age: 15,
  sayHi: function () {
    console.log("안녕하세요 " + this.name + "입니다");
  },
};

학생1.sayHi(); // 안녕하세요 kim입니다

function Student() {
  // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
  this.name = "kim";
  this.age = 15;
}

var 학생1 = new Student();
```

→ 하드코딩말고 기계로 생성되는 모든 학생 object에 `sayHi()` 함수 추가하고 싶다면?

학생1, 학생2에 모두 복사

```jsx
function Student(){ // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
this.name = 'kim';
this.age = 15;
**this.sayHi = function(){
    console.log('안녕하세요 ' + this.name + '입니다')**
}
}

var 학생1 = new Student();
var 학생2 = new Student();

학생1.sayHi(); // 안녕하세요 kim입니다
학생2.sayHi(); // 안녕하세요 kim입니다
```

문제점 → `학생1` 이랑 `학생2` 의 name을 다르게 설정하고 싶을 때 → 파라미터 사용

```jsx
function Student(**이름**){ // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
this.name = **이름**;
this.age = 15;
this.sayHi = function(){
    console.log('안녕하세요 ' + this.name + '입니다')
}
}

var 학생1 = new Student(**'park'**); // 안녕하세요 park입니다
var 학생2 = new Student(**'chae'**); // 안녕하세요 chae입니다

학생1.sayHi();
학생2.sayHi();
```

this : 기계에서 새로 생성되는 object → `instance`

기계 : object 생성기계(constructor, 생성자)

과제

**Q2. 상품마다 부가세() 라는 내부 함수를 실행하면 콘솔창에 상품가격 \* 10% 만큼의 부가세금액이 출력되도록 하고 싶으면**

**constructor를 어떻게 수정해야할까요?**

예를 들면 product1.부가세() 이렇게 쓰면 콘솔창에 5000이 출력되어야합니다.
