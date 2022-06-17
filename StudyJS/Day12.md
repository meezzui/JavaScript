#### Object와 Array의 차이점은❓❓❓
+ `Object`
  + `객체`라고 부른다.
  + 객체는 `키(Key)`와 `값(Value)`으로 이루어진다.✨✨✨
  + 키와 값을 함께 합쳐서 `속성(Property)` 이라고 부른다.
  + 속성값은 어떤 값이든 상관 없다.(속성값은 즉, 키와 값으로 이루어진 것) 그래서 객체나, 함수 역시 들어갈 수 있다.
  + 속성값이 함수인 것을 메소드(method)라고 부른다.
  + 예를들어, `console.log()` 도 `console`이라는 `객체`의 `log메소드`를 호출한 것이다.
  + 배열과 달리 `index`의 개념이 없다❗❗❗
    + `index`가 `length`를 결정하므로, `object.lengt`h 는 `undefined`가 나온다.
+ `Array`
  + `[]`로 감싸서 나타내고, 객체 처럼 안에는 무엇이든 들어갈 수 있다.
  + 배열 안에 들어가있는 것들을 `요소(item)`라고 부른다.
  + 키(key)가 없고, 그냥 값(item) 들만 순서대로 나열되어 있다.✨✨✨


#### 빈 객체를 순회(iteration)할 때 유용하게 사용되는 메서드😀
+ 객체 형식의 자료구조를 변환할 때 유용하게 사용된다.(객체 => 배열)
+ `Object.keys, values, entries`
  + `Object.keys(obj)` – 객체의 키만 담은 배열을 반환
  + `Object.values(obj)` – 객체의 값만 담은 배열을 반환
  + `Object.entries(obj)` – [키, 값] 쌍을 담은 배열을 반환
+ 예시
```node
let user = {
  name: "John",
  age: 30
};

//결과
Object.keys(user) = ["name", "age"]
Object.values(user) = ["John", 30]
Object.entries(user) = [ ["name","John"], ["age",30] ]
```
