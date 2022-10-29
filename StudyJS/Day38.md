#### jQuery로 메뉴 버튼 선택 시 css 변경되게 만들기
+ 메뉴는 총 4개이며 각각의 버튼 클릭 시 해당 부분 css가 변경되고 `display:none;` 처리되었던 요소가 `display:block;`으로 바뀌게 된다.
+ `$('button').click(function(){`: button태그 클릭 시 아래 코드 실행됨
+ `$('.active').siblings('.dot').css('display','none');`
  + `.active` 클래스의 형제위치에 있는 `.dot` 클래스를 `display:none;` 시켜준다.
  + 이렇게 해줘야 다른 버튼을 선택할 때 기존에 `display:block;`되었던 요소가 안 보이게 된다🔸
+ `$('button').removeClass("active");`
  + 버튼 태그에 추가해주었던 `.active` 클래스를 제거해준다.
  + 이렇게 해줘야 다른 버튼을 선택할 때 기존에 적용된 `.active` 클래스가 제거된다.
+ `$(this).addClass("active");`
  + button 태그에 `.active` 클래스를 추가시켜준다.
  + 여기서 포인트‼️ `$(this)`사용
    + jQuery에서의 `$(this)`는 자기자신을 선택하는경우에 많이 사용한다.
    + 이벤트를 실행시킬때 DOM 조작을 하면서 어떠한 선택자에 이벤트를 부여하고 사용자가 이벤트를 실행시키면 이벤트가 적용된 자기자신이 `$(this)` 가 된다.
    + 즉, 여기에서 `$(this)`는 클릭하는 버튼 태그를 의미하는 것이다.  => `$(this) = $('button')`
+ `if($('button').hasClass("active") === true){` 
    + `hasClass()`: 이 함수는 해당 클래스가 있는지 여부를 나타낸다.`(true/false)`
    + : button 태그에 active 클래스가 있으면 즉, `true` 이면
+ `$('.active').siblings('.dot').css('display','block');`
  + `.siblings()`:선택한 요소의 형제 요소 중에서 지정한 선택자에 해당하는 요소를 모두 선택
  + 형제 요소 중 `.dot`이라는 클래스를 `display: block` 시켜주라는 의미이다.
```node
<script>
  $(document).ready(function(){
    $('button').click(function(){
      $('.active').siblings('.dot').css('display','none');
      $('button').removeClass("active");
      $(this).addClass("active");
      if($('button').hasClass("active") === true){
        $('.active').siblings('.dot').css('display','block');
      }
    });
  });
</script>

<body>
  <div class="header_contain">
    <div class="menu_sec">
      <div class="btn">
        <button type="button" class="menu_btn button"><a href="../callingRequestList.html">법인카드 소명등록</a></button>
        <div class="dot" style="display: none;"></div>
      </div>
      <div class="btn">
        <button type="button" class="menu_btn button"><a href="../openTestResult.html">감사결과공개</a></button>
        <div class="dot" style="display: none;"></div>
      </div>
      <div class="btn">
        <button type="button" class="menu_btn button"><a href="../ethicsNotice.html">청념윤리유의사항</a></button>
        <div class="dot" style="display: none;"></div>
      </div>
      <div class="btn">
        <button type="button" class="menu_btn button"><a href="../notice.html">공지사항</a></button>
        <div class="dot" style="display: none;"></div>
      </div>
    </div>
  </div>
</body>
```

#### 위와 같은 방법으로 코드를 짤 경우 문제 발생🛑
+ 메뉴를 클릭 시 변경되는 css가 잠깐 보였다가 다시 원래 상태로 돌아가게 된다.
+ 왜 이러한 현상이 일어나는 걸까❓❓❓
  + 그 이유는 페이지가 이동되면서 변경된 값이 초기화 되기 때문이다.
+ 해결방법✅
  + 버튼을 클릭했을 때 변경되게 하지 말고 해당 페이지에 진입했을 때 변경되게 하면 된다.
  + 즉, 해당 페이지의 `url`을 가져와서 `if문`과 `if~else`문을 사용하여 해당 `url`이 탈때 `css`가 변경되게 해주면된다. 
  + 해당 url을 가져오는 방법🧐
    + `window.location.href.includes()` 사용!! 
    + `window.location.href`는 페이지를 이동할 때 해주는 코드이다. 여기에 `includes()` 라는 특정 문자열을 포함하는지 여부를 확인해주는 함수를 사용한다.
    ```node
    <script>
    $(document).ready(function(){
        if(window.location.href.includes('callingRequestList')){
          $('#btn1 a').css('fontFamily', 'Pretendard-Bold');
          $('#dot1').css('display','block');
        }else if(window.location.href.includes('openTestResult')){
          $('#btn2 a').css('fontFamily', 'Pretendard-Bold');
          $('#dot2').css('display','block');
        }else if(window.location.href.includes('ethicsNotice')){
          $('#btn3 a').css('fontFamily', 'Pretendard-Bold');
          $('#dot3').css('display','block');
        }else if(window.location.href.includes('notice')){
          $('#btn4 a').css('fontFamily', 'Pretendard-Bold');
          $('#dot4').css('display','block');
        }
      });
    </script>
    ```
    + 이렇게 하면 해당 문자열이 포한됨 url을 탈 때 지정해준 css가 변경된다.
