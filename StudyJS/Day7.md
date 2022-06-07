#### validation 체크 문구 띄우기
+ 다음 페이지로 넘어갈 때 해당 형식에 맞게 정보가 작성되었는지 확인 후 페이지가 넘어감
+ 형식에 맞지 않게 작성되었을 시 알림창이 뜬다.
```node
<template>
<div>
  <BottomButton :single="$t('check')" :isValid="userForm.membId && userForm.membEml" @click-single="checkUserInfo"/>
</div>
</template>

data() {
  return {
    userForm: {
      membId: '',
      membEml: ''
    }
  }
},
methods: {
  /**
   * 유저정보 체크
   */
  checkUserInfo() {
    // 아이디 미입력시
    if (this.userForm.membId === '') {
      this.$alert({
        title: this.$t('enterId'),
        single: this.$t('check')
      })
      return
    }

    // 아이디 형식 체크
    if (!checkId(this.userForm.membId)) {
      this.$alert({
        title: this.$t('idFormCheck'),
        single: this.$t('check')
      })
      return
    }

    // 이메일 미입력시
    if (this.userForm.membEml === '') {
      this.$alert({
        title: this.$t('enterEmail'),
        single: this.$t('check')
      })
      return
    }

    initPwd(this.userForm).then(res => {
      this.$alert({
        title: this.$t('pwdInit'),
        single: this.$t('confirm'),
        success: () => {
          if (this.device === 'PC') {
            this.$router.go()
          } else {
            this.$router.push({ name: 'Login' })
          }
        }
      })
    }).catch(e => {
      console.error(e)
      this.$alert({
        title: e.data.errorMessage,
        single: this.$t('check')
      })
    })
  },
  reloadPage(route) {

  }
}
```
+ `<BottomButton :single="$t('check')" :isValid="userForm.membId && userForm.membEml" @click-single="checkUserInfo"/>`
  + `:isValid="userForm.membId && userForm.membEml"`: 정보를 적는 란에 모두 작성이 되어야 버튼이 활성화된다.
  + `@click-single="checkUserInfo"`: 이 버튼을 클릭시 `checkUserInfo`라는 함수가 실행된다.
```node
if (this.userForm.membId === '') {
  this.$alert({
    title: this.$t('enterId'),
    single: this.$t('check')
  })
  return
}
```
+ 이런식으로 `data()`에 선언해준 것(api)을 가지고 빈 값일 경우 alert창이 뜨게 한다.
+ 중요❗❗❗
  + 각 `if문`에 `return`을 꼭 해줘야 한다. 그래야 `if문`을 탈 경우 그 이후의 코드가 읽히지 않아 버튼이 막힌다(즉, 페이지가 넘어가지 않는다.) 
































