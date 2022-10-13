#### 버튼 클릭 시 해당 위치에서 가까운 스토어 목록 소팅하기
+ 지도를 움직이고 해당 위치에서 버튼을 누르면 그 주변에 위치한 해당 스토어들로 목록이 다시 소팅된다.
+ `getCenter()` 라는 메소드를 사용해서 지도의 중심을 구한다.
  + `getCenter()`란❓❓ 지도의 현재 중심의 위도/경도를 반환하는 메소드이다.
```node
data(){
  params: {
    orderGbn: 'REG',
    ctgrSeqNo: '0',
    userLongi: this.$store.getters.defaultLongitude, // 기본값 셋팅해 놓은 것
    userLati: this.$store.getters.defaultLatitude, // 기본값 셋팅해 놓은 것
    size: 20,
    page: 1

  }
},

// 클릭 시 해당 위치에서 가까운 목록 소팅
async sortingListBtn() {
  const info = JSON.stringify(this.map.getCenter()) // 중심을 가져와서 문자열로 반환
  const latLng = JSON.parse(info) // 문자열로 반환된 것을 다시 객체로 변환한다.

  this.mapCenter.lng = latLng.lng // 받아오는 중심값을 지도의 센터에 넣어준다
  this.mapCenter.lat = latLng.lat
  this.params.userLongi = latLng.lng // 받아온 중심값을 사용자 위치값에 넣어준다.
  this.params.userLati = latLng.lat
  this.params.orderGbn = 'DST' // orderGbn 값은 거리순인 'DST'로 지정해준다.
  this.storeList = [] // 스토어 리스트 목록 초기화 - 초기화를 안 해주면 기존 리스트 밑으로 조회된 스토어들이 아래로 계속 쌓이게 된다.

  await this.getStoreList(this.params) // 가까운 거리에 있는 스토어 목록을 보여주기 위해서는 받아온 중심값이 필요한데 그 값을 목록 소팅할 때 넣어주어야 한다. 그래서 기존에 형식과 같은 형식으로 값을 넣어서 보내주었다.
}
```
