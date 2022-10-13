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

