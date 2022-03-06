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

```jsx
document.getElementById('버튼').addEventListener('click', function(e){

        var 어레이 = [1, 2, 3];
        어레이.forEach(function(a){
            console.log(**this**) //
        });
        })
```

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

→ 첫번째 if문 안은 `var b = 2;` 만 남고, 두번째 if문은 `let b = 3;` 가 줄괄호 안에서 쓰이고 끝났기 때문에 외부에서 출력한 b 는 `2`가 된다.

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

<script>
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

</script>
```

`document.querySelectorAll`은 `jQuery의 $('')` 셀렉터와 매우 유사합니다. 동시에 여러 요소를 찾아 어레이 비슷한 자료형에 담아줌

0번째 버튼을 누르면 0번째 모달창,

1번째 버튼을 누르면 1번째 모달창을 보여줌

→ 반복문 안에 담아서 한번 다시 개발

```jsx
<script>
var 버튼들 = document.querySelectorAll('button');
var 모달창들 = document.querySelectorAll('div');

for (var i = 0; i < 3; i++){

  버튼들[i].addEventListener('click', function(){
    모달창들[i].style.display = 'block';
  });

}

</script>
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

→ 그 부분은 **반복문과 동시에 실행되지 않습니다. 좀 나중에 클릭 되면 실행되겠죠 뭐.**

누군가 버튼을 클릭하면 addEventListener 내의 **`모달창들[i].style.display = 'block';`**코드가 발동됨

but, i를 쓰고싶어서 주변을 살펴보았더니 i값은 3밖에 없음

why? → 아까 반복문이 3번 실행되면서 i값은 0,1,2,3 ... 이렇게 차례로 변하다가 i값이 3이 되어 종료

i 값은 var로 만든 전역변수 → i값을 쓰려고 봤더니 **전역변수 i = 3밖에 없어서 3을 집어넣어서 계속 에러발생**

해결책은 for 반복문에서 i변수를 만들 때 `var` 대신 `let`으로 바꾸는 것!!

반복문이 돌고 나서도 let i = 어쩌구 값이 {for 반복문} 내에 남아있기 때문에 그걸 **`모달창들[i].style.display = 'block';`** 의 i값으로 가져다 쓰게 됨
