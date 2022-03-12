## this 키워드

```jsx
console.log(this) // Window

function 함수(){
this  // Window
}
```

this 키워드는 뜻이 3 ~ 4개 정도 됨

1. 그냥 쓰거나 일반 함수 안에서 쓰면 `{window}` , strict mode + 일반 함수 내에서 쓰면 `undefined`

```jsx

        'use strict';  // 자바스크립트를 엄격하게 실행
```

ex) `x = 300;` → 평상시에는 가능하지만 `use strict` 모드 에서는 사용 불가 `var x = 300;` 이렇게 해야함! 

```jsx

        'use strict';  // 자바스크립트를 엄격하게 실행
        console.log(this) 
        function 함수(){ 
            console.log(this) 
        }
        함수() // undefined
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
document.getElementById('버튼').addEventListener('click', function(e){
            console.log(this); // 지금 이벤트가 동작하는 곳
            console.log(e.currentTarget); // 지금 이벤트가 동작하는 곳
        })
```

→

![스크린샷 2022-03-03 오후 7.51.45.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc13dcf9-69e5-4972-bdb5-3f45aba7b246/스크린샷_2022-03-03_오후_7.51.45.png)

Case study 1

forEach 반복문 내에서 콜백함수를 쓴다면 this는?

```jsx
document.getElementById('버튼').addEventListener('click', function(e){
        var 어레이 = [1, 2, 3];
        어레이.forEach(function(a){ // 함수안에 함수가 들어가는게 콜백함수
            console.log(a) // 내부 코드가 3번 반복
        });
        })
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
var 함수 = (a) =>  { return a + 10 }
        함수(5); // 15
```

`arrow function` 장점

1. 입출력 기계 만들 때 보기 쉬움
2. 소괄호 생략 가능(파라미터 1개 일때), 파라미터 여러개면 소괄호 써야함 

`var 함수 = a =>  { return a + 10 }` 이렇게 작성 가능 

1. 코드 한 줄이면 중괄호, return도 생략 가능

```jsx
var 함수 = a =>  a + 10 
```

arrow function 예시 

1. forEach 콜백함수

```jsx
function 함수() {

        }
        var 함수 = (a) =>  { return a + 10 }
        함수(5);
        [1,2,3,4].forEach(a => console.log(a))
```

![스크린샷 2022-03-03 오후 11.13.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/22761ee7-2afa-4c37-bac7-d63717b1aa7f/스크린샷_2022-03-03_오후_11.13.51.png)

1. 이벤트 리스너

arrow function 특징 → 바깥에 있던 this 값을 내부에서 그대로 사용!

일단 이벤트리스너에서는 this == e.currentTarget

1. Object 안의 함수

```jsx
var 오브젝트 = {
            함수 : ()=>{
                return this // window
            }      
        }
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
  name: '손흥민',
}

사람.sayHi(); //안녕 나는 손흥민
```

정답

```jsx
var 사람 = {
            name: '손흥민',
            sayHi : function() {
                console.log('안녕 나는 손흥민')
            }
          }
          
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

→  `손흥민` 이라는 글자가 사라짐 → arrow function 사용 불가!

**2. 오브젝트 내의 데이터를 전부 더해주는 메소드만들기**

오브젝트가 하나 있습니다.

```jsx
var 자료 = {
  data : [1,2,3,4,5]
}
```

그런데 이 오브젝트에 **전부더하기()** 라는 함수를 하나 만들어서 사용하고 싶습니다.

```jsx
var 자료 = {
  data : [1,2,3,4,5]
}
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
            data : [1,2,3,4,5]
          }

          자료.전부더하기 = function(){ // 오브젝트 밖에서 함수 제작
            var 합 = 0;
            this.data.forEach(function(a){
                합 = 합 + a
            })
            console.log(합) // 15
          }
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

1초 후에 실행하려면 →  `setTimeout`

→ 버튼 누르면 this.innerHTML을 1초후에 출력하기 

```jsx
document.getElementById('버튼').addEventListener('click', function(){
        setTimeout(function() { console.log(this.innerHTML)}, 1000)
})// undefined
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
	var 이름 = 'kim'; 
  var 이름 = 'park'
이름 = 'chae' // 재할당 
```

→ `var 이름` →  `이름 = 'kim'` , `이름 = 'park` → 할당

→  `var 이름 = 'kim'` 해놓고 `이름 = 'chae'` → 재할당 

→ function안에서만 존재함

```jsx
function 함수() {
            var 이름 = 'kim'; // function안에서만 존재
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
const 사람 = {이름 : 'kim'}
사람.이름 = 'park'
// 사람 -> {이름 : park}
```

변경 불가능한 오브젝트 만들고 싶다면?

```jsx
const 사람 = {이름 : 'kim'}
Object.freeze(사람) // 오브젝트 값이 변하지 않음!
사람.이름 = 'park' // {이름: 'kim'} 

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
            var 이름 = 'kim'; // 지역변수
            console.log(나이)
        }
        함수();
```

window로 전역변수 만들기 → 전역 변수가 눈에 띄기 때문에 전역변수 만들 때 이 방법을 선호함

```jsx
var 나이 = 20;
        window.이름 = '김'
        console.log(이름);
```

예제)

```jsx
if (true){
            let a = 1;
            var b = 2;
            if (true){
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
  let 안녕 = 'Hello!';
}
```

→ 에러 출력

→ 함수 만들기 전에 `함수()` 써도됨  

`let 안녕 = ‘hello’` 만들기도 전에 `‘안녕’`을 출력하라고 함 → 에러발생

`let 안녕` 은 `Hoisting` 이 됨 하지만, `let`과 `const`는 이런행위 금지 `undefined` 라는 값이 할당되지 X

`var` : `Hoisting`시 `undefined` 할당됨

`let`, `const` : `Hoisting`시 `undefined` 값이 할당X (temporal deadzone / uninitialized)

→  그냥 빈 공간으로 있는 상태로 인식 → 에러 출력

문제2

```jsx
함수();
var 함수 = function() {
  console.log(안녕);
  var 안녕 = 'Hello!';
}
```

→ 에러 출력 (함수가 아닌데요? 라는 에러, 함수가 아닌것에 소괄호를 치면 에러 출력 Why? 아직 할당되지않고 선언만 된 상태이기 때문에)

→ 함수 실행을 함수선언 전에 해도 됨

function 함수() {} : 전부가 Hoisting됨

var 함수 = Function() {} : 선언 부분만 Hoisting됨, 할당은 Hoisting되지 X

문제3

```jsx
let a = 1;
var 함수 = function() {
  a = 2;
}
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

**b가** 4가 되는 이유는 `var b = 2` 와 `window.b = 4`  이 동일한 기능을 하는 코드이기 때문

→ b는 그냥 4로 재할당 되었다고 보면됨

**a는** let 변수로 1을 할당하고 글로벌 변수로 3을 할당

→ 이 경우 우리가 a를 사용했을 때 조금 더 **범위가 작고 가까운 1**을 참조해서 사용

(자바스크립트 변수를 사용할 때 참조할만한 변수가 내 주변에 없으면 계속 상위 중괄호로 시선을 돌리면서 참조함)

문제5

 **콘솔창에 1초에 한번씩 1부터 5까지의 정수 출력**

저번 연습문제에서 setTimeout이라는 유용한 함수를 배운 것 같습니다.

그래서 코드를 이렇게 작성했습니다.

```jsx
setTimeout(function() { console.log(1); }, 1000 );
setTimeout(function() { console.log(2); }, 2000 );
setTimeout(function() { console.log(3); }, 3000 );
setTimeout(function() { console.log(4); }, 4000 );
setTimeout(function() { console.log(5); }, 5000 );
```

→ 반복문 축약

```jsx
for (var i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i*1000 );
}
```

→ 5가 다섯번 출력됨

**Q. 해결할 방법은 ?**

```jsx
for (var i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i*1000 );
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

var 버튼들 = document.querySelectorAll('button');
var 모달창들 = document.querySelectorAll('div');

for (var i = 0; i < 3; i++){

  버튼들[i].addEventListener('click', function(){
    모달창들[i].style.display = 'block';
  });

}

```

**Q. 위 코드는 왜 의도대로 동작하지 않는 것이죠? 해결할 방법은 무엇일까요?**

→ 방금 전 문제랑 거의 똑같은 경우의 문제

```jsx
for (var i = 0; i < 3; i++){

  버튼들[i].addEventListener('click', function(){
    모달창들[i].style.display = 'block';
  });

}
```

내부 코드는 addEventListener, 클릭 되면 콜백함수 내의 **`모달창들[i].style.display = 'block';`** 을 실행해주세요~ 라는 코드임

→ 그 부분은 **반복문과 동시에 실행되지 X**

누군가 버튼을 클릭하면 addEventListener 내의 **`모달창들[i].style.display = 'block';`**코드가 발동됨

but, i를 쓰고싶어서 주변을 살펴보았더니 i값은 3밖에 없음

why? → 아까 반복문이 3번 실행되면서 i값은 0,1,2,3 ... 이렇게 차례로 변하다가 i값이 3이 되어 종료

 i 값은 var로 만든 전역변수 →  i값을 쓰려고 봤더니 **전역변수 i = 3밖에 없어서 3을 집어넣어서 계속 에러발생**

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
        ` // backtick
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
</div>`
```

backquote 문자열 + 함수

tagged literal

→ `함수()` 대신, 문자열 붙여서 실행할 수 있음 

```jsx
var 변수 = `손흥민`; // backtick
var 문자 = `안녕하세요 ${변수} 입니다 `;
function 함수(){
    return 10
}
console.log(함수`안녕하세요 ${변수} 입니다 `) // 10
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
console.log(어레이) // [ 'hello', 'world' ]

var 어레이 = ["hello", "world"];
console.log(...어레이) // hello world
```

1. 문장 붙이면 펼쳐줌

```jsx
var 문자 = "hello";
console.log(...문자) // h e l l o
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

console.log(a);// [ 1, 2, 3, 4 ]
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

함수의 default 파라미터  → 파라미터 집어 넣지 않으면 그냥 디폴트로 집어 넣어줄 값을 표기할 수 있음

```jsx
function 더하기(a, b = 10) {
  console.log(a + b);
}
더하기(1); // 11
더하기(1,2); // 3 
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
  for (var i = 0; i < arguments.length; i++)  // 파라미터 개수만큼 반복문 돌리기
  console.log(arguments[i]);
}
함수(2, 3, 4); // 2 3 4 
```

## Rest 파라미터

1. spread operator

```jsx
function 함수2(...파라미터들){
    console.log(파라미터들)
}

함수2(1,2,3,4,5,6,7);
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

함수2(1, 2, 3, 4, ); // 1 2 3 4
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
var a = [1,2,3];
var b = '김밥';
var c = [...b, ...a];
console.log(c);
```

`['김', '밥', 1, 2, 3 ]` 이라는 array가 출력

글자를 spread → 한글자씩 콤마로 분열

array를 spread → 대괄호를 제거

**2. spread 문제 2** ⭐

```jsx
var a = [1,2,3];
var b = ['you', 'are'];
var c = function(a,b){
  console.log( [[...a], ...[...b]][1] )
}
c(a,b);
```

c라는 함수에 a와 b라는 자료를 집어넣어서 실행

→ `[ [...a], ...[...b] ][1]`, 여기서 a와 b를 집어넣어보면

 → `[ [1,2,3], ...['you', 'are'] ][1]` , spread를 해치워버리면

→  `[ [1,2,3], 'you', 'are' ][1]` 

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
function 함수(a = 5, b = a * 2 ){
  console.log(a + b);
}
함수(undefined, undefined);
```

함수에 파라미터를 입력하지 않았을 경우 그 파라미터를 출력해보면 `undefined`가 출력됨

