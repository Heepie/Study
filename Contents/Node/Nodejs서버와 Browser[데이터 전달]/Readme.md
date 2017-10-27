# Nodejs서버와 Browser[데이터 전달]
Node.js를 공부하며 클라이언트 요청 데이터를 서버에서 가공하는 단계가 복잡했고 햇갈리는 부분이어서 정리했다.

## Step1. 클라이언 -> 서버 데이터 요청
1. 코드
```javascript
// 1. 라이브러리 가져오기
var http = require("http");
// 2. 서버 생성
var server = http.createServer(function(request, response) {
  // 주소를 제외한 url 추출
  console.log(request.url);
  var url = request.url;

  response.end("Connected");
});
// 3. 클라이언트 대기
server.listen(9000, function() {
  console.log("Server listening ...");
});
```

2. url 구성
![url](http://cfile27.uf.tistory.com/image/998EBA3359F08792067CE5)

## Step2. Url -> 구조화(Structed Url)
1. 코드
```javascript
// 1. 라이브러리 가져오기
var http = require("http");
var u = require("url");
// 2. 서버 생성
var server = http.createServer(function(request, response) {
  // 주소를 제외한 url 추출
  // console.log(request.url);
  var url = request.url;
  var strucedUrl = u.parse(url);
  console.log(strucedUrl);        
  response.end("Connected");
});
// 3. 클라이언트 대기
server.listen(9000, function() {
  console.log("Server listening ...");
});
```

2. strucedUrl의 구성
![structedUrl](http://cfile21.uf.tistory.com/image/993E6F3359F0804E0944F5)

## Step3. Query -> 구조화(Structed Query)
1. 코드
```javascript
// 1. 라이브러리 가져오기
var http = require("http");
var u = require("url");
var qs = require("querystring");
// 2. 서버 생성
var server = http.createServer(function(request, response) {
  // 주소를 제외한 url 추출
  // console.log(request.url);
  var url = request.url;
  var strucedUrl = u.parse(url);
  // console.log(strucedUrl);
  var strucedQuery = qs.parse(strucedUrl.query);
  console.log(strucedQuery);
  response.end("Connected");
});
// 3. 클라이언트 대기
server.listen(9000, function() {
  console.log("Server listening ...");
});
```

2. strucedUrl의 구성
![structedQuery](http://cfile23.uf.tistory.com/image/99BF0B3359F087A4174326)
