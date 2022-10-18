#### $(document).ready(function(){})란❓❓
+ jQuery를 사용한 모든 웹페이지는 다음 코드로 시작한다.
```node
<script>
  $(document).ready(function(){

  });
</script>
```
+ `$(document).ready()`는 문서가 준비되면 매개변수로 넣은 콜백 함수를 실행하라는 의미이다.
+ 즉, 문서가 준비되면 그 안에 있는 함수들이 바로 동작한다.
+ 예제
```node
<script>
  $(document).ready(function(){
    alert("First READY");
  });

  $(document).ready(function(){
    alert("Second READY");
  });

  $(document).ready(function(){
    alert("Third READY");
  });
</script>
```
+ 이렇게 하면 3번의 알림창이 뜬다.
+ 간단한 사용형태👍
```node
<script>
  $(function(){

  });
</script>
```
