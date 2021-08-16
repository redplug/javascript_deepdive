# 06장 데이터 타입

- 자바스크립트의 모든 값은 데이터 타입을 갖는다.

- 자바스크립트는 7개의 데이터 타입을 제공한다. 원시타입과 객체 타입으로 분류할 수 있다.

| 구분      | 데이터 타입          | 설명                                                |
| --------- | -------------------- | --------------------------------------------------- |
| 원시타입  | 숫자(number) 타입    | 숫자, 정수와 실수 구분 없이 하나의 숫자 타입만 존재 |
| 원시타입  | 문자열(string) 타입  | 문자열                                              |
| 원시타입  | 불리언(boolean) 타입 | 논리적 참(true)과 거짓(false)                       |
| 원시타입  | undefined 타입       | var 키워드로 선언된 변수에 암묵적으로 할당되는 값   |
| 원시타입  | null 타입            | 값이 없다는 것을 의도적으로 명시할 때 사용하는 값   |
| 원시타입  | 심벌(symbol) 타입    | ES6에서 추가된 7번째 타입                           |
| 객체 타입 | 객체 타입            | 객체 함수, 배열 등                                  |



## 6.1  숫자 타입

- int, long, float, double를 구분하지 않는 하나의 숫자 타입만 존재

- 64비트 부동소수점 형식, 정수만을 위한 데이터 타입이 별도로 존재 하지 않음.

- 예제 06-01

  ```javascript
  // 모두 숫자 타입이다.
  var integer = 10; // 정수
  var double = 10.12; // 실수
  var negative = -20; // 음의 정수
  ```

- 2진수, 8진수, 16진수를 표현하기 위한 데이터 타입을 제공하지 않음.

- 예제 06-02

  ```javascript
  var binary = 0b01000001; // 2진수
  var octal = 0o101; // 8진수
  var hex = 0x41; // 16진수
  
  // 표기법만 다를 뿐 모두 같은 값이다.
  console.log(binary); // 65
  console.log(octal); // 65
  console.log(hex); // 65
  console.log(binary === octal); // true
  console.log(octal === hex); // true
  ```

- 모든 수는 실수로 처리, 정수로 표시되는 수끼리 나누더라도 실수가 나올 수 있다.

- 예제 06-03

  ```javascript
  // 숫자 타입은 모두 실수로 처리된다.
  console.log(1 === 1.0); // true
  console.log(4 / 2); // 2
  console.log(3 / 2); // 1.5
  ```

- 세가지 특별한 값도 표현할 수 있다.

  - Infinity : 양의 무한대
  - -Infinity : 음의 무한대
  - NaN: 산술 연산 불가 (Not-a-number)

- 예제 06-04

  ```javascript
  // 숫자 타입의 세 가지 특별한 값
  console.log(10 / 0); // Infinity
  console.log(10 / -0); // -Infinity
  console.log(1 * 'String'); // NaN
  ```

- 자바 스크립트는 대 소문자를 구별하므로 NaN으로 표기 해야 한다.

- 예제 06-05

  ```javascript
  // 자바스크립트는 대소문자를 구별한다.
  var x = nan; // ReferenceError: nan is not defind
  ```

## 6.2 문자열 타입

- 텍스트 데이터를 나타내는 데 사용

- 문자열은 작은 따옴표(''), 큰따옴표(""), 또는 백틱(``)으로 텍스트를 감싼다.

- 예제 06-06

  ```javascript
  // 문자열 타입
  var string;
  string = '문자열'; // 작은따옴표
  string = "문자열"; // 큰따옴표
  string = `문자열`; // 백틱(ES6)
  
  string = '작은따옴표로 감싼 문자열 내의 "큰따옴표"는 문자열로 인식된다.'
  string = "큰따옴표로 감싼 문자열 내의 '작은따옴표'는 문자열로 인식된다."
  ```

- 문자열을 따옴표로 감싸는 이유는 키워드나 식별자 같은 토큰과 구별하기 위함.

- 예제 06-07

  ```javascript
  // 따옴표로 감싸지 않은 hello를 식별자로 인식한다.
  var string = hello; // ReferenceError: hello is not defined
  ```

- 따옴표로 문자열을 감싸지 않는다면 스페이스와 같은 공백 문자도 포함이 불가.

- 자바스크립트의 문자열은 원시 타입이며, 변경 불가능한 값(immutable value)

## 6.3 템플릿 리터럴

- ES6부터 템플릿 리터럴(template literal)이라고 하는 새로운 문자열 표기법이 도입

- 멀티라인 문자열(multi-lien string), 표현식 삽입(expression interpolation), 테그드 템플릿(tagged template) 등 문자열 처리기능을 제공한다. 백틱을 사용해 표현한다.

