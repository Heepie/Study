# Nodejs 기본 서버 실습
Node.js는 javascript 기반의 서버 프레임워크이므로 클라이언트 단 언어인 javascript로 서버 구현이 가능하다.

## 실습
```javascript
// 1. 서버 모듈(라이브러리)를 import
var http = require("http");

// 2. 서버 모듈을 사용해서 서버를 정의
// 함수형 언어이므로 callback을 할 때 자바처럼 객체를 넘기는 것이 아니라 함수를 넘긴다.
// 그리고 함수 이름은 필요 없다 (코드만 실행하면 되므로)

// request는 사용자의 요청, response는 응답
var server = http.createServer( function(request, response) {
  // 사용자 요청에 대하여 어떻게 응답할지를 정의
  response.write("Hello Heepie!");

  // 응답 종료
  response.end();
});

// 3. 서버 실행
// 소켓의 accept과 비슷한 역할
// 인자로 포트와 수행 함수 설정
server.listen(8091, function() {
  console.log("server is running ... ");
});
```

## 스크린 샷
![screenshot](http://cfile5.uf.tistory.com/image/99EC8A3359EDE327099023)
