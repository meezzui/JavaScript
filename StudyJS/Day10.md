```node
ionViewWillEnter() {
    this.userForm = Object.entries(this.userForm).reduce((a, [k, v]) => {
      a[k] = ''
      return a
 }
```
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
#### Object.entries, reduce를 이용한 방법(ES8이 지원되는 브라우저에서만 가능)
