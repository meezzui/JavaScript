#### Promise
+ `Promise`란??😯
  + `Promise`는 자바스크립트 비동기 처리에 사용되는 객체이다.
  + 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다.
+ 왜 사용할까??🤔
  + 상점에서 물건을 만드는데 언제 나오는지 알 수 없을 경우 소비자는 그 물건이 나왔는지 지속적으로 상점에 문의를 해야 알 수 있다.
  + 이럴때는 상점에 물건이 다 만들어졌을 때 연락을 달라고 전화번호를 남기고 나오는 것이 가장 편하겠지??😄
  + 그럼 소비자는 상품이 완료 되기 전에 다른 곳을 갔다 올 수 있다.
  + 이런게 바로 `promise`이다.
  + 서버에 데이터를 요청했을 때 데이터를 받기 전인데 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜬다.
  + 이러한 문제를 해결하기 위해 `promise`를 사용한다.
  + 또한 가장 큰 이유는❗❗ 
    + 순차적으로 비동기 함수를 호출해야 할 경우 사용한다.
    + 비동기 처리는 순차적으로 처리하지 않는다는 특징이 있는데 경우에 따라 이것을 순차적으로 처리해주어야 할 때가 있다. 
+ `promise` 사용
  + `const pr = new Promise((resolve, reject) => { })`
  + 성공했을 경우 => `resolve`가 실행되고 실패했을 경우 `reject`가 실행된다.
#### Promise의 3가지 상태
+ `pending(대기)` : 처리가 완료되지 않은 상태
+ `fulfilled(이행)` : 성공적으로 처리가 완료된 상태
+ `rejected(거부)` : 처리가 실패로 끝난 상태

+ Promise 처리 흐름 [출처] MDN web docs
  
  <img width="600" src="https://user-images.githubusercontent.com/86812098/170814834-dbce91c0-95f7-4d3c-9e8a-f78a77c43148.png">

#### Promise 예제
+ Promise 객체는 2가지의 콜백 함수를 가진다.
  + `fulfilled` 상태에서 실행되는 `resolve 함수`
  + `rejected` 상태일 경우 실행되는 `reject 함수`

```node
var promiseExample = function (param) {

return new Promise(function (resolve, reject) {

  // 비동기를 표현하기 위해 setTimeout 함수를 사용 
  window.setTimeout(function () {

    // 파라미터가 참이면, 
    if (param) {

      // 해결됨 
      resolve("해결 완료");
    }

    // 파라미터가 거짓이면, 
    else {

      // 실패 
      reject(Error("실패!!"));
    }
  }, 3000);
});
};
```
+ 나중에 promise 객체를 생성하기 위해 Promise 객체를 리턴하도록 `promiseExample` 함수로 감싸고 있다.
+ promise를 보면 익명함수를 담고 있고 익명 함수는 resolve와 reject를 파라미터로 받고 있다.
+ new Promise로 Promise가 생성되는 직후부터 resolve나  reject가 호출되기 전까지의 순간을 pending 상태라고 볼 수 있다.
+ 작업이 잘 수행되었다면 resolve 함수가 호출되고 실패했다며 reject함수가 호출된다.
+ 실행부
```node
promiseExample(true)
.then(function (text) {
	// 성공시
	console.log(text);
}, function (error) {
	// 실패시 
	console.error(error);
});
```
+ promiseExample을 호출하면 Promise 객체가 리턴된다.
+ Promise 객체에는 정상적으로 비동기작업이 완료되었을 때 호출하는 then 이라는 API가 존재한다.
+ then API를 호출해서 비동기 작업이 완료되면 결과에 따라 성공 혹은 실패 메시지를 콘솔에 찍어준다.
#### 즉, 비동기함수를 만들어서 사용해야할 때 프로미스 객체를 리턴하게 만들어서 사용하면 콜백 지옥(콜백 중첩)을 방지할 수 있고 에러처리를 수월하게 할 수 있다는 이야기다❗❗❗

#### catch 메소드
+ 해당 Promise 가 실패했을 때의 동작을 지정한다.
+ then과 catch 메소드는 체인 형태로 활용할 수 있다.
```node
const promise1 = new Promise((resolve, reject) => {
resolve();
});
promise1
.then(() => {
  console.log("then!");
})
.catch(() => {
  console.log("catch!");
});
```

  













