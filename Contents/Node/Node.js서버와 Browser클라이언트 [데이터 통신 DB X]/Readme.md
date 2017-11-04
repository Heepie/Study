# Node.js서버와 Browser클라이언트 [데이터 통신 DB X]
이번 포스팅에서는 Nodejs 서버와 Browser 클라이언트 간의 통신을 실습할 예정이다. 데이터 요청 방식에 따라</br>
1) GET 방식</br>
2) POST 방식</br>
으로 진행 할 예정이다.</br>

## 흐름
![flow](http://cfile2.uf.tistory.com/image/9966013359F1CCA926D4A0)

## 실습 1
```javascript
// 1. 라이브러리 가져오기
var http = require("http");
var u = require("url");
var qs = require("querystring");

// File Stream: 파일을 열기 위한 라이브러리
var fs = require("fs");

// 2. 서버 생성
var server = http.createServer(function(request, response) {
  // 주소를 제외한 url 추출
  // console.log(request.url);
  var url = request.url;

  var strucedUrl = u.parse(url);

  var path = strucedUrl.pathname;
  var cmds = path.split("/");

  // console.log(cmds[1]);
  // console.log("Create Server OK");

  // RESTFul의 'html' 이라면
  if (cmds[1] == "html") {
    console.log("Html OK");
    if (request.method == "GET") {
      console.log("OK");

      // '/' 문자 제거
      var filePath = path.substring(1);
      console.log(path);

      // 파일을 연다.
      fs.readFile(filePath, 'utf-8',function(error, data){
              if(error){
          // 파일이 없다면 오류 메시지로 응답
                  response.writeHead(404,{'Content-Type':'text/html'});
                  response.end("<h1>404 Page not found!</h1>");
              }else{
          // 파일이 존재하면 해당 파일로 응답
                  response.writeHead(200,{'Content-Type':'text/html'});
                  response.end(data);
              }
          });
    }
  } else if (cmds[1] == "signin") {
    // GET Method 처리
    if (request.method == "GET") {
      // 서버 내에 변수로 rootId와 rootPw 설정
      var rootId = "heepie";
      var rootPw = "123456789";
      var datas = qs.parse(strucedUrl.query);
      var id = datas.id;
      var pw = datas.pw;

      console.log(id + " " + pw);
      // id와 pw 확인
      if (rootId == id && rootPw == pw) {
        response.end("Welcome " + id);
      } else {
        response.end("Check Id or Pw");
      }
    }
  }
});

// 3. 클라이언트 대기
server.listen(9000, function() {
  console.log("Server listening ...");
});
```

```html
<html>
<head>
    <meta charset="utf-8"/>
    <title> Input Get Method </title>
</head>
<body>
  <!-- "/signin"에서 다음 진행 처리, GET 방식 -->
  <form action="/signin" method="GET">
    아이디: <input type="text" name = "id"/></br>
    비밀번호: <input type="text" name = "pw"/></br>
    <input type="submit" value="전송"/>
  </form>
</body>
</html>
```

## 스크린 샷
