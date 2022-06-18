#### toFixed() 함수란❓❓❓
+ 소수점의 자릿수를 제한할 수 있는 자바스크립트 메서드이다.
+ Number 인스턴스의 소수 부분 자릿수를 전달받은 값으로 고정한 후, 그 값을 문자열로 반환한다.
+ 사용방법
  + `obj.toFixed([소수 부분의 자릿수])`
  ```node
  let obj = 1.23456 

  console.log(obj.toFixed()); // 결과: '1'
  console.log(obj.toFixed(6)); // 결과: '1.234560'
  console.log(obj.toFixed(3)); // 결과: '1.235'
  console.log(obj.toFixed(1)); // 결과: '1.2'
  ```
+ 소수 부분의 자릿수는 소수점 뒤에 나타날 자릿수이다. 0 이상 100 이하의 값을 사용할 수 있다.
+ 자릿수를 지정해주지 않으면 '0'으로 자동 처리된다. 그래서 소수점 아랫수가 보이지 않는다.
+ 메서드를 호출한 숫자의 크기가 1e+21보다 크다면 Number.prototype.toString()을 호출하여 받은 지수 표기법 결과를 대신 반환헌다.✔
+ 주의사항💥
  + 파라 매터가 0과 100 사이의 값이 아니라면 `Uncaught RangeError: toFixed() digits argument must be between 0 and 100`라는 오류가 발생한다.
  ```node
  obj = 12345.67 
  console.log(obj.toFixed(101)); // 결과: 오류발생
  ```