```jsx
 function 함수(a){
  console.log(a)
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
Math.max(5,6,4,3) // 6
```

 → `6`이라고 최댓값을 출력

최댓값을 검사하고 싶은 숫자들이 많을 때

```jsx
var numbers = [2,3,4,5,6,1,3,2,5,5,4,6,7];
```

numbers 안에 있는 숫자들을 Math.max()에 집어넣어서 쓰면 → 직접 소괄호 안에 10개넘는 숫자를 손수 기입해야함

`Math.max()` 안에 array 안의 모든 데이터를 담고싶으면

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
 console.log( [ 'b', 'c', 'a' ].sort() );

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
function 정렬(글자){
  console.log( [...글자].sort() )
}

정렬('bear'); // [ 'a', 'b', 'e', 'r' ]
```

→ 여기서 대괄호 벗기고 싶다면

→

```jsx
function 정렬(글자){
  console.log( ...[...글자].sort() )
}

정렬('bear'); // a b e r
```

**8. 데이터마이닝 기능 만들기**

알파벳들의 출현 갯수를 세어주는 함수 

**`글자세기('aacbbb')`** 라고 입력하면 콘솔창에

**`{ a : 2, b : 3, c : 1 }`**

→ 이렇게 출력해주는 글자세기() 라는 함수를 만들기

→ 입력한 단어에 들어있는 알파벳의 갯수를 세어서 오브젝트에 기록해주고 출력까지 해주는 함수

→ 글자에다가 반복문을 돌려서 해결 가능!

그냥 반복문을 써도 되고 조금 더 간단하게 사용하려면 `forEach()` 반복문을 쓸 수 있음

but, `forEach()`는  `array에만` 붙일 수 있는 함수

글자에 붙이려면.. `글자를 array화` → `[...글]` (해체하고 대괄호)

→  `‘abc’` → `[ 'a', 'b', 'c’ ]` 로 바뀜 (array로 바뀜)

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
function 글자세기(글){

    var 결과 = {};
      [...글].forEach(function(a){
         if( 결과[a] > 0 ){ 결과[a]++ } else { 결과[a] = 1 }
      });
    console.log(결과)
    }
글자세기('ddqdsqeqt') // { d: 3, q: 3, s: 1, e: 1, t: 1 }
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

why? → 파라미터는 변수생성 &  할당과 같음! `var = obj` 와 같은 개념

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

→ `var obj = { name: "park" };` , 이름1은 그대로  `var 이름1 = { name: "김" };` 

## **객체지향1. Object 생성 기계인 constructor**

constructor 문법의 용도 

→ **object를 마구 복사하고 싶을 때** 사용! (object 생성 기계)

예시) 출석부를 만든다고 가정

constructor

```jsx
var 사람 = { name: "kim", age : 15 };
function Student(){ // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
this.name = 'kim'
this.age = 15;
}
```

→ object 마구 뽑기 가능

→ 기계 사용하려면 `this` 라는 키워드가 필요함

→ this는 새로 생성되는 object를 뜻함 → `this.name = 'kim'` 은 새로 생성되는 오브젝트의 name 속성에 ‘kim’이라는 값을 대입

```jsx
var 사람 = { name: "kim", age : 15 };
function Student(){ // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
this.name = 'kim';
this.age = 15;
}

var 학생1 = new Student();
console.log(학생1) // Student { name: 'kim', age: 15 }
```

Q 기계로 생성되는 모든 학생 object에 `sayHi()` 함수 추가하고 싶다면?

```jsx
var 학생1 = { 
name: "kim",
age : 15,
sayHi : function(){
     console.log('안녕하세요 ' + this.name + '입니다')
 }
};

학생1.sayHi(); // 안녕하세요 kim입니다

function Student(){ // constructor는 일반함수와 다르다는 것을 보여주기 위해 첫글자 대문자 사용
this.name = 'kim';
this.age = 15;
}

var 학생1 = new Student(); 
```

→ 하드코딩말고  기계로 생성되는 모든 학생 object에 `sayHi()` 함수 추가하고 싶다면?

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
function Student(**이름**){ 
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

→ 상속이라고 함

this : 기계에서 새로 생성되는 object → `instance`

기계 : object 생성기계(constructor, 생성자)

**Q2. 상품마다 부가세() 라는 내부 함수를 실행하면 콘솔창에 상품가격 * 10% 만큼의 부가세금액이 출력되도록 하고 싶다면?** 

ex) `product1.부가세()` 이렇게 쓰면 콘솔창에 5000이 출력되어야함

```jsx
function Product(상품명, 가격){
  this.name = 상품명;
  this.price = 가격;
  this.부가세 = function(){
    console.log(this.price * 0.1)
  }
}

var product1 = new Product('shirts', 50000);
var product2 = new Product('pants', 60000);
```

→ product1과 product2는 각각 name, price 그리고 부가세()라는 속성을 가지게 됨

## **prototype**

상속을 구현할 수 있는 또 하나의 문법 prototype

prototype → 유전자 

기계(constructor) 만들면 prototype이라는 공간이 자동으로 생김

`기계.prototype` → 기계의 유전자

prototype에 값을 추가하면 모든 자식들이 물려받기 가능!

```jsx
function Student(이름){ 
    this.name = 이름;
    this.age = 15;
    this.sayHi = function(){
        console.log('안녕하세요 ' + this.name + '입니다')
    }
    }
    
    **Student.prototype.gender = '남';** // 오브젝트 키값 추가, 부모에 등록하면 모든 자식에 쓸 수 있음

    var 학생1 = new Student('park'); // 안녕하세요 park입니다
    var 학생2 = new Student('chae'); // 안녕하세요 chae입니다
    

    console.log(학생1.gender) // '남'
    console.log(학생2.gender) // '남'
    console.log(학생1) // Student { name: 'park', age: 15, sayHi: [Function (anonymous)] }
```

→ `학생1` 에는 gender가 없는데 어떻게 출력이 될까 ?

→ 자바스크립트는 `학생1.name` 의 경우

(1) 학생1이 직접 name을 가지고 있는가? → 출력

→ 학생1이 직접 gender을 가지고 있는가? → 없음 

(2) 그럼 학생1의 부모 유전자가 gender를 가지고 있는가?

→ `Student.prototype` 에 gender가 있는지 물어봄 → 있으면 실행

→ 내가 gender가 없으면 부모 유전자에 물어봄!

prototype의 동작원리 : 내장함수는 어떻게 동작하는가

```jsx
var arr = [1,2,3]
var arr = new Array(1,2,3) // 실제 컴퓨터가 array 만드는 방식 -> array 만드는 기계로부터 하나 뽑음, array도 오브젝트에 속함

arr.sort()
arr.map()
arr.push()
```

→ `sort()`, `map()`, `push()` 모두 사용가능 why? → array도 오브젝트에 속하니까

`arr` 에 sort 부여한적 없지만 쓸 수 있는 이유

→ `arr` 의 부모 유전자가 sort를 가지고 있음

모든 array 자료형은 Array 부모를 이용해 만듦

따라서 `학생.toString();` 의 prototype의 동작원리는

→  `학생1` 에 `toString` 없음

→ `Student.prototype` 에 `toString` 없음

→ `Object.prototype` 에 `toString` 있음

## prototype 특징

1.  `prototype` → `함수`에만 생성됨
2. 내 부모 유전자(부모의 prototype)을 검사하고 싶다면 `__proto__` 
3. `__proto__` 를 이용해 부모 강제 등록하기

```jsx
var 부모 = {name : 'kim'}
var 자식 = {};
자식.__proto__ = 부모; // 나의 부모는 이걸로 해주세요 ~ 
console.log(자식.name); // "kim"
console.log(자식); //{}
```

1. 콘솔창에서 알려주는 prototype chain

**0. 오브젝트 자료 여러개를 만들기**

하드코딩 했을 때

```jsx
var 학생1 = { name : 'Kim', age : 20 }
var 학생2 = { name : 'Park', age : 21 }
var 학생3 = { name : 'Lee', age : 22 }
```

**constructor문법을 사용해서 위의 오브젝트와 똑같은 오브젝트 3개를 한번 뽑기**

**→ 여기에 학생1.sayHi()라고 사용하면 "안녕 나는 Kim이야" 라는 글자가 콘솔창에 나오도록 sayHi()라는 함수도 constructor 안에 추가하려면?**

```jsx
function Student(이름, 나이){
  this.name = 이름;
  this.age = 나이;
  this.sayHi = function(){
    console.log('안녕 나는 ' + this.name + '이야');
  }
}

var 학생1 = new Student('Kim', 20);
var 학생2 = new Student('Park', 21);
var 학생3 = new Student('Lee', 22);

학생1.sayHi(); // 안녕 나는 Kim이야
```

**1. 다음 코드의 출력 결과는?**

```jsx
function Parent(){
  this.name = 'Kim';
}
var a = new Parent();

a.__proto__.name = 'Park';
console.log(a.name)

```

→  `'Kim'` 

첫 4줄에 의해서 `a = { name : 'Kim' }` 이 되고

`a.__proto__.name = 'Park';` 이건 부모 prototype에 `{ name : 'Park' }`이걸 추가하라는 뜻임

그럼 이제 a.name 이라고 사용했을 때

