#### 만 나이 계산하기
+ `getFullYear()`란❓❓
  + 현지 시간에 따라, 주어진 날짜의 연도에 해당하는 숫자를 반환해준다.
  + `getFullYear()`가 반환하는 값은 절댓값이다.(4자리 숫자를 반환)
  + 사용방법(예시)
  ```node
   // 현재 연도의 네 자릿값을 변수 year에 할당
  const today = new Date();
  const year = today.getFullYear();
  ```
+ `getMonth()`란❓❓
  + Date 객체의 월 값을 현지 시간에 맞춰 반환한다.
  + 주의💥 월은 0부터 시작하므로 +1 해줘야 현재 월을 알 수 있다.
  ```node
  const now = new Date(); // 현재시간
  const mon = (now.getMonth()+1); //월
  ```
  + 참고📢 필요한 경우 `Intl.DateTimeFormat()`와 매개변수를 사용해 해당하는 달의 이름("January" 등)을 가져올 수 있다.
  ```node
  const today = new Date()
  const options = { month: 'long'};
  console.log(new Intl.DateTimeFormat('ko-KR', options).format(today));
  // 12월
  console.log(new Intl.DateTimeFormat('en-US', options).format(today));
  // December
  ```
  
+ `getDate()`란❓❓
  + 현지 시간에 따라, 주어진 날짜의 일에 해당하는 1 이상 31 이하의 정수를 반환
  + 사용방법
  ```node
  const today = new Date();
  const year = today.getDate();
  ```
  
