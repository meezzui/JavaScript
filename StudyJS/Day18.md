#### 모바일과 pc의 페이지 이동 차이
+ 모바일은 다른 창으로 넘어갈 때 페이지 이동을한다. 그러나 pc는 페이지 이동을 하는 경우도 있지만 팝업창으로 페이지 이동을 대체하는 경우가 있다.
+ 이러한 경우 모바일에서는 잘 동작하던 기능들이 pc버전에선 안 되는 경우가 있다.
+ 그 이유는 모바일에서 페이지 이동처리가 되어있기 때문이다.
+ pc버전에서도 잘 동작하려면 그 해당 api 값을 모달창을 띄울 때 같이 넘겨주어야 한다.
+ 예시(리뷰작성 팝업창 띄우기)
```node
<tempale>
<div role="btn">
  <p @click="device === 'PC' ? openModal() : goReview()">{{$t('reviewWrite')}}</p>
</div>
</template>
<script>
import makeReview from './ReviewWrite.vue' // 모달로 띄울 페이지 import해주기(이름은 내 맘대로 지정)
import { modalController } from '@ionic/vue' // vue의 모달 라이브러리 사용

data(){
 return{ // pc 팝업 띄울 때 보내지는 값 셋팅
     popReview: {
     id: '',
     rv: 'F',
     ordNo: 0
   }
 }
}
methods:{
// 리뷰 등록 페이지로 이동
    goReview() {
      this.$router.push({ name: 'ReviewWrite', params: { id: this.storeInfo.frcsId, rv: 'F', ordNo: 0 }})
    }
    
// pc에서 모달로 띄우기
 async openModal() {
   this.popReview.id = this.storeInfo.frcsId // id값 보내기
   const component = { title: this.$t('reviewWriteTitle'), comp: makeReview, class: 'make-review-h' } // 객체 형태로 props로 보낼 것
   const modal = await modalController
     .create({
       component: component.comp,
       cssClass: ['pc-modal-sm', component.class], // css로 커스텀해줄 것이기 때문에 원하는 class명 작성
       backdropDismiss: false, // 외부 클릭시 꺼지기
       componentProps: {
         popTitle: component.title, // 위에서 작성한 타이틀 `props`로 보내기
         popReview: this.popReview, // data에 선언해준 객체를 `props`로 보내기
         close: () => { // x표를 누를 시 모달창 꺼짐
           this.$alert({ // 꺼지기 전에 뜨는 알림창(진짜 취소할 것이냐)
             msg: this.$t('cancelReviewWriteMessage'),
             left: this.$t('cancel'),
             right: this.$t('confirm'),
             success: () => { // 성공시
               modal.dismiss()  // 모달창 꺼짐
               this.getReview() // 모달창이 꺼지면 등록된 리뷰를 다시 조회해줌
             }
           })
         },
         closeModal: () => { // 완전히 꺼지게 하기 위해 새로 함수 선언
           modal.dismiss()
           this.getReview()
         }
       }
     })
   return modal.present()
 }
}
</script>
```
+ `<p @click="device === 'PC' ? openModal() : goReview()">{{$t('reviewWrite')}}</p>` : 클릭했을 때 pc일 경우 `openModal()` 함수를 타고 모바일일 경우 ` goReview()`을 탄다.
+ `goReview()` 함수는 말 그대로 페이지가 이동되는 로직이다.
+ `openModal()` 함수는 pc버전일 경우 팝업창으로 리뷰쓰는 창을 띄우는 함수이다.
  + 팝업으로 띄울 때 모바일에 `params`로 보내준 해당 값들을 같이 보내줘야 한다. => `this.popReview.id = this.storeInfo.frcsId`(id값, 나머지는 `popReview`로 보냄)

+ 리뷰쓰기 페이지✏
  + `props: ['popTitle', 'close', 'popReview', 'closeModal', 'popWriteReview']` 이렇게 porps로 선언해서 사용



