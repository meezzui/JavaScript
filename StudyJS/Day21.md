#### 빈 모달창 뜨는 이슈 해결✔
+ 아이디찾기 모달창에서 인증코드 인증을하고 그 다음단계도 모달창을 띄우는데 다음단계 페이지가 뜨다가 갑자기 빈 모달창이 뜨는 현상이 발생했다.
+ 처음엔 팝업창에 값이 제대로 전달되지 않아서 그런가...??하는 생각에 console로 찍어봤지만 값은 잘 들어오고 있었다.
+ 그럼 문제가 뭘까...❓❓😤
  + 확인 버튼을 누르면 다음 단계로 이동하게 되는데 그때 꺼지는 동작과 그 다음단계의 팝업을 띄우는 동작이 동시에 일어났기 때문이다.
  ```node
  // 모달창을 띄울 때 props로 넘겨주는 값 중 확인버튼을 눌렀을 경우 기존의 창이 꺼지고 새로운 팝업창이 열리는 기능
  confirm: (membId, mdaGbn) => {
     modal.dismiss() // 모달창 닫힘
    this.showFindId(membId, mdaGbn) // 다음단계 모달창 열림
  }
  ```
+ 해결방법은❓❓
  + `await`를 사용하는 것이다❗❗(`await`를 사용하려면 `async`를 써주어야 함😉)
  + `await`를 사용하여 함수가 순차적으로 동작하게 해주었다.✨✨✨
  ```node
  confirm: async(membId, mdaGbn) => {
    await modal.dismiss()
    await this.showFindId(membId, mdaGbn)
  }
  ```
  
#### 모달창 띄우는 예시
+ `const modal = await modalController` `vue`의 `modalController` 라이브러리 사용
+ 모달로 띄울 페이지를 `import`하여 `import`시켜준 이름을 `comp: findAccount` 이렇게 적어준다.
+ `class:`이 부분은 해당 모달창에 적용되는 css 클래스 이름이다. 이름을 같이 `props`로 넘겨주면 해당 모달창의 크기를 적용할 수 있다.
  + 해당 페이지에서는 모달창의 크기를 커스텀할 수 없다.(css가 안 먹힘) 
  + 그래서 전역으로 지정해주어야 하기 때문에 `props`로 같이 넘겨준다.
```node
/*
  pc에서 모달로 띄우기
*/
async openModal(flag) {
  const components = {
    id: { title: this.$t('findid'), comp: findAccount, class: 'find-id1-h' },
    pwd: { title: this.$t('findpwd'), comp: checkUserinfo, class: 'find-pwd1-h' },
    pwdReset: { title: this.$t('findpwd'), comp: findPwd, class: 'find-pwd1-h' }
  }
  const modal = await modalController
    .create({
      component: components[flag].comp,
      cssClass: ['pc-modal-findId', components[flag].class],
      componentProps: {
        popTitle: components[flag].title,
        token: this.pwdInitToken,
        close: () => {
          await modal.dismiss()
        },
        confirm: async(membId, mdaGbn) => {
          await modal.dismiss()
          await this.showFindId(membId, mdaGbn)
        }
      }
    })
  return modal.present()
}
```
#### 참고📢 모바일에서 페이지 이동된 것을 pc 모달창으로 띄우기
+ 모바일에서는 페이지를 이동하기 때문에 `router`를 써서 `path`의 `name`이나 `query`,`params`로 넘긴다.
+ 이러한 것을 pc에서 모달창으로 띄울 때 `props`로 값을 넘겨준다. 이때 이 해당하는 `query`나 `params`를 같이 넘겨주면 된다. 
+ 또한 필수적으로 넘겨주어야 하는 값들을 같이 넘겨주어야 모달창이 잘 뜬다.
+ 단, `ionic` 프레임워크는 모바일에서는 `ionViewWillEnter()` 함수를 타지만 pc는 이 함수를 타지 않는다.
  + `ionViewWillEnter()`란❓❓ 
    + 해당 페이지에 진입했을 경우 화면이 그려진다.
+ 이러한 이유 때문에 `created()` 함수에 한번 더 `methods`에 선언해주었던 함수들을 다시 한번 선언해서 그려줘야 한다.
+ 여기서 주의할 점❗❗ 
  + `created()` 함수는 pc와 mobile일 때 두번 다 타기 때문에 반드시 `if문`을 걸어주어 pc일 경우에만 타게 조건을 주어야 한다.
  + 그렇지 않으면 함수가 두번 호출되게 된다.