내가 직접 가지고 있는 `{ name : 'Kim' }` 이걸 우선 출력해줌( `{ name : 'Park' }` 를 우선출력하지 X

**2. 함수가 들어가지 않음**

0번 문제에서 Student라는 부모에 sayHi라는 함수를 하나 추가

→ sayHi()라고 사용하면 "안녕 나는 ~~이야" 라고 내 이름을 출력해주는 함수를 prototype에 추가

→ 의도한 대로 이름이 출력되지 X

```jsx
function Student(이름, 나이){
  this.name = 이름;
  this.age = 나이;
}

Student.prototype.sayHi = () => {
    console.log('안녕 나는 ' + this.name + '이야');
  }
var 학생1 = new Student('Kim', 20);

학생1.sayHi();//왜 이 코드가 제대로 안나오죠?
```

`sayHi()` 라는 함수를 prototype에 추가할 때 `arrow function`을 사용했습니다 .

why?? →  arrow function은 그냥 일반 function 대체품이 X

`arrow function`  → this를 바깥에 있는 `this를 그대로 사용하고 싶을 때 쓰는 함수`

but, sayHi() 함수를 만들 때 arrow function을 사용해서 내부에 있던 this라는 값이 이상해짐

```jsx
Student.prototype.sayHi = () => {
    console.log(this);
}
```

sayHi 함수에 그냥 this 하나만 출력해보시면 window가 출력됨 (strict mode에선 undefined)

`arrow function`을 사용하면 그냥 바깥 아무데나 있던 값을 가져와서 사용함

→  **this 값은 `window`**이며, 그 window를 그대로 저기 함수 안에다가 적용했기 때문

함수안에서 this 키워드의 뜻은 매번 재정의

object안에 들어있는 함수안에 있는 this → 함수를 부른 object가 됨

but, arrow function의 경우 함수 안에서 this 뜻이 재정의되지 않고 바깥에 있던 this를 사용

```jsx
var 오브젝트 = {
  sayHi : () => { console.log(this) }
}
오브젝트.sayHi();
```

→  위 코드의 this는

오브젝트가 아니라 `window`가 출력

**3. 모든 array에 적용할 수 있는 함수를 직접 새로 만들려면?**

모든 array에 붙일 수 있는, array 내에 있는 3이라는 값을 제거해주는 유용한 함수를 하나 만들기

```jsx
var arr = [1,2,3];
arr.remove3();

console.log(arr);//[1,2]
```

→ array뒤에 붙이기만 하면 array 내의 3이라는 모든 숫자 자료들이 삭제

→  `remove3()`

remove3()함수는 어떻게, 어디에 만들어야 모든 array에 쓸 수 있을까?

```jsx
Array.prototype.remove3 = function(){
  this 에서 3을 찾아서 제거해주세요
}
```

이렇게 코드를 짜면 됨

위의 코드에서의 this라는 키워드는 현재 remove3이라는 함수를 작동시키는 object (여기서는 array) 라는 뜻

→ this라는 array에서 3을 제거하는 코드는 짤까?

→  this라는 array 안에 있는 데이터를 하나하나 출력하면서 3과 비교하려고 반복문 사용

```jsx
Array.prototype.remove3 = function(){
  for (var i = 0; i < this.length; i++) {
    if ( this[i] === 3 ) {
      this.splice(i,1);
    }
  }
};

var arr = [1,2,3,4];
arr.remove3();

console.log(arr);//[1,2,4]
```

1. this라는 array의 길이만큼 반복문을 돌리는데, 돌리는 과정에서 this[i] 라고 쓰면서 this 안에 있는 모든 데이터를 출력

2. 만약에 this[i]가 3이면

3. this라는 array에서 i번째 자료를 제거 라고 씀 (splice 라는 함수는 array안에 뭘 제거할 때 사용)

→ remove3() 함수를 제작

## **ES5방식으로 쉽게 구현하는 상속기능**

prototype function 기계() {} →  옛날문법

상속을 구현하는 방법 ES5 / ES6

ES5 방법 : Object.creat(물려 받을 부모 object)

부모가 가진 name, age를 그대로 물려받은 자식 object를 만들고 싶으면?

→ constructor 함수를 만들거나 Object.creat를 사용

```jsx
var 부모 = {name : "kim", age : 50};

var 자식 = Object.create(부모); // protoype을 부모로 해주세요 ~
console.log(자식.name) //"kim"// 자식의 프로토타입을 부모로 두고 있기 때문
console.log(자식) // {}
```

자식의 age를 바꾸고 싶다면?

```jsx
var 부모 = { name: "kim", age: 50 };

var 자식 = Object.create(부모); // protoype을 부모로 해주세요 ~
console.log(자식.name); //"kim"// 자식의 프로토타입을 부모로 두고 있기 때문
console.log(자식); // {}
**자식.age = 20;
console.log(자식.age) // 20**
```

```jsx
var 부모 = { name: "kim", age: 50 };

var 자식 = Object.create(부모); // protoype을 부모로 해주세요 ~
console.log(자식.name); //"kim"// 자식의 프로토타입을 부모로 두고 있기 때문
console.log(자식); // {}
자식.age = 20;
var 손자 = Object.create(자식)
**console.log(손자) // {}
console.log(손자.name) // "kim"**
```

1. 직접 name을 갖고 있나?
2. 없으면 부모의 prototype에는 name이 있나?

`손자.age` → `20`

## ES6 : class

→ constructor, prototype 을 이용한 상속기능을  만들 수 있게 도와주는 문법

기존 function부터 시작하던 문법과 기능상 차이는 크게 없고 약간 더 보기쉽게 표현

상속기능을 구현하는 ES6 방법 : class

```jsx
class 부모 {
  constructor() {
    this.name = "kim";
  }
}

var 자식 = new 부모();
```

함수를 추가하고 싶으면

```jsx
class 부모 {
  constructor() {
    this.name = "kim";
    // this.sayHi = function(){console.log('hello')} // 함수 추가하고 싶으면, constructor에 추가하든가 (자식이 직접 함수를 가짐)
  }
  sayHi(){console.log('hello')} // 여기에 씀 (부모.prototype에 추가됨)
}

var 자식 = new 부모();
console.log(자식.__proto__) //{} // 얘의 부모 prototype(부모유전자)가 출력됨
```

class 안에 함수 여러개 추가

```jsx
lass 부모 {
  constructor() {
    this.name = "kim";
    // this.sayHi = function(){console.log('hello')} // 함수 추가하고 싶으면, constructor에 추가하든가 (자식이 직접 함수를 가짐)
  }
  sayHi(){console.log('hello')} // 여기에 씀 (부모.prototype에 추가됨)
}
**부모.prototype.sayHello = function(){} // sayHello라는 함수 추가**
var 자식 = new 부모();
```

class의 constructor 안에 파라미터 추가

```jsx
class 부모 {
  constructor(**aaa**) {
    this.name = **aaa**
    // this.sayHi = function(){console.log('hello')} // 함수 추가하고 싶으면, constructor에 추가하든가 (자식이 직접 함수를 가짐)
  }
  sayHi(){console.log('hello')} // 여기에 씀 (부모.prototype에 추가됨)
}
부모.prototype.sayHello = function(){}
var 자식 = new 부모();
```

객체지향 문법 

→ object를 여러개 만들어 쓰기 위해서 사용

## **객체지향 : class를 복사하는 extends / super**

```jsx
class 부모 {
}
```

이것과 유사한 class를 하나 더 만들고 싶다면? →  `extends` (class 상속)

```jsx
class 할아버지 {
    constructor(name){
        this.성 = 'kim';
        this.이름 = name;
    }
}

var 할아버지1 = new 할아버지('만덕');
console.log(할아버지1) // 할아버지 { '성': 'kim', '이름': '만덕' }
```

→ 이것과 유사한 클래스 만들고 싶다면? (할아버지의 속성들 그대로 물려 받아서)

but, extends 해서 만든 class는 this 그냥 쓸 수 없음 → `super()` 다음에 써야 함

`super()` → 물려 받는 class의 constructor 라는 뜻 

그리고 파라미터도 할아버지 것과 마쳐주면됨

```jsx
class 할아버지 {
    constructor(name){
        this.성 = 'kim';
        this.이름 = name;
    }
}

var 할아버지1 = new 할아버지('만덕');
//console.log(할아버지1) // 할아버지 { '성': 'kim', '이름': '만덕' }

**class 아버지 extends 할아버지 {
    constructor(name){ // 파라미터도 할아버지 것과 맞춰주면됨
        super(name);
        this.나이 = 50
    }
}

var 아버지1 = new 아버지();
console.log(아버지1) // 아버지 { '성': 'kim', '이름': undefined, '나이': 50 }**
```

→ **`var 아버지1 = new 아버지();` 에서 파라미터를 집어 넣지 않아서 `아버지1` 을 출력 했을 때 `undefined` 가 나옴!**

```jsx

**var 아버지1 = new 아버지('만수');
console.log(아버지1) //아버지 { '성': 'kim', '이름': '만수', '나이': 50 }**
```

`super()` 의 또 다른 용도

함수 만들면 할아버지.prototype에 추가 됨

할아버지 class에 있는 `sayHi()` 가 아버지 class에 전달

```jsx
class 할아버지 {
    constructor(name){
        this.성 = 'kim';
        this.이름 = name;
    }
    sayHi(){ // 함수 만들면 할아버지.prototype에 추가 됨
        console.log('안녕');
    }
}

var 할아버지1 = new 할아버지('만덕');
//console.log(할아버지1) // 할아버지 { '성': 'kim', '이름': '만덕' }

class 아버지 extends 할아버지 {
    constructor(name){ // 파라미터도 할아버지 것과 맞춰주면됨
        super(name);
        this.나이 = 50
    }
}

var 아버지1 = new 아버지('만수');
console.log(아버지1.sayHi()) // 안녕
```

```jsx
class 할아버지 {
    constructor(name){
        this.성 = 'kim';
        this.이름 = name;
    }
    sayHi(){ // 함수 만들면 할아버지.prototype에 추가 됨
        **console.log('안녕 저는할아버지에요');
    }**
}

var 할아버지1 = new 할아버지('만덕');
//console.log(할아버지1) // 할아버지 { '성': 'kim', '이름': '만덕' }

class 아버지 extends 할아버지 {
    constructor(name){ // 파라미터도 할아버지 것과 마쳐주면됨
        super(name);
        this.나이 = 50
    }
    sayHi(){ // 함수 만들면 할아버지.prototype에 추가 됨
        **console.log('안녕 저는 아버지에요');**
    }
}

var 아버지1 = new 아버지('만수');
console.log(아버지1.sayHi()) // **안녕 저는 아버지에요**
```

→ 조금 더 가까운 프로토타입 출력

1. `super(name)`에서 super → 부모 class의 constructor을 의미
2. `super.sayHi();` 에서 super → 부모 class의 prototype을  의미 `__proto__`

```jsx
class 할아버지 {
    constructor(name){
        this.성 = 'kim';
        this.이름 = name;
    }
    sayHi(){ // 함수 만들면 할아버지.prototype에 추가 됨
        console.log('안녕 저는 할아버지에요');
    }
}

var 할아버지1 = new 할아버지('만덕');
//console.log(할아버지1) // 할아버지 { '성': 'kim', '이름': '만덕' }

class 아버지 extends 할아버지 {
    constructor(name){ // 파라미터도 할아버지 것과 마쳐주면됨
        super(name);
        this.나이 = 50
    }
    sayHi(){ // 함수 만들면 할아버지.prototype에 추가 됨
        console.log('안녕 저는 아버지에요');
        **super.sayHi(); // 안녕 저는 할아버지에요**
    }
}

var 아버지1 = new 아버지('만수');
**console.log(아버지1.sayHi()) //안녕 저는 아버지에요**
```

## **getter, setter**

age라는 자료 꺼내고 싶으면?

```jsx
var 사람 = {
    name : 'park',
    age : 30
}
console.log(사람.age) // 30
```

→ `사람.age` 대신 자료를 꺼내는 법을 만들어서 꺼냄(유행하는 기술)

내년 age를 알고 싶음

→ `nextAge()` 라는 함수를 만듦

```jsx
var 사람 = {
    name : 'park',
    age : 30,
    nextAge(){
        return this.age + 1 // this == 사람 object 
    }
}
console.log(사람.nextAge()) // 31
```

`사람.age + 1;` 하면 쉬운데 `nextAge()` 만든 이유는 ?

→ 함수를 만들어 object 데이터를 다루는 이유 

1. object 자료가 복잡할 때 함수를 이용하면 편리함
2. object 자료 수정시 편리함

ex) `사람.age = ‘20’;` 이렇게 문자로 잘못 코딩하면 +1 해도 `201`로 출력됨

→ age를 `30`에서 `20`으로 바꾸어주는 함수 `setAge()` 사용

```jsx
var 사람 = {
  name: "park",
  age: 30,
  nextAge() {
    return this.age + 1; // this == 사람 object
  },
  setAge(나이) {
    this.age = 나이;
  },
};
사람.setAge(20); // 데이터를 수정해주는 함수를 제작
console.log(사람); 
/* 
name: 'park',
  **age: 20,**
  nextAge: [Function: nextAge],
  setAge: [Function: setAge]
}
*/
```

`parseInt()`→ 문자 `‘20’` 써도 숫자로 바뀜 ( 데이터 꺼내거나 수정할때 편리 & 실수 방지 & 관리 편리)

```jsx
var 사람 = {
  name: "park",
  age: 30,
  nextAge() {
    return this.age + 1; // this == 사람 object
  },
  setAge(나이) {
    **this.age = parseInt(나이);** // 문자로 입력하더라도 정수로 바꿔줌 -> 데이터 수정전 미리 검사 가능
  },
};
사람.setAge(**'20'**); // 데이터를 수정해주는 함수를 제작
console.log(사람);

/* 
name: 'park',
  **age: 20,**
  nextAge: [Function: nextAge],
  setAge: [Function: setAge]
}
*/
```

복잡한 소괄호 보기 싫다면 ES5 `set / get` 키워드

`사람.setAge(**'20'**)` → `사람.setAge = ‘20’`

