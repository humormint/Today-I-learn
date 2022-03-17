# 섹션1, 기본 문제 풀이

## 1. 세 수 중 최솟값

100이하의 자연수 A, B, C를 입력받아 세 수 중 가장 작은 값을 출력하는 프로그램을 작성하
세요.(정렬을 사용하면 안됩니다)

▣ 입력설명
첫 번째 줄에 100이하의 세 자연수가 입력된다.

▣ 출력설명
첫 번째 줄에 가장 작은 수를 출력한다.

▣ 입력예제 1
6 5 11

▣ 출력예제 1
5

나의 풀이

```jsx
function solution(a, b, c) {
  let answer;
  if (a < b && a < c) {
    answer = a;
  } else if (b < a && b < c) {
    answer = b;
  } else if (c < a && c < b) {
    answer = c;
  }
  return answer;
}

console.log(solution(6, 5, 11));

// output : 5
```

정답

```jsx

            function solution(a, b, c){
                let answer;
                if(a<b) answer=a;
                else answer=b; // answer에는 a,b 둘중 작은 값이 들어가 있음
                **if(c<answer) answer=c; 
                return answer;**
            }

            console.log(solution(2, 5, 1));
    
```

## 2. 삼각형 판별하기

길이가 서로 다른 A, B, C 세 개의 막대 길이가 주어지면 이 세 막대로 삼각형을 만들 수 있
으면 “YES"를 출력하고, 만들 수 없으면 ”NO"를 출력한다.

▣ 입력설명
첫 번째 줄에 100이하의 서로 다른 A, B, C 막대의 길이가 주어진다.

▣ 출력설명
첫 번째 줄에 “YES", "NO"를 출력한다.

▣ 입력예제 1
6 7 11

▣ 출력예제 1
YES

▣ 입력예제 1
13 33 17

▣ 출력예제 1
NO

→ ‘최솟값 구하기’ 의 응용버전 

→ 짧은 막대의 합이 긴 막대의 합보다 작아야 한다. 

짧은 막대 합 ≤ 긴 막대 → NO 

짧은 막대 합 > 긴 막대 → YES

정답

```jsx
function solution(a, b, c){
    let answer="YES", max; // max는 가장 긴 막대의 길이
    let tot=a+b+c; // 세수의 합

    if(a>b) max=a; // a가 b보다 크면 가장 긴 막대의 길이에 a를 넣고
    else max=b; // 그렇지 않으면 b를 넣음
    if(c>max) max=c;
    if(tot-max<=max) answer="NO"; // tot-max = 세 수의합-가장 긴 막대 = 짧은 두 막대의 합 
    return answer;
}

console.log(solution(13, 33, 17));
```

## 3. 연필 개수

연필 1 다스는 12자루입니다. 학생 1인당 연필을 1자루씩 나누어 준다고 할 때 N명이 학생수
를 입력하면 필요한 연필의 다스 수를 계산하는 프로그램을 작성하세요.

▣ 입력설명
첫 번째 줄에 1000 이하의 자연수 N이 입력된다.

▣ 출력설명
첫 번째 줄에 필요한 다스 수를 출력합니다.

▣ 입력예제 1
25

▣ 출력예제 1
3

▣ 입력예제 2
178

▣ 출력예제 2
15

→ 12자루가 1다스

→ 12로 나눈 몫에다가 +1 (나머지 연필만 담는 다스도 필요하니까)

나의 풀이

```jsx
function solution(a){
    let answer;
    answer = **parseInt(a/12 + 1)**;
     return answer;
}

console.log(solution(25));
```

정답

```jsx
function solution(n){
                let answer;
                answer=**Math.ceil(n/12)**; // 올림 
                return answer;
            }

            console.log(solution(178));
```

참고)

`Math.round()` → 반올림

`Math.floor()` → 내림