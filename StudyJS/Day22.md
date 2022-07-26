#### 구글맵 마커에 마우스 올리면 관련 정보 나오는 기능 구현
<img width="300" src="https://user-images.githubusercontent.com/86812098/179680590-a90ca16d-f91f-46bf-8c65-93653e2ec763.png">

+ `Info Windows`를 이용❗❗
  + 구글 맵 `info windows`를 이용하여 기능을 구현할 수 있다. 📢[구글 맵 API 보러가기 👉](https://developers.google.com/maps/documentation/javascript/infowindows)
  + 마커 상세정보 퍼블리싱 및 api연동 부분
  ```node
  // 마커 상세 정보
  let contentString =
    '<div id="map_info_contain">' +
    `<div class="map_store_img"><img src="${store.tmnlImgUrl}"></div>` +
    '<div class="map_details_wrapper">' +
    '<div class="map_details_sec1">' +
    `<div><p class="map_store_name">${store.frcsNm}</p></div>` + `<div class="map_info_checkbox"><input id="likeBtn" type="checkbox"     onclick="infoWindowLike()"></div>` +
    '</div>' +
    '<div class="map_details_sec2">' +
    `<div class="map_category"><p class="map_category_p">${store.ctgrNm}</p></div>` + '<div class="map_star"><img class="map_star_img" src="/img/Rating.png"></div>' + `<div class="average_num"><p class="average_num_p">${store.rvScr}</p></div>` + `<div class="map_review_num"><p class="map_review_num_p">${'(' + store.rvCnt + ')'}</p></div>` +
    '<div><p>'
  for (let i = 0; i < store.tags.length; i++) {
    contentString += `<span class="map_tag">#${store.tags[i].tagNm}</span>`
  }
  contentString += '</p></div>' + '</div>' +
  '</div>' +
  '</div>'
  ```
  + `infowindow` 객체 생성
  ```node
  const infowindow = new google.maps.InfoWindow({
    content: contentString
  })
  this.infoWindows.push(infowindow)
  ```
  + `infowindow` 창 열고 닫기(열기 전에 닫아줘야 다른 마커를 클릭했을 때 전에 클릭되어서 열린 정보가 닫히고 새로 클릭한 정보가 열린다.)
   ```node
    // info 창 닫기
    this.infoWindows.forEach(i => {
      i.close()
    })

    // info 창 열기
    infowindow.open({
      anchor: marker,
      map: this.map,
      shouldFocus: false
    })  
   ```
#### 위의 요소들을 합치면~~
```node
setMarker(Points, title, store) {
  this.markers = []
  const imgSrc = new window.google.maps.MarkerImage(require('@/assets/image/map_green.svg'))
  const clickImgsrc = require('@/assets/image/map_marker.svg')
  let marker = null
  marker = new window.google.maps.Marker({
    position: Points,
    map: this.map,
    icon: imgSrc,
    title: title
  })
  // 마커 상세 정보
  let contentString =
    '<div id="map_info_contain">' +
    `<div class="map_store_img"><img src="${store.tmnlImgUrl}"></div>` +
    '<div class="map_details_wrapper">' +
    '<div class="map_details_sec1">' +
    `<div><p class="map_store_name">${store.frcsNm}</p></div>` + `<div class="map_info_checkbox"><input id="likeBtn" type="checkbox" onclick="infoWindowLike()"></div>` +
    // `<div><p class="map_store_name">${store.frcsNm}</p></div>` +
    '</div>' +
    '<div class="map_details_sec2">' +
    `<div class="map_category"><p class="map_category_p">${store.ctgrNm}</p></div>` + '<div class="map_star"><img class="map_star_img" src="/img/Rating.png"></div>' + `<div class="average_num"><p class="average_num_p">${store.rvScr}</p></div>` + `<div class="map_review_num"><p class="map_review_num_p">${'(' + store.rvCnt + ')'}</p></div>` +
    '<div><p>'
  for (let i = 0; i < store.tags.length; i++) {
    contentString += `<span class="map_tag">#${store.tags[i].tagNm}</span>`
  }
  contentString += '</p></div>' + '</div>' +
  '</div>' +
  '</div>'

  // eslint-disable-next-line no-undef
  const infowindow = new google.maps.InfoWindow({
    content: contentString
  })
  this.infoWindows.push(infowindow)

  // 마커 클릭 이벤트
  window.google.maps.event.addListener(marker, 'click', async() => {
    console.log('??', marker)

    // info 창 닫기
    this.infoWindows.forEach(i => {
      i.close()
    })
    infowindow.open({
      anchor: marker,
      map: this.map,
      shouldFocus: false
    })
},
```