→ 함수 앞에다가 `set` 이라는 키워드 사용! → 똑같은 결과 나옴

`setter` → `set`은 데이터 변경하는 함수에 `setAge(나이)` → `set setAge(나이)`

 `getter` →  `get`은 데이터 꺼내쓰는 함수에  `nextAge()` → `get nextAge()`

```jsx
var 사람 = {
  name: "park",
  age: 30,
  **get** nextAge() {
    return this.age + 1; // this == 사람 object
  },
  **set setAge(나이)** {
    this.age = parseInt(나이); // 문자로 입력하더라도 정수로 바꿔줌 -> 데이터 수정전 미리 검사 가능
  },
};
**사람.setAge ='20';** // 데이터를 수정해주는 함수를 제작
console.log(사람);
```

get 함수들(getter) 쓸때 → return 있어야 함 why? 뭔가를 꺼내야 하니까

set 함수들 (setter) → 파라미터가 1개 있어야함 ! (1개만)

class에서 사용하는 get / set 

```jsx
class 사람 {
    constructor() {
        this.name = 'park';
        this.age = 20;
    }
    nextAge(){
        return this.age + 1 // 내년 나이를 출력해주는 함수 제작
    }
}

var 사람1 = new 사람();
console.log(사람1) // 사람 { name: 'park', age: 20 }
console.log(사람1.nextAge()) // 21 // 사람1도 nextAge 쓸 수 있음
```

→ 여기서 get 키워드 붙일 수 있음 → 소괄호 제거할 수 있음

```jsx
class 사람 {
    constructor() {
        this.name = 'park';
        this.age = 20;
    }
    **get nextAge(){
        return this.age + 1 /**/ 내년 나이를 출력해주는 함수 제작
    }
}

var 사람1 = new 사람();
console.log(사람1) 
console.log(**사람1.nextAge**) // 21 
```

set 키워드 사용

```jsx
class 사람 {
    constructor() {
        this.name = 'park';
        this.age = 20;
    }
    get nextAge(){
        return this.age + 1 // 내년 나이를 출력해주는 함수 제작
    }
    **set setAge(나이){
        this.age = 나이;**
    }
}

var 사람1 = new 사람();
**사람1.setAge = 200**
console.log(사람1) // 사람 { name: 'park', age: 200 }
```

## class, extends, getter, setter 연습문제

**1. 직접 class 구조 만들어보기**

갑자기 강아지 SNS를 만들고 싶어서 자바스크립트로 열심히 코딩하던 중,

여러 강아지 정보들을 담은 유사한 오브젝트 자료형을 테스트삼아 몇개 만들려고 합니다.

```jsx
var 강아지1 = { type : '말티즈', color : 'white' };
var 강아지2 = { type : '진돗개', color : 'brown' };
```

이렇게 쭉 많이 만들고 싶은데 하드코딩하기 싫어서 class를 만들어 강아지 오브젝트들을 뽑고 싶습니다.

그럼 class를 어떻게 만드는게 좋을까요?

```jsx
 
class Dog {
  constructor(타입, 칼라){
    this.type = 타입;
    this.color = 칼라;
  }
}
var 강아지1 = new Dog('똥개', 'black');
 
```

**2. 이번엔 고양이관련 object들을 만들고 싶습니다.**

이번엔 class를 이용해 고양이 오브젝트 여러개를 뽑고 싶습니다.

```jsx
var 고양이1 = { type : '코숏', color : 'white', age : 5 };
var 고양이2 = { type : '러시안블루', color : 'brown', age : 2 };
```

type, color는 이전에 만든 강아지 object와 유사한데

고양이들만 특별하게 age라는 속성을 하나 더 추가하고 싶습니다. 어떻게 class를 만들면 될까요?

1번 문제에서 만들었던 강아지 class와 유사하기 때문에 extends라는 문법을 쓰는 것도 좋겠군요.

저는 위에서 만들었던 Dog 를 그대로 이용하기 위해

extends 문법을 사용했습니다.

```jsx
class Dog {
  constructor(타입, 칼라){
    this.type = 타입;
    this.color = 칼라;
  }
}

class Cat extends Dog {
  constructor(타입, 칼라, 나이){
    super(타입, 칼라);
    this.age = 나이;
  }
}

var 고양이1 = new Cat('동네고양이', 'white', 5);
```

이제 쉽게 고양이 오브젝트들을 뽑아낼 수 있습니다.

파라미터 어떻게 쓰는지 궁금하다면

지금 고양이 오브젝트에 필요한 파라미터를 constructor()안에 다 나열해주시면 되고

Dog로부터 물려받은 속성들에 필요한 파라미터들은 그대로 super() 안에 넣어주시면 됩니다.

혹은 그냥 **super()함수는 Dog의 constructor()를 그대로 복붙했다~**라고 생각하셔도

쉽게 사용법을 파악할 수 있을겁니다.

**3. 고양이와 강아지 object들에 기능을 하나 추가하고 싶습니다.**

**모든 고양이와 강아지** object들은 **.한살먹기()** 라는 함수를 사용할 수 있습니다.

**(1)** 한살먹기 함수는 강아지 class로부터 생성된 오브젝트가 사용하면 콘솔창에 에러를 출력해주어야합니다.

**(2)** 한살먹기 함수는 고양이 class로 부터 생성된 오브젝트가 사용하면 현재 가지고있는 age 속성에 1을 더해주는 기능을 실행해야합니다.

한살먹기 함수는 어떻게 만들면 좋을까요? (검색이 필요할 수 있습니다)

일단 한살먹기() 함수는 Dog에 추가했습니다. 왜냐면 Cat, Dog 둘다 사용가능해야하니까요.

뭐 Dog에 따로 Cat에 따로 이렇게 하셔도 무방한데 저는 이랬습니다.

그래서 고양이들 강아지들은 전부 한살먹기()를 사용할 수 있습니다.

```jsx
class Dog {
  constructor(타입, 칼라){
    this.type = 타입;
    this.color = 칼라;
  }
  한살먹기(){
    if( this instanceof Cat) {
    this.age++
    }
  }
}

class Cat extends Dog {
  constructor(타입, 칼라, 나이){
    super(타입, 칼라);
    this.age = 나이;
  }
}

```

그럼 이제 한살먹기()를 고양이들이 쓰면 나이를 1살 더해주고,

강아지들이 쓰면 에러를 출력해줘야하는데 그걸 구분하기 위해 함수 안에 if문을 추가했습니다.

자바스크립트는 instanceof 라는 고마운 연산자가 있습니다.

instanceof b 이렇게 쓰시면 a가 b로부터 생성된 오브젝트인지 아닌지를 true/false로 알려주는 연산자입니다.

그래서 한살먹기()라는 함수를 만들고 this.age++를 해주는 기능을 넣었는데 이 기능은 this가 instanceof Cat인 경우에만 실행하도록 if문을 추가했습니다.

그럼 이제 Cat으로 부터 생성된 오브젝트들만 한살먹기() 내부 기능을 사용가능합니다.

**4. get/set을 이용해봅시다**

자바스크립트로 간단한 게임 기능을 가진 오브젝트를 뽑는 class를 만들고 싶습니다.

다음 조건에 따라 class를 만들어보세요. class 이름은 Unit이라고 합시다.

**(1)** 모든 Unit의 인스턴스는 **공격력, 체력** 속성이 있으며 기본 공격력은 5, 기본 체력은 100으로 설정되어 있어야 합니다.

**(2)** 모든 Unit의 인스턴스는 전투력을 측정해주는 battlePoint라는 getter가 있습니다.

console.log( 인스턴스.battlePoint ) 이렇게 사용하면 현재 **공격력과 체력을 더한 값**을 콘솔창에 출력해주어야합니다.

**(3)** 모든 Unit의 인스턴스는 heal이라는 setter가 있습니다.

인스턴스.heal = 50 이렇게 사용하면 **체력 속성이 50 증가**해야합니다.

```jsx
class Unit {
  constructor(){
    this.체력 = 100;
    this.공격력 = 5;
  }
  get battlePoint(){
    return this.체력 + this.공격력;
  }
  set heal(a){
    this.체력 = this.체력 + a;
  }
};

var 쎈애 = new Unit();

console.log(쎈애.battlePoint);
쎈애.heal = 50;

```

1. Unit이라는 class를 만들고 constructor에는 체력과 공격력을 기본으로 부여했습니다.

2. battlePoint()라는 함수를 만들고 이건 체력과 공격력을 합해서 출력하는 기능을 만들었습니다.

get을 붙여서 소괄호없이도 이용가능하게 만들었습니다.

3. heal() 이라는 함수를 만들었고 파라미터로 숫자를 입력하면 체력이 그만큼 증가합니다.

set을 붙여서 소괄호없이도 이용가능하게 만들었습니다.

**5. get/set을 이용해봅시다2**

다음과 같은 오브젝트가 있습니다.

```jsx
var data = {
  odd : [],
  even : []
}
```

**(1) data 오브젝트에는 setter 역할 함수가 하나 필요합니다.**

setter 함수에 1,2,3,4 이렇게 아무 자연수나 파라미터로 입력하면 홀수는 odd, 짝수는 even 이라는 속성에 array 형태로 저장되어야합니다.

**(2) data 오브젝트에는 getter 역할 함수가 하나 필요합니다.**

getter 함수를 사용하면 odd, even에 저장된 모든 데이터들이 숫자순으로 정렬되어 출력되어야합니다.

예를 들면

**data.setter함수(1,2,3,4,5)** 이렇게 입력하면

**data = { odd : [1,3,5], even : [2,4] }**

이렇게 저장이 되어야합니다.

빨리 위의 역할을 하는 함수 두개를 data 오브젝트 내에 만들어보십시오.

**일단 1번은 어떻게 짰냐면**

일단 setter 함수를 만들어봅시다.

이건 파라미터로 숫자들을 입력하면 숫자들을 분류해서 각각 odd, even 이라는 array에 저장해야합니다.

근데 파라미터로 몇개가 들어올지 모르기 때문에 rest 파라미터같은걸 쓰면 좋겠죠?

```jsx
var data = {
  odd : [],
  even : [],
  setter함수 : function(...숫자들){
    console.log(숫자들)
  }
};

data.setter함수(1,2,3);
```

쩜쩜쩜이라는 rest 기호를 쓰시면 입력된 파라미터들을 전부 array로 싸매줍니다.

그 다음에 숫자들이라는 파라미터모음 array를 하나씩 출력해보며 분류하면 되겠죠?

숫자들[0]이 홀수면 odd에 push 해주고 짝수면 even에 push해주고

숫자들[1]이 홀수면.. 짝수면 ...

숫자들[2]가 홀수면.. 짝수면..

반복되는게 싫어서 반복문을 쓰면 뭐 이렇게 되겠죠?

```jsx
var data = {
  odd : [],
  even : [],
  setter함수 : function(...숫자들){
    숫자들.forEach(function(a){
      a가 홀수면 this.odd에 push(a)하고..
      b가 짝수면 this.even에 push(a)하고...
    });
  }
};

data.setter함수(1,2,3);
```

근데 홀수랑 짝수인걸 어떻게 구분합니까?

여러분이 수학을 잘하시면 알 수 있는데

그 숫자를 2로 나눠서 나머지를 보면 알 수 있습니다. 2로 나눠서 나머지가 0이면 짝수죠? 아니면 홀수고요.

자바스크립트는 나머지를 출력해주는 연산자도 친절하게 있습니다. % 기호를 쓰면 됩니다.

6 % 2 써보시면 이 자리에 0이 남습니다.

5 % 2 써보시면 이 자리에 1이 남고요.

