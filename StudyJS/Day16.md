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
#### 적용해보기
```node
data() {
  return {
    year: [],
    month: [],
    day: [],
    bthdt: {
      year: '',
      month: '',
      day: ''
    },
    age: 0
  }
}
methods:{
  setAge() {
    // 만 나이 계산
    const today = new Date()
    const bthDate = new Date(this.bthdt.year, this.bthdt.month, this.bthdt.day)

    let tempAge = today.getFullYear() - bthDate.getFullYear()
    const month = today.getMonth() - bthDate.getMonth()
    if (month < 0 || (month === 0 && today.getDate() < bthDate.getDate())) {
      tempAge--
    }

    // 만 나이에 따른 연령대 세팅
    tempAge = tempAge.toString()
    this.age = tempAge.replace(/.$/, '0')
    this.age = this.age > 50 ? 50 : Number(this.age)

    this.$setAppData('main-age', this.age)
  }
}
```
+ `const today = new Date()`: Date()생성자 생성
+ `const bthDate = new Date(this.bthdt.year, this.bthdt.month, this.bthdt.day)` : `data(){}`에 선언해준 `bthdt`객체의 각각의 이름을 써주어서 년도,월,날짜를 반환하게 한다.
+ `let tempAge = today.getFullYear() - bthDate.getFullYear()`: 지금 년도에서 선택된 년도를 빼준다.
+ `const month = today.getMonth() - bthDate.getMonth()`: 지금 월에서 선택된 월을 빼준다.
+ `if (month < 0 || (month === 0 && today.getDate() < bthDate.getDate()))`
  + 만약 월이 0보다 작거나 월이 0이랑 같으면서 오늘 날짜가 선택된 날짜(태어난 일)보다 작으면 나이를 하나 줄여준다.
