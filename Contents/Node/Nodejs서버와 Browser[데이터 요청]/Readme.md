# Nodejs서버와 Browser[데이터 요청]
Client가 Server에 데이터를 요청하고 응답하는 데이터 흐름을 확인 할 예정이다.
![concept](http://cfile6.uf.tistory.com/image/99D9523359F1C35D3D0AB0)
1) Client는 Server에게 view.html 데이터를 요청</br>
2) Server는 요청한 데이터를 가공해 해당 데이터를 Client에게 전달</br>
하는 흐름이다.

## 실습
1. 코드
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
                  } else {
                      // 파일이 존재하면 해당 파일로 응답
                      response.writeHead(200,{'Content-Type':'text/html'});
                      response.end(data);
                  }
              });
          }
      }
});
// 3. 클라이언트 대기
server.listen(9000, function() {
  console.log("Server listening ...");
});
```
2. 미리 view.html 생성
![view](http://cfile26.uf.tistory.com/image/99C3F73359F0909E1B3174)

## 스크린 샷
![screenshot](http://cfile4.uf.tistory.com/image/9920133359F0914A22DA10)