```jsx
var data = {
  odd : [],
  even : [],
  setter함수 : function(...숫자들){
    숫자들.forEach(function(a){
      if ( a % 2 == 1 ) {
        this.odd.push(a)//홀수일때
      } else {
        this.even.push(a)//짝수일때
      }
    });
  }
};

data.setter함수(1,2,3);
```

그래서 if문을 완성시켰습니다.

근데 제대로 작동되지 않습니다. 에러가 뜨죠?

왜냐면 this.odd.push 이부분이 에러가 나는 것 같습니다. 여기서 this.odd는 내 오브젝트의 odd속성을 뜻하는게 아니라

forEach안의 function(){} 안에서의 this는 약간 다른 뜻입니다.

근본없는 콜백함수에서 쓰시면 this가 window 이런 뜻이니까요.

그래서 this를 위해 함수 모양을 arrow function으로 바꿔주면

```jsx
var data = {
  odd : [],
  even : [],
  setter함수 : function(...숫자들){
    숫자들.forEach((a)=>{
      if ( a % 2 == 1 ) {
        this.odd.push(a)//홀수일때
      } else {
        this.even.push(a)//짝수일때
      }
    });
  }
};

data.setter함수(1,2,3);
```

입니다.

set 키워드는 취향에 따라 알아서 추가해보시길 바랍니다.

**2번은 어떻게 짰냐면**

코드 넘 길어지니까 setter함수 빼고 getter함수만 좀 만들어봅시다.

array 두개를 합치려면 어떻게 합니까.

엣날에 배웠던 ES6 문법을 사용해보십시오.

```jsx
var data = {
  odd : [1,3],
  even : [2,4,6],
  get getter함수(){
    return [...this.odd, ...this.even ].sort()
  }
};

console.log(data.getter함수);
```

... 기호로 spread operator 문법을 이용하시면 this.odd 그리고 this.even이라는 array 두개를 쉽게 합칠 수 있습니다.

그리고 그걸 출력해주는 getter함수를 만들었구염.

근데 출력하기 전에 정렬하고 싶으면 .sort()만 뒤에 붙이시면 됩니다.

그럼 문자정렬 해주는데 문자정렬이 아니라 숫자정렬을 잘 해주셔야하니

숫자정렬하는 법은 구글에 찾아서 한번 적용해보시길 바랍니다.

# level3

## **Destructuring 문법**

= 패턴매칭

array 하나 만들고

→ 중요한 자료이기 때문에 전부 꺼내서 변수에 담고 싶음

```jsx
var arr = [2, 3, 4];
var a = arr[0]
var b = arr[1]
...
```

→ 너무 복잡함

→ 모양만 맞춰 변수 선언하면 변수 생김(직관적으로 변수 만들 수 있음)

```jsx
var arr = [2, 3, 4];
**var [a, b, c] = [2, 3, 4];**
console.log(a) // 2
console.log(b)// 3
```

array destructuring 할 때 몇개를 빼먹는다면

→ 등호로 기본값 지정 가능

```jsx
var arr = [2, 3, 4];
**var [a, b, c = 10] = [2, 3];**
console.log(a) // 2
console.log(b)// 3
console.log(c) // 10
```

변수 선언만하고 할당 안하면 `undefined` 들어감

```jsx
var arr = [2, 3, 4];
var [a, b, c = 10] = [];
console.log(a) // undefined
```

object 데이터를 꺼내 변수에 담으려면?

기존방법

```jsx
var obj = {name : 'kim', age : 30}
var name = obj.name
var age = obj.age
```

똑같이 모양만 맞춰주면 됨 

```jsx
var {name, age} = {name : 'kim', age : 30};
console.log(name) // kim
console.log(age) // 30
```

→ 변수명을 오브젝트의 key명과 똑같이 써야함 

변수명 변경하고 싶을 때 `name` 대신 `이름` 사용

```jsx
var {**name : 이름**, age} = {name : 'kim', age : 30};
console.log(이름) // kim
```

기본값 지정가능

```jsx
var {name : 이름 = 'park'} = {};
console.log(이름) // park
```

반대로 변수들을 object에 집어 넣고 싶은 경우

```jsx
var name = "kim";
var age = 30;

var obj = {**name : name, age : age**}
console.log(obj) // { name: 'kim', age: 30 }
```

→ name이라는 속성에는 변수 name(`"kim"`)을, age라는 속성에는 변수 age (`30`)

ES6 부터는 축약해서 사용할 수 있음(key와 value가 같을 때)

`var obj = {name : name, age : age}` → `var obj = {name, age}`

 → 응용하면 파라미터에도 destructuring 문법 똑같이 사용가능 (파라미터도 넓은 의미의 변수니까)

```jsx
var obj = {name: 'kim', age : 30}
function 함수(파라미터) {
    console.log(파라미터)
}
함수(obj) // { name: 'kim', age: 30 }
```

→ object 데이터들을 파라미터로 만들고 싶은 경우

**`{ name, age }` 사용**

```jsx
var obj = { name: "kim", age: 30 };
function 함수(**{ name, age }**) {
  console.log(name); // kim
  console.log(age); // 30
}
```

ex)

```jsx
function 함수( **[name, age]** ){
  console.log(name);
  console.log(age);
}

var array = [ 'Kim', 30 ];
함수( ['Kim', 30] );
```

이렇게 해도됨

파라미터인 [name, age] 를 만들 때 ['Kim', 30] 이걸 그대로 대입해서 만듦

→ 각각 name과 age에는 `Kim`과 `30`이라는 데이터가 들어갑니다.

**Q1. 변수를 마구 만들었는데 말입니다.**

```jsx
var [number, address] = [ 30, 'seoul' ];
var {address : a , number = 20 } = { address, number };
```

a와 address와 number라는 변수는 각각 무슨 값을 가지고 있을까요?

→ 첫 줄을 거치면 number라는 변수는 30, address라는 변수는 'seoul'이 됩니다.

→ 둘째줄을 약간 보기쉽게 바꿔보자면

```jsx
var {address : a , number = 20 } = { address : 'seoul', number : 30 };
```

이렇게 됩니다. 이러면 조금 더 보기쉽죠?

그래서 a는 `'seoul'`

number는 `30`

address는 첫줄에서 수정되고 끝나니까 그대로 `'seoul'`입니다.

**Q2. 다음과 같은 Object에서 데이터를 뽑아서 변수를 만들고 싶습니다.**

```jsx
let 신체정보 = {
  body: {
    height: 190,
    weight: 70
  },
  size: ["상의 Large", "바지 30인치"],
};
```

여러분의 뛰어난 신체 정보를 담은 Object입니다.

여기서 **키, 몸무게, 상의사이즈, 하의사이즈** 정보를 각각 뽑아서 4개의 변수를 만들고 싶습니다.

어떻게 만들면 될까요?

(참고 : 데이터가 얼마나 복잡하든간에 좌우 형태를 똑같이 맞추시면 destructuring 문법으로 변수를 만들 수 있습니다.)

```jsx
let 신체정보 = {
  body: {
    height: 190,
    weight: 70
  },
  size: ["상의 Large", "바지 30인치"],
};

let {
  body: {
    height,
    weight
  },
  size: [ 상의, 하의 ]
} = 신체정보;
```

잘 보시면 등호를 이용해서 좌우를 똑같이 맞췄습니다.

그리고 왼쪽엔 변수명을 적어주었고요.

그럼 이제 height, weight, 상의, 하의라는 이름의 변수가 생성됩니다.

## **import / export**  ⭐

전통적인 모듈화 방식

```jsx
<script src="main.js"> 
    </script>
```

ES6 import /export 

`import` 가져올거 `from` ‘경로’ → html에서

`export default` 내보낼거 → js에서

```jsx
<script type="module"> 
    import a from 'main.js'
</script>
```

→ 그 변수를  `a`라고 부름

ES6 → main.js에 있던 모든 내용을 가져오지 않고 **필요한 변수 내용만** 가져옴

참고1) export default 쓰면 import 할 때 이름 바꿔도 됨 ( export 사용하면 다른 변수 써도됨)

 

```html
<script type="module"> 
        import a from "/main.js";
        console.log(a); <!-- 10 -->
    </script>
```

```jsx
var a = 10;
export default a;
```

여러개의 변수를 export 하고 싶을 때

참고2) export deafualt 는 파일당 1회 사용할 수 있음

```jsx
var a = 10;
var b = 20;
export default a;
export default b; // 에러출력
```

여러개를 내보내는 export 문법

`import` {가져올것들} `form` ‘경로’

`export` {내보낼것들}

```jsx
var a = 10;
var b = 20;
export {a};
export {b};
```

이렇게 해도됨

```jsx
var a = 10;
var b = 20;
export {a, b};
```

참고3) export 키워드는 변수/함수 선언 왼쪽에 써도 됨

```jsx
export var a = 10;
var b = 20;
export {a, b};
```

이때 import하려면 정확해 써줘야함!

export / import 시 변수이름 똑같이 써야함!

```html
<script type="module"> 
        import {a} from "/main.js";
        console.log(a); <!-- 10 -->
    </script>
```

`{a}`, `{b}`, `{a,b}` 처럼 확실히 import할 내용 적어줘야 함!

`export default`도 동시에 쓸 수 있을까? → 가능

```jsx
var a = 10;
var b = 20;
var c = 30;
export { a, b };
export default c;
```

Q. export default 했던 c를 import 해오고 싶으면?

→  `import` 작명 `from` ‘경로’

```jsx
<script type="module"> 
        import 작명 from "/main.js";
        console.log(작명);
    </script>
```

Q. export {a,b} 했던 a를 import 해오고 싶으면?

→ `import` {변수명} `from` ‘경로’

Q. export default c 와 export {a,b} 동시에 import 하고 싶다면?

```jsx
<script type="module"> 
        import 작명, {a,b} from "/main.js";
        console.log(작명);
    </script>
```

```jsx
var a = 10;
var b = 20;
var c = 30;
export { a, b };
export default c;
```

변수명이 마음에 안들면 새로 짓자

`import` {변수명 `as` 새변수명} `from` ‘경로’

```html
<script type="module"> 
        import {a as 별명} from "/main.js";
        console.log(별명); <!-- 10 -->
				console.log(a); <!-- 에러 -->
    </script>
```

모든 것을 다 import 해오는 `*` 기호

`import` * `as` 변수들명 `from` ‘경로’

```html
<script type="module"> 
        import *  as 별명 from "/main.js";
        console.log(별명);
 </script>
```

디폴트 한걸 가져오려면

`console.log(별명.c)` → 에러 출력!

→ 항상 이런식으로 해야함

```jsx
import c**,** *  as 별명 from "/main.js";
        console.log(c);
```

```jsx
var a = 10;
var b = 20;
var c = 30;
export { a, b };
export default c;
```

 

옛날 방식  : `var 변수 = require(’경로’)`

`import / export`

→ ES6라 호환성이 안좋음 → IE에서 불가!

보통 프론트 개발에선 `<script src=””>` 사용

1. React, Angular 쓸때
2. 또는 JS 파일 나눌 때 사용

## **Stack, Queue를 이용한 웹브라우저 동작원리**

브라우저 동작원리를 알아야 하는 이유?

→ 자바스크립트를 해석해주는 엔진이 브라우저이기 때문에

→ but 코드를 해석하는 순서가 이상함

why?

1+1 하고

1초 쉬고

2+2 하고

파이썬 ver.

```python
print(1+1)

time.sleep(1)

print(2+2)
```

→ 자바스크립트 ver.

```jsx
console.log(1+1)
setTimeout(function(){}, 1000)
console.log(2+2)
```

→ 1초 쉬지 않고 그냥 함수 실행함 why? → 자바스크립트는 setTimeout 함수 안에 실행해야 코드가 작동함

```jsx
console.log(1+1)
setTimeout(function(){console.log(2+2)}, 1000)

```

