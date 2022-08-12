#### 설문조사 api 연동
+ 일단 설문조사에는 등록과 조회가 있잖아??
+ 그럼 api를 짤때 조회먼저 짜고 그 다음 등록을 하면 되는데 백에서 등록된 설문조사가 없을 경우에는 response를 빈값으로 내려오게 되어있어서 등록하는 로직을 먼저 짜야해
+ 등록하는 로직 구현✅
  + 먼저 데이터 가공부터 해야해. 아래 보이는 코드는 `data()`안에 선언해준 부분이야. 각각 `input`태그와 `textarea`태그에 `v-model`로 연결되어 있어
  + 그리고 객체의 키값은 api에 있는 이름과 동일하게 적었어. 이렇게 하면 `...this.checkList` 이렇게 쓸 수 있어서 더 편해
  ```node
  checkList:
    { ans1: '',
      ans11: '',
      ans12: '',
      ans21: '',
      ans22: '',
      ans23: '',
      ans24: '',
      ans25: '',
      ans26: '',
      ans3: '',
      ans4: ''
    },
    review: ''
  ```
  + 자, 데이터를 가공해보자. 일단 함수를 `try{} catch{}`문으로 묶은 다음 변수를 하나 선언하여 객체를 만든다.
  ```node
  async regServey() {
    try {
      const data = {
        regPsId: this.custId,
        ...this.checkList,
        ans5: this.review

        await registServey(data)
        await this.getServeyInfo()
      }
    } catch (e) {
      console.log(e)
    }
  }
  ```
  + `await registServey(data)` 이렇게 객체로 만든 것을 await를 사용하여 api와 통신하게 한다.
  + 등록이 되면 바로 조회를 할 수 있게 `await this.getServeyInfo()` 조회 함수도 통신하여 넣어준다.
  + 참고📢 `registServey()`는 api통신을 위해 `post`하는 `url`을 작성해 놓은 파일을 `import`해서 사용한 것이다.
+ 조회하는 로직 구현✅
  + 조회는 회원 아이디로 조회를 한다.
  + 그래서 회원 아이디를 가져올 수 있게 아래처럼 만들어준다.
  ```node
  ionViewDidEnter() {
    getInfo().then(res => {
      this.custId = res.data.membId
      this.getServeyInfo()
    })
  }
  ```
  + `ionViewDidEnter()`: 페이지가 엑티브 되고 나서 실행된다. 즉, 페이지 표시할때 마다 실행되며 페이지가 뜰때마다 갱신된다.
    + 이 함수 안에 `api주소`가 적힌 파일을 `import`한 `getInfo()`를 사용하여 회원 아이디를 가져온다.
    + 그리고 이 안에서 `getServeyInfo()`






