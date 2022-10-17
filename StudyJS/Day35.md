#### 구글 지도 줌 레벨 유지
+ 지도에 '현 지도에서 검색'이라는 버튼을 누르면 해당 위치에서 젤 가까운 스토어 40개가 소팅되게 해놨는데 지도를 확대/축소하고 그 버튼을 누르면 목록은 소팅이 되는데 다시 원래 줌 레벨로 돌아오는 현상이 생겼다.
+ 해결 방법✅
  + 버튼을 눌렀을 때 타는 함수에 지도를 확대/축소 할 때마다 줌 레벨 값을 받아와서 그것을 지도의 `zoom`값에 넣어주면 된다.
  + `map.getZoom()` 함수 사용
  ```node
  // 클릭 시 해당 위치에서 가까운 목록 소팅
    async sortingListBtn() {
      const info = JSON.stringify(this.map.getCenter())
      const latLng = JSON.parse(info)

      // 지도 줌 레벨 유지
      const mapZoom = this.map.getZoom()
      this.map.zoom = mapZoom

      this.mapCenter.lng = latLng.lng
      this.mapCenter.lat = latLng.lat
      this.params.userLongi = latLng.lng
      this.params.userLati = latLng.lat
      this.params.orderGbn = 'DST'
      this.storeList = []

      await this.getStoreList(this.params)
    }
  
  // 지도 생성 (구글)
  this.map = new window.google.maps.Map(document.getElementById('map'), {
    center: this.mapCenter,
    zoom: 17, // 기본값은 17로 설정
    minZoom: 12,
    streetViewControl: false,
    mapTypeControl: false,
    fuulscreenControl: true,
    zoomControl: true,
    styles: myStyles
  })
  ```
+ 그런데 이렇게 하면 기능이 제대로 작동하지 않는다. 콘솔을 찍어봤더니 버튼을 누르면 타는 함수에서는 zoom 레벨이 잘 바뀌는 그 바뀐 값이 원래 기본값을 설정해둔 `zoom`값이 바뀌지 않았다.
+ 그렇다면 어떻게 해야할까⁉️
  + `data(){}`부분에 변수를 하나 선언하여 거기에 줌 레벨의 기본값을 설정해주고 사용하는 곳에서 `this.`을 이용해 값을 바꿔주었다.
  ```node
  data(){
    mapZoom: 17
  }
  
  
  // 지도 생성 (구글)
  this.map = new window.google.maps.Map(document.getElementById('map'), {
    center: this.mapCenter,
    zoom: this.mapZoom // this. 을 이용하여 사용
    minZoom: 12,
    streetViewControl: false,
    mapTypeControl: false,
    fuulscreenControl: true,
    zoomControl: true,
    styles: myStyles
  })
  
  
  // 클릭 시 해당 위치에서 가까운 목록 소팅
  async sortingListBtn() {
      const info = JSON.stringify(this.map.getCenter())
      const latLng = JSON.parse(info)

      // 지도 줌 레벨 유지
      this.mapZoom = this.map.getZoom()

      this.mapCenter.lng = latLng.lng
      this.mapCenter.lat = latLng.lat
      this.params.userLongi = latLng.lng
      this.params.userLati = latLng.lat
      this.params.orderGbn = 'DST'
      this.storeList = []

      await this.getStoreList(this.params)
    }
  
  ```
