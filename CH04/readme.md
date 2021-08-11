# 04장 변수

## 4.1 변수란 무엇인가? 왜 필요한가?
- 컴퓨터의 모든 데이터는 메모리에 저장되며 2진수로 저장된다.
- 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름, 값의 위치를 가리키는 상직적인 의미
- 변수 이름(변수명) : 메모리 공간에 저장된 값을 식별할 수 있는 고유 이름
- 변수 값 : 변수에 저장된 값.
- 할당(assignment) : 변수에 값을 저장
- 참조(reference) : 변수에 저장된 값을 읽어 드림
- 변수명은 잘지어야 한다.

## 4.2 식별자
- 변수의 이름을 식별자라고도 함.
- 어떤 값을 구별해서 식별할 수 있는 고유한 이름
- 값이 저장되어 있는 메모리 주소와 매핑 관계
- 식별자는 값이 아니라 메모리 주소를 기억함.
- 변수 뿐만 아니라 함수 클래스도 포함됨.
- 선언(declaration)에 의해서 식별자의 존재를 알림

## 4.3 변수 선언
- 변수를 생성하는 행위, 값 저장을 위해 메모리 공간을 확보(allocate) 하고, 메모리 공간의 주소를 연결(name binding)해서 값을 저장할 수 있게 준비
- 변수 사용을 위해서는 선언이 필요함.
- 변수 선언은 var, let, const를 사용, let, const는 ES6부터 사용 가능.
- let, const는 var의 단점을 보완하기 위해 도입됨.
- var 키워드는 뒤에오는 변수 이름으로 새로운 변순을 선언을 지시
- 예제 04-04
    ```javascript
    var scope; // 변수 선언(변수 선언문)
    ```
- 변수 선언 후 확보된 메모리에는 undefined라는 값이 암죽적으로 할당되어 초기화 된다.
- 변수 선언의 단계
  - 선언 단계 : 변수 이름을 등록해 자바스크립트 엔진에 변수의 존재를 알림
  - 초기화 단계 : 값을 저장히기 위한 메모리 공간을 확보 undefined를 할당해 초기화
- 변수 이름은 실행 컨텍스트에 등록
- 실행 컨텍스트(execution context) : 코드의 실행결과를 실제로 관리하는 영역
  - 변수 이름과 값은 실행 컨텍스트 내 Key / Value 형식인 객체로 등록되어 관리
  
## 4.4 변수 선언의 실행 시점과 변수 호이스팅
- 예제 04-05
    ```javascript
    console.log(score); // undefined

    var score; // 변수 선언문
    ```
- score 변수 선언보다 console.log가 앞에 있더라도 참조 에러가 아닌 undefined가 떨어진다.
- **변수 선언**이 코드가 한 줄씩 순차적으로 실행되는 시점, 즉 **런타임(runtime)이 아니라 그 이전 단계에 먼저 실행**되기 떄문이다.
- 자바스크립트 엔진은 한줄씩 실행하기에 앞서 소스코드의 평가 과정을 거치면서 소스코드 실행할 준비를 한다.
- 이 시점에 변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문 등)을 소스코드에서 찾아내서 먼저 실행한다.
- 평가 과정이 끝나면 선언문을 제외하고 소스코드를 한줄씩 실행한다.
- 변수 선언은 소스코드 어디에 있어도 상관이 없다.
- **변수 호이스팅(variable hoisting) : 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트의 고유의 특징**

## 4.5 값의 할당
- 변수에 값을 할당할 떄는 '='를 사용한다.
- 예제 04-06
    ```javascript
    var scoure; // 변수 선언
    score = 80; // 값으 ㅣ할당
    ```
- 변수를 선언하면서 값을 할당할 수도 있음.
- 예제 04-07
    ```javascript
    var score = 80; // 변수 선언과 값의 할당
    ```
- 변수 선언과 할당의 실행시점이 다르다.
- 변수의 선언은 런타임 이전, 할당은 런타임에 실행
- 예제 04-08
    ```javascript
    console.log(score); // undefined

    var score; // 1. 변수 선언
    score = 80; // 2. 값의 할당

    console.log(score); // 80
    ```
- 예제 04-09
    ```javascript
    console.log(score); // undefined

    var score = 80; // 변수 선언과 값의 할당

    console.log(score); // 80
    ```
- 예제 04-10
    ```javascript
    console.log(score); // undefined

    score = 80; // 값의 할당
    var score; // 변수 선언

    console.log(score); // 80
    ```

