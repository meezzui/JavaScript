#### 다른 페이지 갔다 왔을 때 지도/목록 소팅 초기화 안 되는 현상 해결✅
+ 문제🛑
  + 지도를 옮겼을 때 버튼을 누르면 해당 위치와 가까운 스토어가 소팅되는 기능을 구현하였다.
  + 그런데 다른 페이지를 갔다 왔을 때 그 페이지가 다시 초기화 되는 것이 아니라 다른 페이지를 가기 전 상태 그대로 남아있는 문제가 발생했다.

+ 원인은??🧐
  + 초기화 문제였다.
  + 처음 페이지를 타면 기본으로 설정해둔 값으로 바껴야 하는데 그게 동작하고 있지 않아서 계속 이전 데이터가 남아있게 되었다.

+ 해결방법😎
  + 뷰에는 `ionViewWillEnter()`라는 함수가 있다. 이 함수는 페이지를 진입했을 때 타는 함수이다.
  + 여기에서 지도와 목록 초기화할 때 사용되는 값들을 초기화 해준다.
  ```node
   reset() {
    this.storeList = [] // 스토어 리스트 초기화
    this.mapCenter = { // 지도 중심좌표 초기화
      lat: this.$store.getters.defaultLatitude,
      lng: this.$store.getters.defaultLongitude
    }
    // 사용자 위치 초기화
    this.params.userLati = '' 
    this.params.userLongi = ''
    this.params.orderGbn = 'REG' // 등록순으로 초기화
  }
  ```

#### 🎇 알게 된 점 🎇
+ data(){} 부분에 `params`로 아래와 같이 선언해주었다.
```node
data(){
  params: {
    ctgrSeqNo: 0,
    orderGbn: 'REG',
    plNo: '',
    page: 1,
    size: 40
  }
 userLongi: this.$store.getters.defaultLongitude,
 userLati: this.$store.getters.defaultLatitude
}
```
+ 이렇게 선언해주면 params안에 있는 것은 this.params. 이런식으로 선언하여 값을 변경해줄 수 있는데 버튼 클릭 시 받아오는 지도의 사용자 위치 값도 보내줘야 해서 this.params형식으로 값을 보내주었다.
+ 위에 페이지에 진입할 때 `userLongi`와 `userLati`의 값을 초기화 해줬는데 페이지를 나갔다 오면 `userLongi`와 `userLati`에 값이 전혀 들어가지 않아서 목록 초기화 셋팅이 안 되는 문제가 생겼었다.
+ 그 이유는❓❓
  +  목록을 소팅할 때 보내주는 `this.params` 값에 `userLongi`와 `userLati`이 없어서 그런 것이다.
  + 난 에초에 `params`를 선언해줄 때 `params`안에 `userLongi`와 `userLati`가 없었기 때문에 그냥 `this.userLongi`와 `this.userLati` 하여 클릭 했을 때 타는 함수 안에다가 지도를 움직일 때마다 사용자 위치를 받아오는 값을 셋팅해줬었는데 이렇게 하면 안 되었었다.
+ 즉, `this.params.userLongi`와 `this.params.userLati` 이렇게 해줘야 했었다. 이렇게 해줘도 `params`안에 값이 셋팅된다.(난 이렇게 하면 안 되는건 줄 알았지...😓)
