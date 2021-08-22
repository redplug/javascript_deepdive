# 10장 객체 리터럴

## 10.1 객체란? 
- 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 객체
- 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다.
- 함수도 객체가 될 수 있다.

## 10.2 객체 리터럴에 의한 객체 생성
- 자바스크립트의 객체 생성 방법

  - 객체 리터럴
  - Object 생성자 함수
  - 생성자 함수
  - Object.create 메서드
  - 클래스(ES6)

- 객체 리터럴은 중괄호({....}) 내에 0개 이상의 프로퍼티를 정의

  ```javascript
  var person = {
    name: 'Lee',
    sayHello: function () {
      console.log(`Hello! My name is ${this.name}.`);
    }
  };
  
  console.log(typeof person); // object
  console.log(person); // {name: "Lee", sayHello: ƒ}
  ```

  ```javascript
  var empty = {}; // 빈 객체
  console.log(typeof empty); // object
  ```

  

- 객체 리터럴의 닫는 중괄호 뒤에는 세미콜론을 붙인다.

## 10.3 프로퍼티
- 객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.

  ```javascript
  var person = {
    // 프로퍼티 키는 name, 프로퍼티 값은 'Lee'
    name: 'Lee',
    // 프로퍼티 키는 age, 프로퍼티 값은 20
    age: 20
  };
  ```

- 프로퍼티의 나열은 쉼표로 구분, 마지막 프로퍼티에는 사용하지 않으나 사용해도 무방

  - 프로퍼티 키 : 빈 문자열을 포함하는 모든 문자열 또는 심벌 값, 식별자 역할을 한다.

    - 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용

      ```javascript
      var person = {
        firstName: 'Ung-mo', // 식별자 네이밍 규칙을 준수하는 프로퍼티 키
        'last-name': 'Lee'   // 식별자 네이밍 규칙을 준수하지 않는 프로퍼티 키
      };
      
      console.log(person); // {firstName: "Ung-mo", last-name: "Lee"}
      ```

  - 프로퍼티 값 : 자바스크립트에서 사용할 수 있는 모든 값

- 문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다.

  ```javascript
  var obj = {};
  var key = 'hello';
  
  // ES5: 프로퍼티 키 동적 생성
  obj[key] = 'world';
  // ES6: 계산된 프로퍼티 이름
  // var obj = { [key]: 'world' };
  
  console.log(obj); // {hello: "world"}
  ```

## 10.4 메서드
- 프로퍼티 값이 함수 일 경우 일반 함수와 구분하기 위해 메서드(method)라고 부른다.

  ```javascript
  var circle = {
    radius: 5, // ← 프로퍼티
  
    // 원의 지름
    getDiameter: function () { // ← 메서드
      return 2 * this.radius; // this는 circle을 가리킨다.
    }
  };
  
  console.log(circle.getDiameter()); // 10
  ```

## 10.5 프로퍼티 접근
- 프로퍼티 접근 방법

  - 마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기볍(dot notation)
  - 대괄호 프로퍼티 접근 연산자([ ... ])를 사용하는 대괄호 표기법(bracket notation)

  ```javascript
  var person = {
    name: 'Lee'
  };
  
  // 마침표 표기법에 의한 프로퍼티 접근
  console.log(person.name); // Lee
  
  // 대괄호 표기법에 의한 프로퍼티 접근
  console.log(person['name']); // Lee
  ```

- 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 바드시 따옴표로 감싼 문자열이어야 한다.

- 객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다.

## 10.6 프로퍼티 값 갱신
- 이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

  ```javascript
  var person = {
    name: 'Lee'
  };
  
  // person 객체에 name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신된다.
  person.name = 'Kim';
  
  console.log(person);  // {name: "Kim"}
  ```

  

## 10.7 프로퍼티 동적 생성
- 존재 하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

  ```javascript
  var person = {
    name: 'Lee'
  };
  
  // person 객체에는 age 프로퍼티가 존재하지 않는다.
  // 따라서 person 객체에 age 프로퍼티가 동적으로 생성되고 값이 할당된다.
  person.age = 20;
  
  console.log(person); // {name: "Lee", age: 20}
  ```

  

## 10.8 프로퍼티 삭제
- delete 연산자는 객체의 프로퍼티를 삭제한다.

  ```javascript
  var person = {
    name: 'Lee'
  };
  
  // 프로퍼티 동적 생성
  person.age = 20;
  
  // person 객체에 age 프로퍼티가 존재한다.
  // 따라서 delete 연산자로 age 프로퍼티를 삭제할 수 있다.
  delete person.age;
  
  // person 객체에 address 프로퍼티가 존재하지 않는다.
  // 따라서 delete 연산자로 address 프로퍼티를 삭제할 수 없다. 이때 에러가 발생하지 않는다.
  delete person.address;
  
  console.log(person); // {name: "Lee"}
  ```

  

## 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

- ES6에 간편하고 표현력 있는 객체 리터럴의 확장 기능을 제공

### 10.9.1 프로퍼티 축약 표현

- 프로퍼티 값을 변수로 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생력할 수 있다

  ```javascript
  // ES5
  var x = 1, y = 2;
  
  var obj = {
    x: x,
    y: y
  };
  
  console.log(obj); // {x: 1, y: 2}
  
  // ES6
  let x = 1, y = 2;
  
  // 프로퍼티 축약 표현
  const obj = { x, y };
  
  console.log(obj); // {x: 1, y: 2}
  ```

  

### 10.9.2 계산된 프로퍼티 이름

- 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

  ```javascript
  // ES5
  var prefix = 'prop';
  var i = 0;
  
  var obj = {};
  
  // 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
  obj[prefix + '-' + ++i] = i;
  obj[prefix + '-' + ++i] = i;
  obj[prefix + '-' + ++i] = i;
  
  console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
  
  // ES6
  const prefix = 'prop';
  let i = 0;
  
  // 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키 동적 생성
  const obj = {
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i
  };
  
  console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
  ```

  

### 10.9.3 메서드 축약 표현

- 메서드 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.

  ```javascript
  // ES5
  var obj = {
    name: 'Lee',
    sayHi: function() {
      console.log('Hi! ' + this.name);
    }
  };
  
  obj.sayHi(); // Hi! Lee
  
  
  // ES6
  const obj = {
    name: 'Lee',
    // 메서드 축약 표현
    sayHi() {
      console.log('Hi! ' + this.name);
    }
  };
  
  obj.sayHi(); // Hi! Lee
  ```

  

## 
