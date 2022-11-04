#### 한 버튼 눌렀을 때 조건에 따라 다른 팝업 나오게 하기
+ '제출' 버튼을 눌렀을 때
  + 조건1 > `textarea`가 빈 값일 경우 `내용이 입력되지 않았습니다. 계속 진행 하시겠습니까?` 팝업이 뜸
  + 조건2 > `textarea`에 값이 있을 경우 `소명 제출 시 수정이 불가합니다. 계속 진행 하시겠습니까?` 팝업이 뜸

+ 빈 값 확인 코드
  + `.trim()` 함수 사용 => 문자열의 공백을 없애주는 함수. 특히 문자열을 입력받거나 문자열을 합칠경우 가끔 쓸데없는 공백이 따라 들어오곤 하는데 그럴 때 유용하다😎
  + `let text = $('#write_opinion').val().trim();` : 해당 textarea의 값을 가져와서 공백을 제거
```node
<script>
  $(document).ready(function(){
    // 소명제출 팝업 열림
    $('.click_submit').click(function() {
      let text = $('#write_opinion').val().trim();
      if(text == ''){ // textarea 가 빈 값일 경우
        $('#empty_area_popup').show();
        $('body').css('overflow','hidden');
      }else{ // textarea 에 값이 있을 경우
        $('#submit_popup_sec').show();
        $('body').css('overflow','hidden');
      }
    })

    // 소명제출 팝업 닫기
    $('.submit_cancel').click(function() {
      $('#submit_popup_sec').hide();
      $('body').css('overflow-y','scroll');
    })

    // 소명 의견 미작성 팝업 닫기
    $('.stop').click(function() {
      $('#empty_area_popup').hide();
      $('body').css('overflow-y','scroll');
    })
  });
</script>

<!-- 의견 작성 -->
<textarea name="write_opinion" id="write_opinion" placeholder="여기에 소명 의견을 작성해주세요."></textarea>

<!-- 소명 제출 버튼 눌렀을 시 뜨는 팝업 -->
<div id="submit_popup_sec" style="display: none;">
  <div class="dim"></div>
  <div class="modal">
    <div class="inner_modal">
      <div class="popup_comment">
        <p>소명 제출 시 수정이 불가합니다.<br>계속 진행 하시겠습니까?</p>
      </div>
      <div class="popup_btn_box">
        <div class="btn_cancel">
          <button class="submit_cancel">취소</button>
        </div>
        <div class="btn_ok" onclick="location.href='./callingRequestList.html'">
          <button>확인</button>
        </div>
      </div>
    </div>
  </div>
</div>
<!-- 소명 의견 미작성 시 뜨는 팝업 -->
<div id="empty_area_popup" style="display: none;">
  <div class="dim"></div>
  <div class="modal">
    <div class="inner_modal">
      <div class="popup_comment">
        <p>내용이 입력되지 않았습니다.<br> 계속 진행 하시겠습니까?</p>
      </div>
      <div class="popup_btn_box">
        <div class="btn_cancel">
          <button class="stop">취소</button>
        </div>
        <div class="btn_ok" onclick="location.href='./callingRequestList.html'">
          <button>확인</button>
        </div>
      </div>
    </div>
  </div>
</div>
```
