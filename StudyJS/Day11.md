#### css `opacity`와 `rgba`의 차이점
+ `opacity`를 사용하여 배경색에 투명도를 주었다. 그런데 배경색 뿐만 아니라 하위 요소들까지 모두 투명도가 적용되는 현상이 나타났다..😅
+ `opacity`는 투명도를 조절해주는 css 프로퍼티인데 이것은 해당 div의 하위 요소까지 모두 투명하게 만드는 특징이있다.
+ 그렇다면 배경색만 투명하게 하고 싶을 때 어떻게 해야할까❓❓❓
  + `rgba`를 사용한다❗❗❗
  + `rgba`는 해당 div요소에만 투명도가 적용되게 하는 특성이 있다. 그래서 해당 요소만 투명하게 하기 위해서는 `rgba`를 사용하면 된다.
  + 예) rgba(r,g,b,투명도)

#### 선택된 이미지만 css 변경
```node
<div v-for="(store, s) in storeZoneList" :key="s" class="store_img_list_box">
  <div :class="clickZone === s ? 'store_img store_zone_click ' : 'store_img'" @click="clickedStoreZone(s)">
    <img src="@/assets/image/signupcomplete.png" alt="store img">
  </div>
  <div class="store_zone">
    <p>Zone2</p>
  </div>
</div>

<script>
data() {
  return {
    clickZone: 0,
    storeZoneList: [{}, {}, {}]
  }
},
methods: {
  clickedStoreZone(idx) {
    this.clickZone = idx
  }
}
</script>
```
+ 기본으로 첫번째 요소가 선택되어 있게 보이기 위해  `clickZone: 0`라고 데이터에 선언해주었다.
+ `@click="clickedStoreZone(s)"` : 클릭했을 때 `storeZoneList`의 인덱스값을 넘겨준다.
+ `clickedStoreZone(idx)`: 받은 인덱스 값을 `clickZone`에 넣어준다.
+ `:class="clickZone === s ? 'store_img store_zone_click ' : 'store_img'"`
  + 그 받은 인덱스가 `storeZoneList`의 인덱스 값과 같으면 `store_zone_click`라는 css가 적용된다.

