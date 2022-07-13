#### 문제 발생상황💥
+ 아이디 찾기를 했을 때 인증코드가 메일로 온다. 그것을 복사해서 코드 적는 곳에 붙여넣기를 할 경우 공백이 같이 따라 들어오는 현상이 발생했다.😅
+ 해결방법
  + `trim()` 함수 사용하기❗❗❗

#### trim() 함수란❓❓
+ 문자열을 입력받거나 문자열을 합칠경우 가끔 쓸데없는 공백이 따라 들어오곤 한다
+ 그럴 때 이 함수를 사용하면 따라들어오는 공백을 자동으로 없애주는 기능을 한다.
+ 사용법
  + 문자열이나 사용하는 곳에 `.trim()`이라고 써주면 된다.
+ 예시
  ```node
  <ion-col>
    <input class="input-email-auth" :placeholder="$t('enterAuthenticationCode')" v-model.trim="emailAuthParam.code">
  </ion-col>
  ```
  + 위 코드는 메일로 받은 인증코드를 작성하는 곳이다.
  + `v-model="emailAuthParam.code"` 이렇게 v-model로 코드를 보내고 있기 때문에 여기에 `.trim()`을 추가해주면 공백이 제거되어 들어온다.  
    => `v-model.trim="emailAuthParam.code"`
                        