## 4.6 값의 재할당
- 재할당 : 이미 값이 할당되어 있는 변수에 새로운 값을 또다시 할당
- 예제 04-11
    ```javascript
    var score = 80; // 변수 선언과 값의 할당
    score = 90; // 값의 재할당
    ```
- 상수(constant) : 변수에 저장된 값을 변경 불가, 재할당이 불가함 -> const
- 값을 재할당 할 경우 메모리 공간을 확보해서 값을 재할당 한다(같은 메모리주소에 넣지 않는다.)
- 가비지 콜렉터 : 애플리케이션이 할당한 메모리 공간을 주기적으로 검사하여 더 이상 사용하지 않는 메모리를 해제하는 기능, 즉 어떤 식별자도 참조하지 않는 메모리 공간을 삭제하는 기능, 자바스크립트는 가비지 콜렉터를 내장하고 있는 매니지드 언어로 메모리 누수(memory leak)를 방지한다.
- 매니지드 언어(managed language) vs 언 매니지드 언어(unmanaged language)
  - C와 같은 언매니지드 언어는 개발자가 명시적으로 메모리를 할당하고 해제 하기 위한 malloc(), free()같은 메모리 제어 기능을 제공
  - 자바스크립트와 같은 매니지드 언어는 메모리 할당 및 헤제를 언어 차원에서 담당하고 있어서 개발자가 직접적인 메모리 제어를 허용하지 않음.

## 4.7 식별자 네이밍 규칙
- 식별자는 다음과 같은 네이밍 규칙을 준수해야 한다.
  - 식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(_), 달러 기호($)를 포함할 수 있다.
  - 식별자는 특수문자를 제외한 문자, 언더스코어(_), 달러 기호($)로 시작해야 한다. 숫자로 시작하는 것은 허용하지 않는다.
  - 예약어는 식별자로 사용할 수 없다.(await, break, case ....)
- 쉼표로 여러개의 변수를 선언이 가능하나 가독성이 좋지 않음.
- 예제 04-12
    ```javascript
    var person, $elem, _name, first_name, val1;
    ```
- ES5부터 유니코드 문자를 허용, 비권장
- 예제 04-13
    ```javascript
    var 이름;
    ```
- 다음 식별자는 명명 규칙에 위배되므로 변수 이름으로 사용이 불가하다
- 예제 04-14
    ```javascript
    var first-name; // SyntaxError : Unexpected token -
    var 1st;        // SyntaxError : Invalid or unexpected token
    var this;       // SyntaxError : Unexpected token this
    ```
- 자바스크립트는 대소문자를 구별하므로 다음 변수는 각각 별개의 변수다.
- 예제 04-15
    ```javascript
    var firstname;
    var firatName;
    var FIRSTNAME;
    ```
- 변수 이름은 변수의 목적 존재를 쉽게 이해할 수 있도록 의미를 명확히 표현해야 한다.
- 예제 04-16
    ```javascript
    var x = 3;       // NG. x 변수가 의미하는 바를 알 수 없다.
    var score = 100; // OK. score 변수는 점수를 의미한ㄷ.
    ```
- 변수 선언에 별도의 주석이 필요하다면 변수의 존재 목적을 명확히 드러내지 못하는 것이다.
- 예제 04-17
    ```javascript
    // 경과 시간, 단위는 날짜다.
    var d; // NG

    var elapsedTimeInDays; // OK
- 네이밍 컨벤션(naming convention) 하나 이상의 영어 단어로 구성된 식별자를 만들떄 가독성이 좋게 만드는 명명 규칙, 하기 4가지가 많이 사용됨.
    ```
- 예제 04-18
    ```javascript
    // 카멜 케이스(camelCase)
    var firstName;

    // 스네이크 케이스(snake_case)
    var first_name;

    // 파스칼 케이스(PascalCase)
    var FirstName;

    // 헝가리언 케이스(typeHungarianCase)
    var strFirstName;                               // type + identifier
    var $elem = document.getElementById('myId');    // DOM 노드
    var observable$ = fromEvent(document, 'click'); // RxJS 옵저버블
    ```
- 자바스크립트에서는 일반적으로 하기와 같이 사용하고 있으며 가독성을 높이기 위해서는 하기와 같이 사용하는 것이 좋다.
  - 카멜 케이스 : 변수나 함수
  - 파스칼 케이스 : 생성자 함수, 클래스의 이름 
