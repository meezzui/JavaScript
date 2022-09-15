#### 구글 맵 infoWindow 클릭 시 해당 상품 상세 페이지로 이동
+ `infoWindow`에 스토어 이름을 클릭하면 해당 상품의 상세페이지로 이동하는 기능을 구현하였다.
```node
setMarker(Points, title, place) {
  this.imgSrc = ''
  this.clickImgsrc = ''
  this.markers = []

  this.imgSrc = new window.google.maps.MarkerImage(require('@/assets/image/map_green.svg'))
  this.clickImgsrc = require('@/assets/image/map_marker.svg')
  this.marker = null
  this.marker = new window.google.maps.Marker({
    position: Points,
    map: this.map,
    icon: this.imgSrc,
    title: title
  })
  // 마커 상세 정보
  this.contentString =
    '<div id="map_info_contain">' +
    `<div class="map_store_img"><img src="${place.img}"></div>` +
    '<div class="map_details_wrapper">' +
    '<div class="map_details_sec1">' +
    `<div><a id="detailBtn" onclick="goInfo(${place.plNo})"><p class="map_store_name">${place.mainTitle}</p></a></div>` + `<div class="map_info_checkbox"><input id="plLikeBtn" type="checkbox" onclick="infoWindowLike()"></div>` +
    // `<div><p class="map_store_name">${place.mainTitle}</p></div>` +
    '</div>' +
    '<div class="map_details_sec2">' +
    `<div class="map_category"><p class="map_category_p">${place.stORCtgr}</p></div>` + '<div class="map_star"><img class="map_star_img" src="/img/Rating.png"></div>' + `<div class="average_num"><p class="average_num_p">${place.rating}</p></div>` + `<div class="map_review_num"><p class="map_review_num_p">${'(' + place.rvCnt + ')'}</p></div>` +
    '<div><p>'
  for (let i = 0; i < place.tags.length; i++) {
    this.contentString += `<span class="map_tag">#${place.tags[i].tagNm}</span>`
  }
  this.contentString += '</p></div>' + '</div>' +
  '</div>' +
  '</div>'

  // eslint-disable-next-line no-undef
  this.infowindow = new google.maps.InfoWindow({
    content: this.contentString
  })
  this.infoWindows.push(this.infowindow)
  // 마커 클릭 이벤트
  if (this.device === 'PC') {
    window.google.maps.event.addListener(this.marker, 'click', async() => {
    // info 창 닫기
      this.infoWindows.forEach(i => {
        i.close()
      })
      this.infowindow.open({
        anchor: this.marker,
        map: this.map,
        shouldFocus: false
      })
      if (!this.selectedMarker || this.selectedMarker !== this.marker) {
        !!this.selectedMarker && this.selectedMarker.setIcon(this.imgSrc)
        this.marker.setIcon(this.clickImgsrc)
      }
      this.selectedMarker = this.marker
      this.params.plNo = this.marker.title
      const res = await requstTourPlaceList(this.params)
      this.TourInfoList = []
      this.paging.total = res.data.totCnt
      res.data.places.forEach(p => {
        this.TourInfoList.push({
          stORCtgr: p.ctgrNm, // 상단 우측
          mainTitle: p.plNm, // 상품 이름
          subTitle: p.plSbj, // 메인타이틀 하단 서브 타이틀
          img: p.tmnlImgUrl, // 이미지
          fvrYn: p.fvrYn, // 즐겨찾기 여부
          fvrGbn: 'S', // 즐겨찾기 대상구분,
          fvrVal: p.plNo, // 즐겨찾기 대상 번호
          rating: p.rvScr, // 별점
          rvCnt: p.rvCnt, // 리뷰 갯수
          DcYn: p.frcsDcYn, // 할인 여부
          DcVal: p.frcsDcVal, // 할인률?
          tags: p.tags,
          plLati: p.plLati,
          plLongi: p.plLongi,
          plNo: p.plNo,
          postNoAddr: p.postNoAddr
        })
      })
      // infoWindow 창에 스토어 이름을 클릭하면 상세 페이지로 이동
      window.goInfo = (plNo) => {
        const goInfo = document.getElementById('detailBtn')
        if (goInfo.click) {
          this.$router.push({ name: 'placeDetail', params: { plNo: plNo }})
        }
        this.params.plNo = ''
      }
    })
    this.markers.push(this.marker)
  }
}
```
#### 시행착오🤦🏻‍♀️
+ 마커 상세 부분을 보면 `this.cotentString`으로 시작되는 부분이 있다. 이부분이 바로 상세 정보 즉, 팝업창 UI이다. 
+ 저기서 ``<div><a id="detailBtn" onclick="goInfo(${place.plNo})"><p class="map_store_name">${place.mainTitle}</p></a></div>``이 부분을 보면 `onclick="goInfo(${place.plNo})"`으로 `onclick()`함수를 볼 수 있다.
+ 처음에 a태그가 아닌 div태그에 `onclick()`함수를 써서 했지만 `onclick()`함수가 아예 동작하지 않았다. 그리고 `onclick()`함수에 페이지 번호를 넣어서 보내줘야 하는데 그것 또한 먹히지 않았다.
+ 그래서 링크 이동 기능이 있는 a태그로 묶고 거기에 `onclick()`함수를 사용하여 `onclick="goInfo(${place.plNo})"`이렇게 해당 페이지 번호를 넘겨주었다.

#### 상세 페이지로 이동
```node
// infoWindow 창에 스토어 이름을 클릭하면 상세 페이지로 이동
window.goInfo = (plNo) => {
  const goInfo = document.getElementById('detailBtn')
  if (goInfo.click) {
    this.$router.push({ name: 'placeDetail', params: { plNo: plNo }})
  }
  this.params.plNo = ''
}
```
+ `this.params.plNo = ''` 이렇게 해준 이유는 상세 페이지를 갔다가 다시 목록 페이지로 왔을 경우 목록이 초기화가 되지 않는 문제가 발생하였다.🙀
+ 목록이 초기화 되지 않았던 이유는 페이지 번호가 초기화 되지 않고 선택되었던 페이지 번호 그대로 가지고 있어서 였다.
+ 그래서 `this.params.plNo = ''` 이 코드를 추가하여 페이지 이동 시 페이지 번호를 초기화 시켜주었다‼️ 

#### 📢참고 `${}` 의미
+ `${}`란❓❓
