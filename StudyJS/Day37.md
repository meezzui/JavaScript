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
  + 







