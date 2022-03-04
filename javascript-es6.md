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