→

```jsx
console.log(1+1)
setTimeout(function(){console.log(2+2)}, 1000)
console.log(3+3)
```

`console.log(1+1)` 먼저 출력되고 `console.log(3+3)` 그다음 출력되고 1초뒤에 `console.log(2+2)` 

→ 코드를 위에적든 밑에적든 빠른것부터 실행!

Stack : 코드 실행해주는 곳 (1개)

`setTimeout()` 은 바로 실행할 수 없기 때문에 잠깐 대기실로 치워버림

대기실 보내는 코드들 → Ajax 요청 코드, 이벤트리스너, setTimeout()

→ 대기가 끝나면 Queue에 줄세움 → 대기끝난 코드1, 대기끝난 코드2, 대기끝난 코드3 ..

→ Stack으로 하나씩 올림(Stack이 비어있을 때만 올려보냄)

![스크린샷 2022-03-11 오후 6.48.02.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e47dbc46-e486-4236-9ea9-ecf2a352000e/스크린샷_2022-03-11_오후_6.48.02.png)

for 반복문 → 많이 돌리면 오래걸림!

→ 자바스크립트로 시키면 안됨!

why? Stack에서 오래걸리는 연산을 시킨 상태에서는 버튼누르면 모달창 띄워주는 간단한 코드도 실행이 안됨!

(버튼눌러도 실행이 안됨) <-Stack이 비어 있을 때만 Queue에 있는 내용 올려주기 때문에

주의사항

1. Stack을 바쁘게 하지 말것
2. Queue를 바쁘게 하지 말것

자바스크립트는 동기적으로 처리됨(한번에 한줄씩 순서대로)

but 가끔 비동기적인 처리도 가능 → Ajax 요청 코드, 이벤트리스너, setTimeout()

Heap : 

## **동기/비동기처리와 콜백함수**

자바스크립트는 동기식처리(Synchronous)

→ 한번에 코드 한줄씩 차례로 실행

→ 병렬처리가 가능한 것은 아님! (한번에 한줄씩 처리하니까)

비동기처리(Asynchronous)

```jsx
console.log(1);
setTimeout(() => {
  console.log(2);
}, 1000);
console.log(3);

/*
1
3
2 -> 1초 뒤에 실행
*/

```

파이썬 → 

```python
print(1)
time.sleep(1) 
print(2)
```

파이썬의 `time.sleep()` 는 자바스크립트의 `setTimeout()` 와 같다.

but, `time.sleep()` 은 n초간 정지, `setTimeout()` 는 정지 하지 X

why? →`setTimeout()` 은 자바스크립트가 비동기식으로 처리할 수 있도록 도와줌

→ 오래걸리는 작업이 있으면 제껴두고 다른 작업부터 처리하는 방식

`addEventListener()` , `$.ajax()` → 오래걸리거나 실행까지 오래걸리는 함수들 

Web API(대기실) 덕분에 오래걸리는 작업이 있으면 제껴두고 다른 작업부터 처리하는 비동기식 처리가능

그냥 자바스크립트는 오래걸리는 연산 만나면 멈춤 ( = 동기식처리, Synchronous)

Web API와 연관된 특수한 함수들을 쓰면 작업이 오래걸릴때 다른거부터 실행하능(= 비동기식처리, asynchronous)

웹브라우저의 특수성 

Javascript를 순차적으로 실행하려면? → 콜백함수를 사용함

```jsx
console.log(1);
setTimeout(() => {}, 1000)
console.log(2)
```

자바스크립트는 이렇게 하면 안됨 

why? → `setTimeout(() => {}, 1000)` 이 코드가 1초간 Web API 대기실로 보내지기 때문에 `2` 는 1초뒤가 아니라 `1` 다음에 바로 출력됨

→ 콜백함수를 사용 (함수안에 함수)

```jsx
console.log(1);
setTimeout(() => {console.log(2)
}, 1000)
```

화살표 함수 대신 일반 함수로 표현하면

```jsx
console.log(1);
setTimeout(function() {console.log(2)
}, 1000)
```

```jsx
console.log(1);
setTimeout(function() {console.log(2)
}, 1000)
addEventListener('click', function(){})
```

→ setTimeout 함수안의 함수 `{console.log(2)}` 와 addEventListener 함수 안의 함수 `function(){}` 가 콜백함수 

`첫째함수()` 다음에 `둘째함수()` 실행하고 싶을 때

```jsx
function 첫째함수(구멍) {
  console.log(1);
  구멍();
}

function 둘째함수() {
  console.log(2);
}

첫째함수(둘째함수);
```

→ `첫째함수()` 먼저 실행하고 `1` 출력됨 → 그다음에 `둘째함수()` 가 출력됨

콜백함수는 동기/비동기가 아니고 함수 디자인 패턴일 뿐

비동기는 Ajax 요청 코드, 이벤트리스너, setTimeout() 이런 함수들

콜백함수의 문제점

→ 평소에 코딩할 때 함수이름을 많이 짓지 않음

→ 선언하고 바로 쓸 수도 있음

```jsx
첫째함수(function(){
    둘째함수(function(){
        셋째함수(function() {

        })
    })
});
```

→ 코드 너무 복잡하고 길어짐

→ 더 쉽게 쓰기 위해서 Promise 패턴 사용 (만들기는 어렵지만 쓸때 편리함)

Promise 패턴

```jsx
첫째함수().then(function(){

}).then(function(){
    
})
```

## Promise

→ 코드가 옆으로 길어지지 않아서 좋음

```jsx
var 프로미스 = new Promise();

프로미스.then(function(){

}).then(function(){

})
```

→ 실행에 실패했을 경우에도 코드실행 가능! (catch)

일반 콜백함수 → 1번 실행 후 2번 실행해 주세요 ~

Promise → 1번 실행 후 성공시 2번 실행해주세요 ~

실패시 3번 실행해 주세요~ 

성공 / 실패 판정 기계긴 Promise 디자인 하는법

```jsx
var 프로미스 = new Promise(function(resolve, reject){
    resolve(); // 성공판정 내리는 법
    reject(); // 실패판정 내리는 법
});

프로미스.then(function(){ // 성공하면 then 안에 있는 걸 실행

}).catch(function(){ //실패하면 catch 안에 있는 걸 실행

})
```

promise예시

어려운 연산이 끝나면 특정코드 실행하고 싶음

```jsx
var 프로미스 = new Promise(function(resolve, reject){
  var 어려운연산 = 1 + 1;
    **resolve()**; 
});

프로미스.then(function(){ // 성공하면 then 안에 있는 걸 실행
    console.log('성공했어요^^')
}).catch(function(){ //실패하면 catch 안에 있는걸 실행
    console.log('실패했어요^^')
})
```

→ `성공했어요^^` 출력

```jsx
var 프로미스 = new Promise(function(resolve, reject){
  var 어려운연산 = 1 + 1;
    **reject();** 
});

프로미스.then(function(){ // 성공하면 then 안에 있는 걸 실행
    console.log('성공했어요^^')
}).catch(function(){ //실패하면 catch 안에 있는걸 실행
    console.log('실패했어요ㅠㅠ')
})
```

→ `실패했어요ㅠㅠ` 출력 

성공 / 실패시 데이터 전달하기

함수안에 파라미터 추가 가능

```jsx
var 프로미스 = new Promise(function(resolve, reject){
  var 어려운연산 = 1 + 1;
    **resolve(어려운연산);** 
});

프로미스.then(function(**결과)**{ // 성공하면 then 안에 있는 걸 실행
    console.log(**결과**)
}).catch(function(){ //실패하면 catch 안에 있는걸 실행
    console.log('실패했어요ㅠㅠ')
})
```

→ `2` 출력

`1 + 1` → `어려운연산` → then 함수의 파라미터 `결과` → console.log(`결과`) 

1초 후에 성공하는 Promise 그리고 성공시 특정 코드를 실행하고 싶음

```jsx
var 프로미스 = new Promise(function(resolve, reject){
    **setTimeout(function(){
        resolve();
    },1000)**
});

프로미스.then(function(){ // 성공하면 then 안에 있는 걸 실행
    console.log('성공했어요^^')
}).catch(function(){ //실패하면 catch 안에 있는걸 실행
    console.log('실패했어요ㅠㅠ')
})
```

→ 1초 후에 `성공했어요^^` 출력

Promise의 3가지 상태

1. 성공하면 <resolved>
2.  판정 대기중이면 <pending>
3. 실패하면 <rejected>

Promise에 대한 오해

→ 비동기적 처리가 가능하게 바꿔주는 마법의 문법이 아님!

Promise가 적용된 곳들

`$.ajax().done(function(){})` → promise와 유사한 패턴

fetch() → promise를 return함 

`fetch().then().catch()` → 성공했을때 then `()` 를 실행, 실패했을 때 catch `()` 를 실행

## ES6 Promise 연습문제

**Q1. <img> 이미지 로딩 성공시 특정 코드를 실행하고 싶습니다.**

HTML 안에 있는 이미지 로딩이 끝나면 무언가 코드를 실행하고 싶습니다.

```jsx
<img id="test" src="https://codingapple1.github.io/kona.jpg">
```

이 이미지가 로드가 되면 콘솔창에 성공, 로드가 실패하면 콘솔창에 실패를 출력하고 싶은데

Promise 문법의 then, catch 함수를 사용해 만들고 싶습니다. 어떻게 코드를 짜면 될까요?

(참고) 이미지 로딩이 끝났다는 것은 <img>에 load라는 이벤트리스너를 붙여서 체크가 가능합니다.

(참고) 이미지 로딩이 실패했다는 것은 <img>에 error라는 이벤트리스너를 붙여서 체크가 가능합니다.

id가 test인 <img>가 로딩이 되었는지 / 로딩 실패했는지 판단하려면

```jsx
var img = document.querySelector('#test'); // 셀렉터로 이미지를 찾음

img.addEventListener('load', function(){
    // 로딩성공시 실행할 코드
});
img.addEventListener('error', function(){
   // 로딩실패시 실행할 코드
});
```

이렇게 하면 됩니다. 별거아닙니다.

그럼 이걸 Promise를 이용해서 로딩성공시 .then() 실패시 .catch()를 실행하도록 코드를 짜보도록 합시다.

```jsx
var 이미지로딩 = new Promise(function(성공, 실패){
  var img = document.querySelector('#test');
  img.addEventListener('load', function(){
      성공();
  });
  img.addEventListener('error', function(){
      실패();
  });

});

이미지로딩.then(function(){
  console.log('성공했어요')
}).catch(function(){
  console.log('실패했어요')
})

```

이렇게 짤 수 있겠습니다.

프로미스 안에서는 성공(), 실패()가 실행되는 경우의 수를 만들어주시면 되고

그렇게 하면 이제 .then() .catch()를 이용해서 성공/실패시 특정 코드들을 실행할 수 있습니다.

![스크린샷 2022-03-12 오전 10.55.20.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/03d4c5c8-8871-46af-a090-f05ca6cf5889/스크린샷_2022-03-12_오전_10.55.20.png)

 

**Q2. Ajax 요청이 성공하면 무언가 코드를 실행하고 싶습니다.**

https://codingapple1.github.io/hello.txt 라는 경로로 GET 요청을 하면 인삿말이 하나 딸려옵니다.

여기로 GET 요청을 해서 성공하면

Promise의 then 함수를 이용해서 Ajax로 받아온 인삿말을 콘솔창에 출력해주고 싶습니다.

어떻게 하면 될까요?

(jQuery done함수 자체에 Promise 기능이 있기 때문에 코드가 약간 중복도 많고 쓸데없을 수 있지만 연습삼아 해봅시다.)

```html
<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
```

일단 jQuery로 Ajax 요청을 하려면 `$.ajax`혹은 `$.get`을 쓰시면 됩니다.

