#### Object.entries()란??🧐
+ 객체를 배열로 만들어 준다.
+ 객체의 키와 값을 `[key, value]`의 배열로 반환한다.(객체가 배열로 바뀜에 따라 key와 value는 순서성을 가지게 됨)
+ 사용법 및 결과
  + `Object.entries`를 사용하면 객체가 2차원 배열이 된다. 따라서 key와 value가 순서성을 가지게 된다. 
  ```node
  const object1 = {
     a: 'apple',
     b: 'banana',
     c: 'cocoa'
    }
  let objToArr = Object.entries(object1);
  console.log(objToArr)
  
  // 결과
  0 : ["a", "apple"]
  1 : ["b", "banana"]
  2 : ["c", "cocoa"]
  ```
#### Object.entries, reduce를 이용한 방법(ES8이 지원되는 브라우저에서만 가능)😲
```node
ionViewWillEnter() {
    this.userForm = Object.entries(this.userForm).reduce((a, [k, v]) => {
      a[k] = ''
      return a
 }
```
+ reduce() 함수는 배열의 각 요소를 순회하며 `a`의 함수의 실행값을 누적하여 하나의 결과값으로 나타낸다.
+ 즉, useForm을 배열의 형태로 바꾸고 그 배열을 다 돌면서 하나의 결과값(return a 의 값)으로 나타낸다.  
