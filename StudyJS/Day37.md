#### 순수 html 컴포넌트 import해서 사용하기
+ 순수 `html`로 작업을 하는데 푸터와 헤더를 컴포넌트로 따로 뻬서 작업을 하고 그것을 각각에 `html` 파일에 `import`하는 방식으로 진행했다.
+ 처음에는 `<link rel="import" href="header.html">` 이런 식의 방법으로 `body` 안에 저 코드를 넣어주어서 `import` 해주려고 했는데 기능이 먹히지 않았다.
+ 그 이유는❓❓❓ 
  + 이 기능은 더 이상 지원되지 않는 기능이기 때문이다.(띠로리~)😭
  + 콘솔창에 현재 파일에 import가 지원되는지 여부를 알아보는 코드가 있다. => `'import' in document.createElement('link');` 
  + 이것을 콘솔창에 적으면 `true/false` 값으로 나오는데 `true`면 `import` 기능이 지원되는 것이고 `false`면 지원되지 않는 것이다.
  + 그런데 나는 `false`가 나왔다....ㅠㅠ
  
    ![KakaoTalk_Photo_2022-10-19-16-09-33](https://user-images.githubusercontent.com/86812098/196621202-6bc85f5c-561a-40d0-9530-7b7890cc686c.png)

+ 그래서 `.load()` 함수를 써서 아래와 같은 형식으로 `import` 해주려고 위와 같은 `html` 파일을 로컬환경에서 크롬 브라우져로 실행시켰더니 에러가 났다⁉️ => `$('컴포넌트가 들어갈 부분의 아이디 값').load("컴포넌트 html 파일 경로")`
```node
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,minimum-scale=1,user-scalable=no,viewport-fit=cover">
  <link href="./assets/css/main.css" rel="stylesheet">
  <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
  <script>
    $(document).ready(function(){
      $("#headers").load("components/header.html");
      $("#footers").load("components/footer.html");
    });
  </script>
</head>
<body>
  <div id="headers"></div>
  <div class="main_contain">
    <div class="main_img">
      <img src="./assets/img/main.png" alt="메인 이미지">
    </div>
  </div>
  <div id="footers"></div>
</body>
</html>
```
#### 로컬에서 CORS policy 에러 발생
+ 발생한 에러
```node
Access to script at 'file:///C:/경로/components/header.html' from origin 'null' has been blocked by CORS policy: Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, https.
```
+ 처음엔 이 에러가 왜 나는지 몰랐는데 자세히 보니까 `CORS` 에러였다.
+ 해결 방법🧐
  + 로컬 서버를 만들어서 해당 파일을 서버에 올려주면 된다.
  + 순서📃
    + vscode에서 새로운 터미널을 연다.
    + `npm install http-server -g` : `http-server`를 전역으로 설치
    + `npx http-server`:`http-server`를 실행시켜 해당 폴더를 서버에 올린다.(npx 오타 아님)
    + `http://127.0.0.1:8080` 이 url로 접속하면 에러가 사라진다!!
  + 즉, 서버에 올리면 해결이 된다❗️❗️❗️
+ 그렇다면 왜 이런 문제가 발생하는 것일까⁉️
  + 로컬시스템에서 로컬 파일 리소스를 요청할 때는 origin(출처)이 `null`로 넘어가기 때문에 `CORS`에러가 발생한다.

#### SOP (Same Origin Policy - 동일 출처 정책)
+ `SOP`는 '동일 출처 정책' 이다. 어떤 출처(origin)에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 브라우저의 보안 방식이다.
+ 이 때 다른 출처와 같은 출처를 구분하는 기준은 URI의 '프로토콜 호스트 포트 가 같은가'이다.
```node
scheme(protocol)	host	(port)	resource
    프로토콜        호스트    포트
http://	www.example.com	(:80)	/folder/file.html
```
+ 포트까지의 부분이 같다면 같은 출처,다르면 다른 출처로 간주
+ 그러나 이러한 정책이 모든 방식의 요청에 적용 되는 것은 아니다⁉️
+ 예를 들어, `<img>` 태그로 다른 도메인의 이미지 파일을 가져오거나 `<link>` 태그로 다른 도메인의 CSS를 가져오거나 `<script>` 태그로 다른 도메인의 `javascript`를 가져오는 것
그 외에도 `<video>, <audio>, <object>, <embed>, <applet>`태그에는 동일 출처 정책이 적용되지 않는다.
+ `SOP`는 `script`에서 `XMLHttpRequest`나 `Fetch API`를 사용해 다른 출처에 리소스를 요청할 때 적용된다.
SOP는 script에서 XMLHttpRequest나 Fetch API를 사용해 다른 출처에 리소스를 요청할 때 적용됩니다.
+ 결국 `CORS` 에러로 불리는 에러가 발생하는 이유는 이 `SOP`가 적용되는 방식으로 다른 출처의 자원에 접근하려 했기 때문이었고 `CORS`는 이런 경우 `cross-origin HTTP` 요청을 실행하여 액세스 권한을 부여하도록 하는 매커니즘을 가르키는 말이다.
+ 예를 들어, `<img>` 태그로 다른 도메인의 이미지 파일을 가져오거나 `<link>` 태그로 다른 도메인의 `CSS`를 가져오거나 `<script>` 태그로 다른 도메인의 `javascript`를 가져오는 것 그 외에도 <video> <audio> <object> <embed> <applet> 태그
에는 동일 출처 정책이 적용되지 않는다.
+ 즉, `SOP`는 `script`에서 `XMLHttpRequest`나 `Fetch API`를 사용해 다른 출처에 리소스를 요청할 때 적용.





