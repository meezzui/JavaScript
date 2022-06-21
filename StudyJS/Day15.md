#### props란❓❓
부모에서 자식 컴포넌트로 데이터 전달

#### 카테고리 슬라이드 컴포넌트(자식)
+ 어느 페이지에서든 카테고리 슬라이드를 사용할 수 있게 컴포넌트로 따로 빼주었다.
+ 그리고 props로 `'list', 'disable', 'idx'`를 넘겨주었다.
  + `v-if="!disable"` 이것은 사용단에서 disable이 true인 경우에만 이 카테고리 슬라이드가 보여지게 하는 용도로 사용된다.
+ 웹접근성에 맞게 하기 위해 `<span v-if="idx === undefined ? c === 0 : c === idx" class="sr-only">선택됨</span>`을 추가했다.
  + 카테고리가 선택되면 '선택됨'이라고 표시가 떠야한다.(화면적으로는 보이지 않게 `display:none` 처리했다. => 개발자 모드로 보면 보임)
+ 여기서 키포인트🔑🔑🔑
  + `@click="$emit('select-category', {category, idx: c})"`
    + `$emit`으로 카테고리를 클릭했을 경우 category와 idx를 `select-category`라는 이름으로 오브젝트 형식으로 넘겨주고 있다.
    + 즉, 키값과 value값이 같으면 선택되게 하는 것이다.
```node
<swiper v-if="!disable" :slidesPerView="'auto'" :spaceBetween="10" class="swiper">
    <swiper-slide v-for="(category, c) in list" :key="c"  class="swiper-slide">
        <input :id="category.value" name="favoriteCategory" type="radio" :value="category" :checked="idx === undefined ? c === 0 : c === idx">
        <label :for="category.value" role="btn" @click="$emit('select-category', {category, idx: c})">{{category.value}}</label>
        <span v-if="idx === undefined ? c === 0 : c === idx" class="sr-only">선택됨</span>
    </swiper-slide>
  </swiper>
 
 <script>
 
  props: ['list', 'disable', 'idx']
  data() {
    return {
      selectedCategory: ''
    }
  }
  
 </script>

```
#### 카테고리 슬라이드 사용하기(부모)
+ 카테고리 슬라이드를 사용해보자😉
+ 카테고리 컴포넌트에서 props로 넘겨준 값을 여기에서 사용한다.
  + `:list`를 바인딩하여 사용단에서 사용할 카테고리 리스트의 이름을 지정해준다.(categoryList)
    + `data(){}` 안에 선언해준다.
  + `:idx`를 바인딩하여 사용할 이름을 지정해준다.(selIdx)
    + `data(){}` 안에 선언해준다.
  + `@select-category`: `$emit`으로 보낸 `select-category`의 객체를 사용할 함수 이름을 지정해준다. 
+ 그리고 `selectCategory`함수에 넘겨받은 `category`와 `idx`를 사용해준다.
  + 코딩방법은 두가지❗❗❗
    + `async selectCategory(info)` : info 자체가 객체이기 때문에 idx를 사용하기 위해선 `this.selIdx = info.idx`이렇게 추가해주면 된다. 즉, info가 category와 idx를 둘다 가지고 있다.
    + `async selectCategory({info, idx})` : 객체로 묶어서 따로따로 풀어서 써주는 방법이 있다. 이럴 경우  idx를 사용하기 위해선 `this.selIdx = idx` 이렇게 적어주면 된다.

```node
<template>
   <CategoryMenu  :list="categoryList"  :idx="selIdx" @select-category="selectCategory"/>
</template>

<script>
data(){
  selIdx: null // selIdx: 0 도 된다.
  categoryList: []
}
methods:{
  // 카테고리 선택 시 카테고리에 해당되는 상품 조회
  async selectCategory(info) { // selectCategory({category, idx}) 이것도 가능
    this.selIdx = info.idx // this.selIdx = idx
    // console.log(test.category)
    this.params.ctgrSeqNo = info.category.key
    this.category = info.category.value

    // this.getProductList()
    await this.getLocation()
  }
}
</script>
```