- 예제 06-08

  ```javascript
  var template = `Template literal`;
  console.log(template); // Template literal
  ```

### 6.3.1 멀티라인 문자열

- 일반 문자열은 줄바꿈이 허용 불가 -> 백슬래시로 시작하는 이스케이프 시퀸스를 사용

- 템플릿 리터럴 내에서는 이스케이프 시퀸스를 사용하지 않고 줄바꿈이 허용

- 예제 06-11

  ```javascript
  var template = `<ul>  <li><a href="#">Home</a></li></ul>`;console.log(template);
  ```

### 6.3.2 표현식 삽입

- 표현식을 삽입하려면 ${}로 표현식을 감싼다.

- 예제 06-14

  ```javascript
  console.log(`1 + 2 = ${1 + 2}`); // 1 + 2 = 3
  ```

## 6.4 불리언 타입

- true 와 false

- 조건문에 자주 사용함

- 예제 06-16

  ```javascript
  var foo = true;console.log(foo); // truefoo = false;console.log(foo); // false
  ```

## 6.5 undefined 타입

- undefined가 유일

- var로 선언한 변수는 undefined로 초기화

- 예제 06-17

  ```javascript
  var foo;console.log(foo); // undefined
  ```

- 변수에 값이 없다고 명시하고 싶을 때는 null을 할당함.

## 6.6 null 타입

- null이 유일한 값.

- 변수에 값이 없다는 것을 의도적으로 명시

- 함수가 유효한 값을 반환할 수 없는 경우 명시적으로 null을 반환

- 예제 06-18

  ```javascript
  var foo = 'Lee';// 이전 참조를 제거. foo 변수는 더 이상 'Lee'를 참조하지 않는다.// 유용해 보이지는 않는다. 변수의 스코프를 좁게 만들어 변수 자체를 재빨리 소멸시키는 편이 낫다.foo = null;
  ```

  

## 6.7 심벌 타입

- ES6에 추가, 변경 불가능한 원시 타입 값

- 다른 값과 중복되지 않는 유일무이한 값

- 객체의 유일한 프로퍼티 키를 만들기 위해 사용

- Symbol 함수를 호출해 생성

- 예제 06-20

  ```javascript
  // 심벌 값 생성var key = Symbol('key');console.log(typeof Key); // symbol// 객체 생성var obj = {};// 이름이 충돌할 위험이 없는 유일무이한 값인  심벌을 프로퍼티 키로 사용한다.obj[key] = 'value';console.log(obj[key]); // value
  ```

## 6.8 객체 타입

- 11장에서 자세히 다룸.
- 객체 기반 언어이며, 상기 타입을 제외한 건 모두 객체 타입이다.

## 6.9 데이터 타입의 필요성

- 값을 저장할 때 확보해야 하는 **메모리 공간의 크기**를 결정하기 위해
- 값을 참조할 떄 한 번에 읽어 들여야 할 **메모리 공간의 크기**를 결정하기 위해
- 메모리에서 읽어 들인 **2진수를 어떻게 해석**할지 결정하기 위해

## 6.10 동적 타이핑

### 6.10.1 동적 타입 언어와 정적 타입 언어

- 정적 타입 언어는 타입체크를 해서 안맞을 경우 실행을 막음

- 동적 타입의 경우 자유롭게 할당이 가능하다.

- 예제 06-23

  ```javascript
  var foo;console.log(typeof foo); // undefinedfoo = 3;console.log(typeof foo); // numberfoo = 'Hello';console.log(typeof foo); // stringfoo = true;console.log(typeof foo); // booleanfoo = null;console.log(typeof foo); // objectfoo = Symbol(); // 심벌console.log(typeof foo); //  symbolfoo = {}; // 객체console.log(typeof foo); // objectfoo = []; // 배열console.log(typeof foo); // objectfoo = function () {}; // 함수console.log(typeof foo); // object
  ```

- typeof 연산자는 변수에 할당된 값의 데이터 타입을 반환

- 동적 타이핑 : 선언이 아닌 할당에 의해 타입이 결정(타입추론 type inference)되며, 재할당에 의해 변수의 타입은 언제든지 동적으로 변한다.

### 6.10.2 동적 타입 언어와 변수

- 편리하다
- 변수값 추적하기가 어려울 수 있다.
- 유연성이 높지만 신뢰성이 떨어진다.
- 변수 사용은 최소화
- 변수의 스콥을 최대한 좁게
- 전역 변수는 최대한 사용하지 않는다.
- 변수보다는 상수값을 사용해 값의 변경을 억제
- 변수의 목적이나 의미를 파악할 수 있도록 네이밍 한다.
- 가독성이 좋은 코드가 좋은 코드다