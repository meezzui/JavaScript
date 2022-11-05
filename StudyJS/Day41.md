#### jQuery를 이용하여 마우스 올리면 이미지, 글씨 색상 변하게 하기(hover 기능)
+ 메뉴에 마우스를 올리면 해당 메뉴의 이미지가 on 이미지로 바뀌었다가 떠나면 다시 원래 이미지로 돌아온다.
+ 그럼 어떻게 하면 될까❓❓
  + 먼저 html 코드를 봐보자😉
  ```node
  <div class="menu">
    <div class="menu_img">
      <img class="menu_on" src="./assets/img/monitoring-off.png" alt="법인카드 상시모니터링">
    </div>
    <p class="menu_name">법인카드 상시모니터링</p>
  </div>
  ```
  + 위에 코드가 메뉴 하나의 html 코드이다. `.menu` 클래스를 메뉴 하나의 틀로 보고 그 안에 이미지와 메뉴이름이 들어간다.
  + 그러면 저 `.menu`인 메뉴 하나의 틀에 마우스를 올리면 이미지가 on 이미지로 변경되고 글씨의 색깔이 파란색으로 바껴야 한다.
  ```node
   <script>
    $(document).ready(function(){
      $(".menu").on('mouseenter', function() {
        $(this).find('.menu_on').attr("src", $(this).find('.menu_on').attr("src").replace("-off","-on"));
        $(this).children('.menu_name').css('color','#003288');
      }).on('mouseleave', function() {
          $(this).find('.menu_on').attr("src", $(this).find('.menu_on').attr("src").replace("-on", "-off"));
          $(this).children('.menu_name').css('color','#808080')
      });
    });
  </script>
  ```
  + `$(".menu").on('mouseenter', function() {`: `.menu`클래스 div에 마우스를 올리면 작동
  + `$(this).find('.menu_on').attr("src", $(this).find('.menu_on').attr("src").replace("-off","-on"));`
    + `$(this)`: `.menu`를 가리킴(이렇게 해줘야 선택한 해당 메뉴에만 적용됨)
    + `find('.menu_on')`: `.menu` `div`의 하위 요소 중에 `.menu_on`라는 클래스를 찾음
    + `attr('')`: 이 함수는 속성값을 가져오는 함수이다. 즉, `attr("src")`라는 것은 `.menu_on`의 `src` 속성을 가져온다는 의미이다.
    + `$(this).find('.menu_on').attr("src").replace("-off","-on")`: `.menu`클래스 하위요소 중 `menu_on`라는 클래스를 찾아서 그것의 `src`속성을 바꾸는데 `-off`라고 되어있는 부분을 `-on`으로 바꾸라는 의미이다.
    + `attr('','')`: 왼쪽의 속성값을 오른쪽의 속성값으로 바꾸겠다는 의미이다.
      + `$(this).find('.menu_on').attr("src", $(this).find('.menu_on').attr("src").replace("-off","-on"));` : src 속성을 바꾸는데 `-on`으로 바뀐걸로 바꾸겠다는 것이다.
  + `$(this).children('.menu_name').css('color','#003288');` : `.menu` 클래스의 바로 아래 요소인 `.menu_name`클래스의 글씨 색깔을 `#003288`로 바꾸겠다.
  + `}).on('mouseleave', function() {` : 마우스가 `.menu` 요소를 떠날 경우 작동
  + `$(this).find('.menu_on').attr("src", $(this).find('.menu_on').attr("src").replace("-on", "-off"));`: 다시 이미지를 끝에 글자가 `-off`인 애로 바꿔준다.
  + `$(this).children('.menu_name').css('color','#808080')` : `.menu` 클래스의 바로 아래 요소인 `.menu_name`클래스의 글씨 색깔을 `#808080`로 바꾼다.

+ 여기서 포인트✅
  + 이미지들의 이름을 맞춰줘야 한다는 것이다🔑
  + 예) `off`이미지 이름: `monitoring-off.png"` ,  `on`이미지 이름: `monitoring-on.png"`
  + 이렇게 하고 `-off`, `-on`만 바뀌게 적용하면 된다😎

