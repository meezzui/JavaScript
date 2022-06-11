#### 아이디 찾기🔍
+ 일반 앱으로 회원가입한 회원일 경우 아이디를 노출시키고, 간편 회원가입한 회원일 경우 아이디 노출 대신 어떤 방법으로 간편 회원가입 했는지 문구 노출
+ 예) 간편회원가입 => (간편)카카오로 가입된 회원입니다. / 앱 회원가입 => fgjdk****
+ 최종 아이디/간편 회원 문구 노출되는 페이지는 이 전 단계의 페이지에서 url로 회원의 아이디와 어떤 방법으로 회원가입했는지 구분해주는 api를 받아서 보여준다.

#### 최종 아이디/간편 회원 문구 노출되는 페이지의 이전 페이지
+ `params`랑 `query`로 회원의 아이디와 어떤 방법으로 회원가입을 했는지의 여부를 구분하는 값을 넘겨준다.
+ `name: 'FindId', params: { membId: res.data.membId }, query: { mdaGbn: res.data.mdaGbn }`
  + `name`에은 넘겨주는 페이지의 `path`이름을 적는다. 
  + `params`와 `query`에는 오브젝트(`{ }`) 형태로 넘겨줄 해당 api의 값을 적어준다.
```node
      findMembId(this.findAccntForm).then(res => {
        this.$router.push({ name: 'FindId', params: { membId: res.data.membId }, query: { mdaGbn: res.data.mdaGbn }})
      }).catch(e => { // 에러 메시지 
        console.error(e)
        this.eamilConfirmYn = false
        this.$alert({
          title: e.data.errorMessage,
          single: this.$t('check')
        })
      })
    }
```
#### 최종 아이디/간편 회원 문구 노출되는 페이지
+ `created()` 함수 : data, methods 속성이 정의되어서 접근 가능❗❗
+ `data(){ }` 안에 `membId: ''`, `mdaGbn: ''` 이렇게 아이디값과 회원가입 구분값을 빈값으로 선언해준다.
+ 그리고 `created()` 함수 안에 $router를 이용해서 저장된 것을 가져온다.
  + `this.membId = this.$route.params.membId`, `this.mdaGbn = this.$route.query.mdaGbn`
+ template단
  + `<p v-if="this.mdaGbn === 'APP'">{{this.membId}}</p>`: `v-if`로 앱으로 회원가입한 회원일 경우 회원 아이디가 보이게 하고
  + `<p v-else>{{$t('simpleSignUpMember', {flag: sns[mdaGbn]})}}</p>`: 그렇지 않을 경우 어떤 경로로 회원가입했는지를 보여준다.
    + `$t('simpleSignUpMember', {flag: sns[mdaGbn]})` 이것은 언어프로퍼티로 따로 빼기 위해서 이렇게 해주었다.
+ 주의🧨🧨
  + 간편회원가입 경로가 다양하기 때문에 `data(){ }`안에 배열을 하나 선언해준다.
  + 그리고 그 안에 `mdaGbn`의 구분값을 해당 키값으로 잡아서 간편 회원가입의 종류를 넣어준다.
  + 그러면 `mdaGbn`의 해당하는 값으로 어떤 경로로 회원가입했는지가 노출된다.
```node
<template>
  <ion-page :force-overscroll="false">
    <BaseLayout :header="{title:$t('findAccountPage'),close:true, displayNone: true}" :fullWidth="true">
      <template #con>
            <form>
=====================================================(생략)================================================
            <ion-row>
              <div class="return-id">
                <p v-if="this.mdaGbn === 'APP'">{{this.membId}}</p>
                <p v-else>{{$t('simpleSignUpMember', {flag: sns[mdaGbn]})}}</p>
              </div>
            </ion-row>
======================================================(생략)===============================================
          </form>
        </div>
      </template>
    </BaseLayout>
  </ion-page>
</template>

<script>
import {
  IonPage,
  IonRow
  } from '@ionic/vue'
  import { defineComponent } from 'vue'
  export default defineComponent({
  name: 'FindId',
==========================(생략)======================
  created() {
    this.membId = this.$route.params.membId
    this.mdaGbn = this.$route.query.mdaGbn
  },
  data() {
    return {
      membId: '',
      mdaGbn: '',
      sns: [
        KAKAO: this.$t('kakao'),
        NAVER: this.$t('naver'),
        GOOGLE: this.$t('google'),
        FACEBOOK: this.$t('facebook'),
        TWITTER: this.$t('twitter')
      ]
    }
  }
})
</script>
```
### $route란??🧐
+ `this.$route.params` 등의 코드에 나오는 `$route` 는 `Route 객체`다.
+ 페이지 이동 등으로 라우팅이 발생할 때마다 생성되며, 현재 활성화된 라우트의 상태를 저장한 객체이다. 
+ 즉, 현재의 경로 및 URL 파라미터 등의 정보를 이 객체에서 받을 수 있다. 
+ 컴포넌트 내부에 구현된 Router 훅 함수 등을 통해서 참조할 수 있고, watch에서 모니터링하기도 한다.




