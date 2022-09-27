#### '$ is not defined' 에러 해결
+ `javasctipt`를 사용하기 위해 `.html` 파일에 `import`를 해줬는데 계속 아래와 같은 에러가 떴다.
<img width="395" alt="image" src="https://user-images.githubusercontent.com/86812098/192543362-cf9ca7c5-e3ed-4c7a-be1f-55fdf2ab1822.png">

+ 처음엔 자바스크립트 버전이 안 맞아서 그런 줄 알고 버전을 변경해 봤는데도 계속 똑같은 오류가 떴었다.
+ 원인이 뭘까⁉️
  + 위와 같은 오류가 뜨는 이유는 `import`해주는 자바스트립트의 위치 때문이였다.
  + `jQuery`와 `javaScript`를 동시에 사용하는 경우, `jQuery`를 먼저 `import` 해야 한다🤨
+ 해결✅
  + `<script src="https://code.jquery.com/jquery-2.2.4.js"></script>` `jQuery` 스크립트를 `.js` 스크립트들 보다 먼저 `import` 해주었다. 
