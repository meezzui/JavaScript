#### 버튼 클릭 시 클래스 추가하기
+ 버튼을 클릭 했을 때 원하는 곳에 클래스 추가
```node
// 버튼 클릭 템플릿단
<div class="roulette_start_btn" @click="startLoulette()">
 <img src="@/assets/image/event-roulette-start-btn.png" alt="룰렛 시작">
</div>
// 돌아가는 룰렛 부분 템플릿단
<div class="roulette_event">
  <img :class="roulletteClass" src="@/assets/image/event-roulette.png" alt="룰렛">
</div>

<script>
// 스크립트단
data() {
  return {
    roulletteClass: []
  }
},
methods: {
  // 룰렛 시작 버튼 클릭 시 클래스 추가
  startLoulette() {
  this.roulletteClass.push('rotation-item')
}
</script>
```
+ `@click="startLoulette()"`: 버튼 클릭 시 해당 함수 실행
+ `:class="roulletteClass"`: 클래스 바인딩으로 data()에 선언해준 클래스 배열을 넣어준다. 그러면 저기에 push한 클래스들이 들어가게 된다.
+ `this.roulletteClass.push('rotation-item')`: 해당 배열에 원하는 클래스 이름을 넣어준다.
  + 참고📢 `document.getElementsByClassName('roulette_event').addClass('rotation-item')` 이렇게 해도 되지만 위의 방법이 더 간편하다.
