# 08장  제어문

- 제어문? 조건에 따라 코드 블록을 실행하거나 반복 실행 할때 사용하는 문

## 8.1 블록문

- 블록문(block statement/compound statement) : 0개 이상으 ㅣ문을 중괄호로 묶은것, 코드 블럭, 또는 블럭

  - 하나의 실행단위로 취급
  - 블록문의 끝에는 세미콜론을 붙이지 않는다.

- 예제 08-01

  ```javascript
  // 블록문
  {
      var foo = 10;    
  }
  
  // 제어문
  var x = 1;
  if (x < 10) {
      x++;
  }
  
  // 함수 선언문
  function sum(a, b) {
      return a + b;
  }
  ```

## 8.2 조건문

- 조건문 : 주어진 조건식의 평가 결과에 따라 코드블럭을 실행 한다.
- 조건식은 블리언 값으로 평가될 수 있는 표현식이다.
- if ... else문과 switch 문 두가지 조건문을 제공

### 8.2.1 if ... else 문

```javascript
if (조건식) {
    // 조건이 참이면 이 코드 블록이 실행
} else {
    // 조건식이 거짓이면 이 코드 블럭이 실행
}

if (조건식) {
    // 조건식이 참이면 이 코드 블럭이 실행
}

if (조건식1) {
    // 조건식1이 참이면 이 코드 블럭이 실행
} else if (조건식2) {
    // 조건식2가 참이면 이 코드 블럭이 실행
} else {
    // 조건식1,2가 모두 거짓이면 이 코드 블럭 실행
}

// 코드 블럭 내에 문이 하나라면 중괄호 생략 가능

var num = 2;
var kind;
if (num > 0) 	 kind = '양수';
else if(num < 0) kind = '음수';
else			kind = '영';

console.log(kind); // 양수
```

- 조건식이 블리언 값이 아닌경우 자바스크립트 엔진에 의해 암묵적으로 블리언 값으로 강제 변환

- if ... else문은 삼항 조건 연산자로 바꿀 수 있다.

  ```javascript
  var num = 2;
   var kind = num ? (num > 0 ? '양수' : '음수') : '영';
  ```

### 8.2.2 switch 문

- 표현식과 일치하는 case문을 실행하며, 업삳면 default 문으로 이동한다.

  ```javascript
  switch (표현식) {
      case 표현식1:
          // switch 문의 표현식1과 표현식1이 일치하면 실행;
          break;
      case 표현식2:
          // switch 문의 표현식2과 표현식1이 일치하면 실행;
          break;
      default:
          // switch 문과 일치하지 않으면 실행;
  }
  ```

- case문 마지막에는 break문을 사용해야 빠져나온다

- default 문에는 break를 생략하는 것이 일반적이다.

- 필요에 따라 break문을 생략하기도 한다(윤년 계산)

- 가독성과 필요에 따라 if .. else, switch 문중 필요한 조건문을 사용하는것이 좋다.

## 8.3 반복문

- 반복문 : 조건식의 평가 결과가 참인 경우 코드 블럭을 실행, 조건식이 참일경우 계속 반복

### 8.3.1 for 문

- 예제

  ```javascript
  for (변수 선언문 또는 할당문; 조건식; 증감식) {
      조건이 참인경우 반복 실행될 문;
  }
  
  for (var i = 0; i < 2; i++) {
      console.log(i);
  }
  ```

  ![image-20210818143113838](https://raw.githubusercontent.com/redplug/shareimages/master/img/image-20210818143113838.png)

  ![image-20210818143127027](https://raw.githubusercontent.com/redplug/shareimages/master/img/image-20210818143127027.png)

- 무한루프

  ```javascript
  for( ;; ) { ... }
  ```

- 중첩 사용

  ```javascript
  for (var i = 1; i <= 6; i++) {
      for (var j = 1; j <= 6; j++){
          if (i + j == 6) console.log('[${i}, ${j}]');
      }
  }
  
  // 결과
  [1, 5]
  [2, 4]
  [3, 3]
  [4, 2]
  [5, 1]
  ```

### 8.3.2 while 문

- for문은 반복횟수가 명확할때 주로 사용

- while는 반복횟수가 불명확할떄 주로 사용

  ```javascript
  var count = 0;
  
  // count가 3보다 작을 때까지 코드 블록을 계속 반복실행한다.
  while (count < 3) {
      console.log(count); // 0 1 2
      count++;
  }
  ```

- 무한루프를 탈출하기 위해서는 중간에 break문을 넣는다.

  ```javascript
  var count = 0;
  
  // 무한루프
  while (true) {
      console.log(count);
      count++;
      if (count === 3) break;
  } // 0 1 2
  ```

### 8.3.3 do ... while문

- 코드 블록을 먼저 실행하고 조건식을 평가 -> 코드 블록은 무조건 한번 이상 실행

  ```javascript
  var count = 0;
  
  // count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
  do {
      console.log(count); // 0 1 2
      count++;
  } while (count < 3);
  ```

## 8.4 break문

- 레이블문, 반복문, switch문의 코드 블록에서 탈출할 때 사용.
- 레이블문 : 식별자가 붙은 문
- 중첩된 for문 내부에서 break문을 실행하면 내부 for문을 탈출하여 외부 for문ㅇ 진입.

## 8.5 continue 문

- 반복문의 코드 블록 실행을 현 시점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
- break문처럼 반복문을 탈출하지는 않는다.
