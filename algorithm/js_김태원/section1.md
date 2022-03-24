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

## 4. 1부터 N까지 합

자연수 N이 입력되면 1부터 N까지의 합을 출력하는 프로그램을 작성하세요.

▣ 입력설명
첫 번째 줄에 20이하의 자연수 N이 입력된다..

▣ 출력설명
첫 번째 줄에 1부터 N까지의 합을 출력한다.

- ▣ 입력예제 1
6
- ▣ 출력예제 1
21
- ▣ 입력예제 2
10
    
    ▣ 출력예제 2
    55
    

누적하는 방법, for문 돌리는 법

```jsx
function solution(n){
    let answer =0; // answer는 0
    for(let i = 1; i<=n; i++ ){ // i는 1부터 n까지
        answer=answer+i; // 
    }
     return answer;
}

console.log(solution(10)); // 55
```

오른쪽을 연산 다 하고 왼쪽에 갱신됨

answer =  answer + i

 `1`(오른쪽은 나중에) = `0 + 1`(왼쪽먼저)

`3` = `1 + 2` 

`6` = `3 + 3`

`10` = `6 + 4`

... 

`55` = `45 + 10`

## 5. 최솟값 구하기

7개의 수가 주어지면 그 숫자 중 가장 작은 수를 출력하는 프로그램을 작성하세요.

▣ 입력설명
첫 번째 줄에 7개의 수가 주어진다.

▣ 출력설명
첫 번째 줄에 가장 작은 값을 출력한다.

▣ 입력예제 1
5 3 7 11 2 15 17

▣ 출력예제 1
2

```jsx
function solution(arr){         
                let answer, min=Number.MAX_SAFE_INTEGER; // 안정적인 가장 큰 정수값이 min에 기록됨
                for(let i=0; i<arr.length; i++){
                    if(arr[i]<min) min=arr[i]; // 해당값이 min보다 작으면 min을 그 값으로 바꿔줌
                }
                answer=min;
                return answer;

            }

            let arr=[5, 7, 1, 3, 2, 9, 11];
            console.log(solution(arr));
```

→ `arr[0]` 은 `5` 이고 `MAX_SAFE_INTEGER` 보다 무조건 작으니까 `min`에 `5`가 들어감

... → `min`에 `1` 이 저장됨

for문 말고 내장함수(배열의 최솟값)로 구할 수 있음

```jsx
function solution(arr) {
  let answer = Math.min(...arr); // 배열그대로 넣으면 NaN 출력함
  return answer;
}

let arr = [5, 7, 1, 3, 2, 9, 11];
console.log(solution(arr));// 1 
```

## 6. 홀수

7개의 자연수가 주어질 때, 이들 중 홀수인 자연수들을 모두 골라 그 합을 구하고, 고른 홀수들
중 최소값을 찾는 프로그램을 작성하세요.
예를 들어, 7개의 자연수 12, 77, 38, 41, 53, 92, 85가 주어지면 이들 중 홀수는 77, 41, 53, 85이므로 그 합은

77 + 41 + 53 + 85 = 256

이 되고,

41 < 53 < 77 < 85
이므로 홀수들 중 최소값은 41이 된다.

▣ 입력설명
첫 번째 줄에 자연수 7개가 주어진다. 주어지는 자연수는 100보다 작다. 홀수가 한 개 이상
반드시 존재한다.

▣ 출력설명
첫째 줄에 홀수들의 합을 출력하고, 둘째 줄에 홀수들 중 최소값을 출력한다.

▣ 입력예제 1
12 77 38 41 53 92 85

▣ 출력예제 1
256
41

```jsx
function solution(arr){
    let answer=[]; // 빈배열 만들기
    let sum=0, min=Number.MAX_SAFE_INTEGER;
    for(let x of arr){ // x라는 변수로 받기
        if(x%2===1){ // 홀수이면
            sum+=x; // 홀수값들 더해라 (sum = sum + x)
            if(x<min) min=x;
        }
    }
    answer.push(sum);
    answer.push(min);     
    return answer;
}

arr=[12, 77, 38, 41, 53, 92, 85];
console.log(solution(arr)); // [ 256, 41 ]
```

`for of` 구문 사용