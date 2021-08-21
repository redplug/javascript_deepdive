# 09장 타입 변환과 단축 평가

## 9.1 타입 변환이란?
- 개발자가 의도적으로 값의 타입을 변환 -> 명시적 타입 변환(explicit coercion), 타입 캐스팅(type casting)

  ```javascript
  var x = 1-;
  
  // 명시적 타입 변환
  // 숫자를 문자열로 타입 캐스팅 한다.
  var str = x.toString();
  console.log(typeof str, str); // string 10
  
  // x 변수의 값이 변경된 것은 아니다.
  console.log(typeof x, x); // number 10
  ```

  

- 개발자의 의도와 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 타입이 자동 변환 -> 암묵적 타입 변환(implicit coercion), 타입 강제 변환(type coercion)

  ```javascript
  var x = 10;
  
  // 암묵적 타입 변환
  // 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
  var str = x + '';
  console.log(typeof str, str); // string 10
  
  // x 변수의 값이 변경된 것은 아니다.
  console.log(typeof x, x); // number 10
  ```

- 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.

- 암묵적 타입변환이 발생하는지 예측 가능해야 한다.

## 9.2 암묵적 타입 변환
### 9.2.1 문자열 타입으로 변환

```javascript
1 + '2' // -> "12"
```

- 피 연산자중 하나가 문자열이므로 문자열 연결 연산자로 동작

- ES6에서 도입된 템플릿 리터럴의 표현식 삽입은 표현식의 평가 결과를 문자열 타입으로 암묵적 타입변환 한다.

  ```javascript
  '1 + 1 = ${1 + 1}' // -> "1 + 1 = 2"
  ```

- 문자열 타입 암묵적 변환 동작

  ![image-20210821183318985](https://raw.githubusercontent.com/redplug/shareimages/master/img/image-20210821183318985.png)

### 9.2.2 숫자 타입으로 변환

```javascript
1 - '1' // -> 0
1 * '10' // -> 10
1 / 'one' // -> NaN
```

- 코드 문맥상 숫자 타입이어야 변환함.
- 단항 연산자는 피연산자가 숫자 타입으 ㅣ값이 아니면 숫자 타입의 값으로 암묵적으로 타입변환 수행

### 9.2.3 불리언 타입으로 변환

- 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입변환 한다
- false로 평가되는 Falsy값
  - false
  - undefined
  - null
  - 0, -0
  - NaN
  - ''(빈문자열)
- Falsy값 외의 모든 값은 true로 평가되는 Truthy값

## 9.3 명시적 타입 변환

### 9.3.1 문자열 타입으로 변환

- 변환 방법
  - String 생성자 함수를 new 연산자 없이 호출하는 방법
  - Object.prototype.toString 메서드를 사용하는 방법
  - 문자열 연결 연산자를 이용하는 방법

### 9.3.2 숫자 타입으로 변환

- 변환 방법
  - Number 생성자 함수를 new 연산자 없이 호출하는 방법
  - parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
  - '+' 단항 산술 연산자를 이용하는 방법
  - '*' 산술 연산자를 이용하는 방법

### 9.3.3 불리언 타입으로 변환

- 변환 방법
  - Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
  - ! 부정 논리 연산자를 두번 사용하는 방법

## 9.4 단축 평가
### 9.4.1 논리 연산자를 사용한 단축 평가

```javascript
'Cat' && 'Dog' // -> "Dog"
```

- 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다, -> 단축 평가

- 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.

  ```javascript
  // 논리합(||) 연산자
  'Cat' || 'Dog' // -> "Cat"
  false || 'Dog' // -> "Dog"
  'Cat' || false // -> "Cat"
  
  // 논리곱(&&) 연산자
  'Cat' && 'Dog' // -> "Dog"
  false && 'Dog' // -> false
  'Cat' && false // -> false
  ```

- 어떤 조건이  Truthy값일 때 무언가를 해야 한다면 논리곱(&&) 연산자 표현식으로 if문을 대체할 수 있다.

- 어떤 조건이 Falsy값일떄 무언가를 해야 한다면 논리합(||) 연산자 표현식으로 if문을 대체할 수 있다. 

### 9.4.2 옵셔널 체이닝 연산자

- ES11에 도입된 옵셔널 체이닝(optional chaining) 연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

### 9.4.3 null 병합 연산자

- ES11에 도입된 null 병합(nullsh coalescing) 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피 연산자를 반환한다.

- null 병합 연산자 ??는 변수에 기본값을 설정할 떄 유용하다

  ```javascript
  // 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고,
  // 그렇지 않으면 좌항의 피연산자를 반환한다.
  var foo = null ?? 'default string'
  console.log(foo) // "default string"
  ```

  