(그리고 jQuery 설치 파일이 상단에 첨부되어있어야겠죠?)

```jsx
$.ajax({
  type : 'GET',
  url : 'URL 경로'
})

$.get('URL 경로')
```

둘중 하나 마음에 드는거 쓰시면 URL 경로 상에 있는 데이터를 가져올 수 있습니다.

그리고 가져온 데이터를 출력하거나 가져온 후에 특정 코드를 실행하고 싶다면

```jsx
$.ajax({
  type : 'GET',
  url : 'URL 경로'
}).done(function(결과){
  console.log(결과);
});

$.get('URL 경로').done(function(결과){
  console.log(결과)
});
```

`done`함수를 뒤에 붙여서 이렇게 쓰시면 됩니다.

결과라는 파라미터에 여러분이 가져온 데이터가 담겨져있습니다.

일단 위의 저 경로로 Ajax요청을 해봅시다.

$.get('요청할 URL')을 적어주시면 Ajax GET요청이 간단하게 가능합니다.

```jsx
$.get('https://codingapple1.github.io/hello.txt').done(function(결과){
  console.log(결과)
});
```

![스크린샷 2022-03-12 오전 11.09.30.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/491b102d-b7ac-441c-b258-8be224d03940/스크린샷_2022-03-12_오전_11.09.30.png)

이렇게 하시면 되겠군요. 콘솔창에 Ajax로 가져온 인삿말이 출력되죠?

근데 이걸 성공하면 Promise의 then 함수로 뭔가 코드를 실행시키고 싶다고 했죠?

그럼 Promise 기계를 하나 만들어줍니다. 그리고 안에 성공판정 기준도 하나 마련해주고요.

```jsx
var 프로미스 = new Promise(function(성공, 실패) {
    $.get('https://codingapple1.github.io/hello.txt').done(function(결과){
      성공(결과)
    });
});
```

기계가 완성되었습니다.

이제 프로미스에 then을 붙여서 성공시 뭔가 코드를 실행할 수 있습니다.

```jsx
var 프로미스 = new Promise(function(성공, 실패) {
    $.get('https://codingapple1.github.io/hello.txt').done(function(결과){
      성공(결과)
    });
});

프로미스.then(function(결과) {
  console.log(결과);
})
```

이제 프로미스가 성공하면 콘솔창에 결과가 출력되죠? 성공입니다.

**Q3. Promise chaining**

2번 문제에서 https://codingapple1.github.io/hello.txt 라는 경로로 GET 요청을 한 뒤에

.then을 이용해 인삿말을 콘솔창에 출력해보았습니다.

이번엔 그 직후 https://codingapple1.github.io/hello2.txt 라는 경로로 GET 요청을 또 하고

.then을 이용해 인삿말을 또 출력해보고 싶습니다.

쉽게 말하면

**1. hello.txt GET 요청**

**2. 그게 완료되면 hello2.txt GET 요청**

**3. 그게 완료되면 hello2.txt 결과를 콘솔창에 출력**

을 하고 싶다는 말입니다.

2번에서 만든 코드를 어떻게 업데이트하면 될까요?

**힌트1) 프로미스.then(()=>{둘째실행할거}).then(()=>{셋째실행할거})**

**이렇게 then을 여러개 이어붙여 만들어봅시다.**

**힌트2) .then()은 당연히 new Promise()로 생성한 프로미스 오브젝트들에 붙일 수 있습니다.**

**저는 어떻게 짰냐면**

이것도 그냥 jQuery done이나 콜백함수를 쓰는게 더 깔끔할 수 있겠지만

연습삼아 then을 여러개 사용해서 단계적으로 코드를 실행시켜보도록 합시다.

일단 이렇게 코드를 실행하고 싶다는 것입니다.

```jsx
var 프로미스 = new Promise(function(성공, 실패) {
    $.get('https://codingapple1.github.io/hello.txt').done(function(결과){
      성공(결과)
    });
});

//hello1.txt 가져오는 프로미스가 성공하면
프로미스.then(function(결과) {
  // 그럼 이제 hello2.txt도 가져와주세요
}).then(function(결과) {
  // hello2.txt 가져오면 콘솔창에 출력해주세요
})
```

then을 여러개 붙여서 뭔가 단계적으로 실행할 수 있습니다.

하지만 그냥 붙이면 안되고 then 함수는 new Promise()로 부터 생성된 오브젝트에만 붙일 수 있습니다.

그럼 then을 붙일 수 있게 첫째 then에서 return new Promise() 이런걸 해주면 되지 않을까요?

return 해주면 그 자리에 new Promise()가 남아서 거기 뒤에 .then을 붙일 수 있으니까요.

```jsx
var 프로미스 = new Promise(function(성공, 실패) {
    $.get('https://codingapple1.github.io/hello.txt').done(function(결과){
      성공(결과)
    });
});

프로미스.then(function(결과) {
  console.log(결과);

  var 프로미스2 = new Promise(function(성공, 실패) {
    $.get('https://codingapple1.github.io/hello2.txt').done(function(결과){
      성공(결과)
    })
  });

  return 프로미스2;

}).then(function(결과) {
    console.log(결과);
})
```

그래서 첫 then 안에 `프로미스2`를 만들고, 프로미스2는 두번째 ajax 요청을 해주고 성공판정을 내립니다.

그리고 프로미스2를 `return` 해주는 기능을 만들었습니다.

그럼 이제 뒤에 then을 붙여서 코드를 연달아 실행이 가능하겠군요.

흐름은 이렇습니다.

1. 첫프로미스가 성공하면 then() 안의 코드를 실행시켜줍니다.

2. 근데 거기 안에는 프로미스2가 있습니다. 프로미스2가 성공하면

3. 뒤에 있는 then() 안의 코드를 실행시켜줍니다.

그래서 이렇게 하시면 프로미스를 이용해 단계적으로 코드를 실행할 수 있습니다.

## async / await

promise → 순차적 실행을 위해 콜백함수 대신 쓸 수 있는 코딩 패턴

ES8 문법  → async / await

연산이 끝나면 특정 코드 실행하고 싶음

→ 콜백함수 디자인

```jsx
function 더하기(콜백) {
  1 + 1;
  콜백();
}
더하기(함수);
```

→ 콜백함수 대신 promise 사용

```jsx
function 더하기(콜백) {
  1 + 1;
  콜백();
}
더하기().then(function(){
    
})
```

→ 맨 위의 함수에 promise 사용하기 귀찮을 때 `async/await` 사용

→ `async`를 function 앞에 붙이면 함수가 Promise 역할 가능

```jsx
async function 더하기(콜백) {
  1 + 1;
  콜백();
}
더하기().then(function(){

})
```

→ async를 function 앞에 붙이면 함수 실행 후에 Promise 오브젝트가 남음( `더하기()` 자리에 남음)

```jsx
**async** function 더하기() {
  1 + 1;
}
더하기()**.then**(function(){
    console.log('성공이에요')
})
```

→ `new Promise() ~` 이렇게 디자인 안해도 `.then()` 사용 가능

`return`을 쓰면 함수 실행 결과를 출력할 수 있음!

```jsx
async function 더하기() {
  **return** 1 + 1;
}
더하기().then(function(**결과**){
    console.log(**결과**)
})
```

단점 → 성공만 판정할 수 있음, 실패 할 경우를 쓸 수 없음

강제로 실패를 보낼 수는 있음 

```jsx
async function 더하기() {
    **return Promise.reject('실패')**
  }
  더하기().then(function(결과){
      console.log(결과)
  })
```

![스크린샷 2022-03-12 오후 3.22.18.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/510f9b89-0232-4eec-bd17-1b2d8a014dce/스크린샷_2022-03-12_오후_3.22.18.png)

async function 안에서 쓰는 await

→ 함수 안에서 Promise 쓰기 

```jsx
async function 더하기() {
        var 프로미스 = new Promise(function(성공, 실패){
            var 힘든연산 = 1 + 1;
            성공();

        })
          }
          더하기().then(function(결과){
              console.log(결과)
          })
```

→ promise를 조금더 깔끔하게 쓸 수 있음

`then` 대신 `await`사용 가능함, `await` → 프로미스 해결될까지 기다려주셈!

```jsx
async function 더하기() {
        var 프로미스 = new Promise(function(성공, 실패){
            var 힘든연산 = 1 + 1;
            성공(**100**);
        })
        **var 결과 = await 프로미스;**
        console.log(결과);
          }
          더하기();
```

![스크린샷 2022-03-12 오후 3.52.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0af5448e-8e1d-42c4-bdde-893058d5f623/스크린샷_2022-03-12_오후_3.52.07.png)

`await` → `then()` 과 똑같다고 생각하면 됨!!

→ 프로미스 실패시 에러나고 멈춤

→ 실패가 나올거 같으면 실행해주는 자바스트립트 문법이 있음

`try {이걸해보고 에러나면} catch {이걸실행해주세요}`

→ 코드 멈춤없이 실행가능

```jsx
async function 더하기() {
        var 프로미스 = new Promise(function(성공, 실패){
            var 힘든연산 = 1 + 1;
            **실패**(100);
        })

        **try** {
        var 결과 = await 프로미스;
        console.log(결과);
          } **catch** {
              console.log('잘안되었군요')
          }
        }
```

![스크린샷 2022-03-12 오후 3.58.42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5fb97661-a8a0-4f35-9984-f1503023a8b0/스크린샷_2022-03-12_오후_3.58.42.png)

성공으로 바꾸면

```jsx
async function 더하기() {
        var 프로미스 = new Promise(function(성공, 실패){
            var 힘든연산 = 1 + 1;
            성공(100);
        })

        try {
        var 결과 = await 프로미스;
        console.log(결과);
          } catch {
              console.log('잘안되었군요')
          }
        }
```

![스크린샷 2022-03-12 오후 3.59.41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8fd2fbf6-8bba-48cc-9333-cc30d324affe/스크린샷_2022-03-12_오후_3.59.41.png)

예제)

Q. `<button>` 누르면 성공 판정하는 Promise 만들기

→ 성공시 `‘성공했어요'`출력하려면? (await 키워드 이용해서)

```jsx
async function 더하기() {
        var 프로미스 = new Promise(function(성공, 실패){
           document.getElementById('btn').addEventListener('click', function(){
               성공('성공했어요');
           })
        })
            var 결과 = await 프로미스;
            console.log(결과)
        }
          더하기();
```

![스크린샷 2022-03-12 오후 4.07.28.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b8f9af1b-7ab1-4798-9c5a-1d136d3be3e8/스크린샷_2022-03-12_오후_4.07.28.png)

## for in / for of

그냥 for 반복문 (어려움)

→ `forEach()` 반복문 (Array 전용)

→ `for in` 반복문 (Object 전용)

→ `for of` 반복문 (iterable 전용)

반복문 이용할 때

1. 코드를 여러번 실행할 때
2. Array, Object에서 자료를 꺼내쓸 때

for in 반복문 : Object 값을 하나씩 출력하고 싶을 때 

1. enumerable 한 것만 반복해줌( 셀 수 있는 것만)

```jsx
var 오브젝트 = {name : 'kim', age : 30};

        for (var key in 오브젝트){  // var 작명 in 반복할 object
        console.log(오브젝트[key])
        }
```

![스크린샷 2022-03-12 오후 5.13.40.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d211e69e-8b43-4021-827e-22a44e9d61d7/스크린샷_2022-03-12_오후_5.13.40.png)

오브젝트.name의 숨겨진 정보 출력

```jsx
var 오브젝트 = {name : 'kim', age : 30};
        Object.getOwnPropertyDescriptor(오브젝트, 'name'); // 오브젝트.name의 숨겨진 정보 출력
        
        for (var key in 오브젝트){  // var 작명 in 반복할 object
        console.log(오브젝트[key])
        }
```

