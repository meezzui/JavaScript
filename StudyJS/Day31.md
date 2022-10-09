#### 에러 일지 - 지도 infoWindow 안 열리는 문제 해결✅
+ 처음 페이지를 탈 경우에는 잘 열리는데 해당 스토어 상세 페이지를 갔다가 다시 목록 페이지로 돌아와서 목록을 클릭 했을 경우 `infoWindow`가 열리지 않는 현상이 발생했었다.
+ 해결✅
  + 지도에 표시되는 마커를 initMap() 즉, 지도를 그릴 때 초기화 해주었더니 해결 되었다.
  + 보통 이런 경우는 초기화 문제이다‼️

```node
initMap() {
  this.markerInfo = []
  this.markers = []
  this.infoWindows = []

  const myStyles = [
    {
      featureType: 'poi',
      elementType: 'labels',
      stylers: [
        { visibility: 'off' }
      ]
    }
  ]
  // 지도 생성 (구글)
  this.map = new window.google.maps.Map(document.getElementById('map'), {
    center: this.mapCenter,
    zoom: 16,
    minZoom: 12,
    streetViewControl: false,
    mapTypeControl: false,
    fuulscreenControl: true,
    zoomControl: true,
    styles: myStyles
  })

  for (let i = 0; i < this.markerPositions.length; i++) {
    this.setMarker(this.markerPositions[i], this.markerTitles[i], this.storeList[i], i)
  }
  this.userMarker(this.mapCenter)
  this.$nextTick(() => {
    this.dismissLoading()
  })
  this.map.addListener('click', () => {
    this.storeList = []
    this.markerInfo = []
    this.markers = []
    this.getStoreList()
  })
}
```
