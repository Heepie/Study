# Node.js 기본 문법
Node.js는 자바스크립트 기반 서버 프레임워크이다. </br>

자바스크립트 서버 표준: CommonJS </br>
자바스크립트 클라이언트 표준: ECMAScript

## 기본 문법
- 변수 설정
  ```javascript
  var a = 11;
  var b = "hello";

  console.log(a);
  console.log(b);
  ```

- 반복문
  ```javascript
  for (var i=0; i<10; i=i+1) {
    console.log(i);
  }
  ```

- 조건문</br>
  자바와 달리 '===' 비교 연산자가 있다. '==='는 값과 더불어 타입까지 검사한다.
  ```javascript
  if (a > 10)
    console.log("a가 10보다 큽니다.");
  else if (a < 10)
    console.log("a가 10보다 작습니다.");
  else
    console.log("a가 10입니다.");
  ```

- 함수 만들기
  - 파라미터에 타입이 없다.
  - 문장 내의 return 여부에 따라 리턴값 결정, 자바처럼 반환자를 정해 놓지 않는다.

  1-1. 함수를 만드는 방법
  ```javascript
  function sum1(param1, param2) {
    console.log(param1 + param2);
  }
  ```
  1-2. 함수를 만드는 방법
  ```javascript
  function sum2(param1, param2) {
    return param1 + param2;
  }
  ```

  2-1. 함수를 만드는 방법
  ```javascript
  var sum = function(param1, param2) {
    return param1 + param2;
  };

  sum1(1,2);
  console.log(sum2(1,2));
  ```

- 클래스 만들기
  - 함수와 클래스는 동일한 문법을 사용. 즉, 함수와 클래스를 구분하는 문법은 없다.
  - 개발자 간 구분을 위해 앞 글자가 대문자면 클래스, 아니면 함수로 사용한다.

  ```javascript
  function Num(param1, param2) {
    // private 선언된 변수 : 외부에서 접근 안됨
    var a=0;  

    // public 선언된 변수 : 외부에서 접근 가능
    this.b = 10;  

    // pirvate 함수
    function a() {

    }

    // public 함수
    this.c = function(param1, param2) {

    }
  }

  // 클래스의 사용
  var num = new Num("hello",2);

  num.b = 500;
  num.c("a", 452);
  ```