![스크린샷 2022-03-12 오후 6.02.14.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c6f4e084-bb64-4ae4-940b-23ac7643263f/스크린샷_2022-03-12_오후_6.02.14.png)

→ ‘kim’이외에 숨겨진 정보 3개

enumerable이 true 이면 반복문에서 출력이 가능함!

일반 자료들은 항상 enumerable이 true가 기본값

1. 부모의 prototype도 반복해줌

→ but, 부모 prototype까지 반복할 일이 별로 없음!

1. 보통 Object 자료형에만 씀 

Array → for, forEach() 사용

for of 반복문 → forEach() 보다 더 간단함

→ Array, 문자, arguments, NodeList, Map, Set

for of 반복문 → iterable한 자료형에만 사용가능

```jsx
var 어레이 = [2,3,4,5];

        for (var 자료 of 어레이){  // var 작명 in 반복할 object
            console.log(자료)
           }
```

![스크린샷 2022-03-12 오후 6.13.32.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d3a3b4a-79b2-47d1-b8f2-d4b6d937b295/스크린샷_2022-03-12_오후_6.13.32.png)

→ string도 가능

```jsx
var 어레이 = [2,3,4,5];

        for (var 자료 of 'ㅁㄴㅇㅂㅇ'){  // var 작명 in 반복할 object
            console.log(자료)
           }
```

![스크린샷 2022-03-12 오후 6.15.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/275d5c97-19f9-432f-a354-5f7cd6314dbc/스크린샷_2022-03-12_오후_6.15.51.png)

`어레이[Symbol.iterator]();` → 내부 데이터 출력을 도와주는 함수 같은 것(중요하지는 X)

![스크린샷 2022-03-12 오후 6.19.06.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9018d2d-51df-4a40-9858-69d151c84c87/스크린샷_2022-03-12_오후_6.19.06.png)

참고) NodeList가 무엇인가

```jsx
document.getElementsByClassName(); // [HTML1, HTML2] // 이런게 남음.. array는 아니고 NodeList
        document.querySelectorAll();
```

## Symbol

실용적인 자료형은 아님, 참고용

심볼 만드는 법

```jsx
var 심볼 = Symbol('설명')
```

`Symbol(설명)` 

심볼의 용도 : Object의 key 값으로 사용할 수 있음

비밀스런 데이터를 저장하고 싶다면? → `Symbol()` 사용

```jsx
var person = {name : 'kim'}
        person.weight = 100;
```

→ 기존의 데이터 추가하는 방법은 너무 오픈되어 있음

원래의 Object의 key값은 문자만 가능했는데 ES6부터 Symbol을 집어넣을 수 있음

```jsx
var 심볼 = Symbol('설명')

        var weight = Symbol('내 시크릿 몸무게')
        var person = {name : 'kim'}
        person.weight = 100;
        person[weight] = 100;
```

→ `{ name: 'kim', weight: 100, Symbol(내 시크릿 몸무게) }` 

```jsx
var 심볼 = Symbol('설명')

        var weight = Symbol('내 시크릿 몸무게')

        var person = {name : 'kim'}
        person.weight = 100;
        person[weight] = 100;
        
        for (var key in person){
            console.log(person[key])
```

![스크린샷 2022-03-12 오후 8.49.46.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b08878f-7342-4e03-8f40-6cfd9ac42027/스크린샷_2022-03-12_오후_8.49.46.png)

`person[weight] = 100;` → 반복문에서 출력안됨 why? enumerable 하지 않기 때문에

import 해온 파일 / 라이브러리 쓸 때 거기 있던 object에 자료를 추가하고 싶다면 

Symbol 특징

1. 설명이 같다고 같은 Symbol이 아님 

→  Symbol 만들때 마다 유니크한 Symbol이 생김

`a === b` → `false`

```jsx
var a = Symbol('설명1');
var b = Symbol('설명1')
```

1. 전역 변수같은 전역 Symbol

`Symbol.for()` 로 만드는 전역 심볼

→ 위에 이미 있으면 기존 심볼을 복붙해줌

```jsx
var a = Symbol.for('설명1');
var b = Symbol.for('설명1');
```

=

```jsx
var a = Symbol.for('설명1');
var b = a
```

→ `a === b` → `true`

1. 기본 내장 Symbol들

```jsx
var 어레이 = [2,3,4];
어레이[Symbol.iterator] // array에 집어넣는 기본 Symbol
```

## Map / Set

Map 자료형 → key, value를 저장

```jsx
var person = new Map();
        person.set('name', 'kim');
```

![스크린샷 2022-03-12 오후 10.20.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb353dee-a43f-411e-ac0c-7bee3af7a46a/스크린샷_2022-03-12_오후_10.20.07.png)

```jsx
var person = new Map();
        person.set('name', 'kim');
        person.set('age', 20);
```

![스크린샷 2022-03-12 오후 10.22.13.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2b49e74c-c5ce-4c7d-84f3-fe858370bd49/스크린샷_2022-03-12_오후_10.22.13.png)

Map 자료형은 자료간의 연관성을 표현하기 위해서 씀

Object 자료형은 자료 이름으로 글자만 가능

Map 자료형은 다 가능

`name` 대신 `100`으로 변경 (숫자형)

```jsx
var person = new Map();
        person.set(**100**, 'kim');
        person.set('age', 20);
```

![스크린샷 2022-03-12 오후 10.24.57.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/235cb00b-7a85-4daf-b76f-113a53f75dc9/스크린샷_2022-03-12_오후_10.24.57.png)

`name` 대신 `[1,2,3]` (어레이)

```jsx
var person = new Map();
        person.set([1,2,3], 'kim');
        person.set('age', 20);
```

→ `Map()` 은 키와 값을 아무 자료나 이용해서 입력할 수 있음

### Map에서 자료 꺼내는 법

`person.get('age')` → `get` 사용

삭제할 때 → `person.delete.('age')` → `delete` 사용

반복문 사용할 수 있음 (자주 사용함)

```jsx
for(var key of person.keys()){
            console.log(key)
        }
```

Map 자료형에 직접 자료 집어 넣을 때(대괄호 2개)

```jsx
var person = new Map([
        ['name', 'kim'], ['age', 20]
        ])
```

## Set 자료형

집합(어레이)와 유사함

중복 자료를 허용하지 않는 Array 비슷한 것

```jsx
var 출석부 = ['john', 'tom', 'andy', 'tom'];
        
        var 출석부2 = new Set(['john', 'tom', 'andy', 'tom']);
```

![스크린샷 2022-03-12 오후 10.39.13.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/086f286d-0aeb-4132-8f81-beae4e28e54b/스크린샷_2022-03-12_오후_10.39.13.png)

![스크린샷 2022-03-12 오후 10.39.30.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/436e64c6-c9c8-4ed7-86ef-677bbd329d2e/스크린샷_2022-03-12_오후_10.39.30.png)

→ 출석부2는 ‘tom’의 중복을 허용하지 X

Set 자료형에 자료 추가하기

```jsx
var 출석부 = ['john', 'tom', 'andy', 'tom'];
        
        var 출석부2 = new Set(['john', 'tom', 'andy', 'tom']);
        출석부2.add('sally')
```

![스크린샷 2022-03-12 오후 10.41.45.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9cc63b1d-b2f7-485c-a48d-5dbecc1d154f/스크린샷_2022-03-12_오후_10.41.45.png)

자료 제거하기

```jsx
var 출석부 = ['john', 'tom', 'andy', 'tom'];
        
        var 출석부2 = new Set(['john', 'tom', 'andy', 'tom']);
        출석부2.delete('sally')
```

![스크린샷 2022-03-12 오후 10.42.39.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9aa38645-8f88-4489-84d7-43b183653c13/스크린샷_2022-03-12_오후_10.42.39.png)

있는지 없는지 boolean 값으로 확인

```jsx
var 출석부 = ['john', 'tom', 'andy', 'tom'];
        
        var 출석부2 = new Set(['john', 'tom', 'andy', 'tom']);
        출석부2.has('sally')
```

![스크린샷 2022-03-12 오후 10.44.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c7e1097-49c8-4a15-ab3a-c2b51bacfbce/스크린샷_2022-03-12_오후_10.44.05.png)

자료의 개수 확인

![스크린샷 2022-03-12 오후 10.44.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/40edd3ba-641a-4f69-a574-116158f504ab/스크린샷_2022-03-12_오후_10.44.53.png)

Set 자료형 ←→ Array 자료형

활용문제 : Array의 중복자료를 제거하고 싶으면??

![스크린샷 2022-03-12 오후 10.47.14.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3897f40e-0653-4191-b4b0-7357b38a3f42/스크린샷_2022-03-12_오후_10.47.14.png)

```jsx
var 출석부 = ['john', 'tom', 'andy', 'tom'];
        
        var 출석부2 = new Set(['john', 'tom', 'andy', 'tom']);
        출석부 = [...출석부]
```

![스크린샷 2022-03-12 오후 10.48.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ed664fc-4acd-4409-9390-3811c73ae79a/스크린샷_2022-03-12_오후_10.48.51.png)

Set 자료형에 반복문 돌리기

## **Web Components**

Web Components → 자바스크립트 문법X, 브라우저 기본 기능

<커스텀태그>로 길고 복잡한 HTML 축약

<lavel>, <input> → <custome-input>

```jsx
<custom-input></custom-input>
    <script>

        class 클래스 extends HTMLElement {
            connectedCallback(){ // 내가 만든 태그가 HTML에 정착될 때 실행할 코드 적는 곳 
                this.innerHTML = `<label>이메일인풋이에요</label><input>`
            }
        }
        customElements.define('custom-input', 클래스);
</script>
```

![스크린샷 2022-03-12 오후 11.17.12.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0576fc64-f81b-49a6-af8d-4d5c4784a457/스크린샷_2022-03-12_오후_11.17.12.png)

`this` → 클래스로부터 새로 생성될 오브젝트 (`instance`) → 새로 생성될 `<custom-input>` 요소

<커스텀태그> 장점은

html 중복제거, 다른 페이지에서 재활용가능

<커스텀태그> 안에서도 파라미터 문법 구현 가능

```jsx
<custom-input **name**="비번"></custom-input> // 
    <custom-input **name**="이메일"></custom-input> //
    <script>

        class 클래스 extends HTMLElement {
            connectedCallback(){ // 내가 만든 태그가 HTML에 정착될 때 실행할 코드 적는 곳 
                let **name** = this.getAttribute('**name**')
                this.innerHTML = `<label>${**name**}인풋이에요</label><input>`
            }
        }
        customElements.define('custom-input', 클래스);
    
    </script>
```

![스크린샷 2022-03-12 오후 11.42.09.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d453b9f3-38be-444c-ad19-7f898215857f/스크린샷_2022-03-12_오후_11.42.09.png)

attribute 변경 감지 기능 제공됨

React, Vue 특징

→ Props(attribute) 변경되면 html 자동 재렌더링됨

attribute 변경할 때마다 html 재렌더링 할 때? 

```jsx
<script>

        class 클래스 extends HTMLElement {
            connectedCallback(){ // 내가 만든 태그가 HTML에 정착될 때 실행할 코드 적는 곳 
                let name = this.getAttribute('name')
                this.innerHTML = `<label>${name}인풋이에요</label><input>`
            }
            static get observedAttributes() {
                return ['name']
            }
            attributeChangedCallback(){
                **this.innerHTML = `<label>${name}인풋이에요</label><input>`**
            }
        }
        customElements.define('custom-input', 클래스);
    </script>
```

→ Web Components 기능 쓰면 긴 HTML도 함수처럼 재사용 가능!