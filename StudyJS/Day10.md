```node
ionViewWillEnter() {
    this.userForm = Object.entries(this.userForm).reduce((a, [k, v]) => {
      a[k] = ''
      return a
 }
```
#### Object.entries()란??🧐
+ object에 직접있는 enumerable 속성 [key, value] 쌍에 해당하는 배열을 반환한다. 
+ 속성의 순서는 개체의 속성 값을 수동으로 반복하여 주어진 순서와 동일하다.
+ 사용법
 
 
