#### Promise
+ `Promise`λ??π―
  + `Promise`λ μλ°μ€ν¬λ¦½νΈ λΉλκΈ° μ²λ¦¬μ μ¬μ©λλ κ°μ²΄μ΄λ€.
  + μ£Όλ‘ μλ²μμ λ°μμ¨ λ°μ΄ν°λ₯Ό νλ©΄μ νμν  λ μ¬μ©νλ€.
+ μ μ¬μ©ν κΉ??π€
  + μμ μμ λ¬Όκ±΄μ λ§λλλ° μΈμ  λμ€λμ§ μ μ μμ κ²½μ° μλΉμλ κ·Έ λ¬Όκ±΄μ΄ λμλμ§ μ§μμ μΌλ‘ μμ μ λ¬Έμλ₯Ό ν΄μΌ μ μ μλ€.
  + μ΄λ΄λλ μμ μ λ¬Όκ±΄μ΄ λ€ λ§λ€μ΄μ‘μ λ μ°λ½μ λ¬λΌκ³  μ νλ²νΈλ₯Ό λ¨κΈ°κ³  λμ€λ κ²μ΄ κ°μ₯ νΈνκ² μ§??π
  + κ·ΈλΌ μλΉμλ μνμ΄ μλ£ λκΈ° μ μ λ€λ₯Έ κ³³μ κ°λ€ μ¬ μ μλ€.
  + μ΄λ°κ² λ°λ‘ `promise`μ΄λ€.
  + μλ²μ λ°μ΄ν°λ₯Ό μμ²­νμ λ λ°μ΄ν°λ₯Ό λ°κΈ° μ μΈλ° νλ©΄μ λ°μ΄ν°λ₯Ό νμνλ €κ³  νλ©΄ μ€λ₯κ° λ°μνκ±°λ λΉ νλ©΄μ΄ λ¬λ€.
  + μ΄λ¬ν λ¬Έμ λ₯Ό ν΄κ²°νκΈ° μν΄ `promise`λ₯Ό μ¬μ©νλ€.
  + λν κ°μ₯ ν° μ΄μ λββ 
    + μμ°¨μ μΌλ‘ λΉλκΈ° ν¨μλ₯Ό νΈμΆν΄μΌ ν  κ²½μ° μ¬μ©νλ€.
    + λΉλκΈ° μ²λ¦¬λ μμ°¨μ μΌλ‘ μ²λ¦¬νμ§ μλλ€λ νΉμ§μ΄ μλλ° κ²½μ°μ λ°λΌ μ΄κ²μ μμ°¨μ μΌλ‘ μ²λ¦¬ν΄μ£Όμ΄μΌ ν  λκ° μλ€. 
+ `promise` μ¬μ©
  + `const pr = new Promise((resolve, reject) => { })`
  + μ±κ³΅νμ κ²½μ° => `resolve`κ° μ€νλκ³  μ€ν¨νμ κ²½μ° `reject`κ° μ€νλλ€.
#### Promiseμ 3κ°μ§ μν
+ `pending(λκΈ°)` : μ²λ¦¬κ° μλ£λμ§ μμ μν
+ `fulfilled(μ΄ν)` : μ±κ³΅μ μΌλ‘ μ²λ¦¬κ° μλ£λ μν
+ `rejected(κ±°λΆ)` : μ²λ¦¬κ° μ€ν¨λ‘ λλ μν

+ Promise μ²λ¦¬ νλ¦ [μΆμ²] MDN web docs
  
  <img width="600" src="https://user-images.githubusercontent.com/86812098/170814834-dbce91c0-95f7-4d3c-9e8a-f78a77c43148.png">

#### Promise μμ 
+ Promise κ°μ²΄λ 2κ°μ§μ μ½λ°± ν¨μλ₯Ό κ°μ§λ€.
  + `fulfilled` μνμμ μ€νλλ `resolve ν¨μ`
  + `rejected` μνμΌ κ²½μ° μ€νλλ `reject ν¨μ`

```node
var promiseExample = function (param) {

return new Promise(function (resolve, reject) {

  // λΉλκΈ°λ₯Ό νννκΈ° μν΄ setTimeout ν¨μλ₯Ό μ¬μ© 
  window.setTimeout(function () {

    // νλΌλ―Έν°κ° μ°Έμ΄λ©΄, 
    if (param) {

      // ν΄κ²°λ¨ 
      resolve("ν΄κ²° μλ£");
    }

    // νλΌλ―Έν°κ° κ±°μ§μ΄λ©΄, 
    else {

      // μ€ν¨ 
      reject(Error("μ€ν¨!!"));
    }
  }, 3000);
});
};
```
+ λμ€μ promise κ°μ²΄λ₯Ό μμ±νκΈ° μν΄ Promise κ°μ²΄λ₯Ό λ¦¬ν΄νλλ‘ `promiseExample` ν¨μλ‘ κ°μΈκ³  μλ€.
+ promiseλ₯Ό λ³΄λ©΄ μ΅λͺν¨μλ₯Ό λ΄κ³  μκ³  μ΅λͺ ν¨μλ resolveμ rejectλ₯Ό νλΌλ―Έν°λ‘ λ°κ³  μλ€.
+ new Promiseλ‘ Promiseκ° μμ±λλ μ§νλΆν° resolveλ  rejectκ° νΈμΆλκΈ° μ κΉμ§μ μκ°μ pending μνλΌκ³  λ³Ό μ μλ€.
+ μμμ΄ μ μνλμλ€λ©΄ resolve ν¨μκ° νΈμΆλκ³  μ€ν¨νλ€λ©° rejectν¨μκ° νΈμΆλλ€.
+ μ€νλΆ
```node
promiseExample(true)
.then(function (text) {
	// μ±κ³΅μ
	console.log(text);
}, function (error) {
	// μ€ν¨μ 
	console.error(error);
});
```
+ promiseExampleμ νΈμΆνλ©΄ Promise κ°μ²΄κ° λ¦¬ν΄λλ€.
+ Promise κ°μ²΄μλ μ μμ μΌλ‘ λΉλκΈ°μμμ΄ μλ£λμμ λ νΈμΆνλ then μ΄λΌλ APIκ° μ‘΄μ¬νλ€.
+ then APIλ₯Ό νΈμΆν΄μ λΉλκΈ° μμμ΄ μλ£λλ©΄ κ²°κ³Όμ λ°λΌ μ±κ³΅ νΉμ μ€ν¨ λ©μμ§λ₯Ό μ½μμ μ°μ΄μ€λ€.
#### μ¦, λΉλκΈ°ν¨μλ₯Ό λ§λ€μ΄μ μ¬μ©ν΄μΌν  λ νλ‘λ―Έμ€ κ°μ²΄λ₯Ό λ¦¬ν΄νκ² λ§λ€μ΄μ μ¬μ©νλ©΄ μ½λ°± μ§μ₯(μ½λ°± μ€μ²©)μ λ°©μ§ν  μ μκ³  μλ¬μ²λ¦¬λ₯Ό μμνκ² ν  μ μλ€λ μ΄μΌκΈ°λ€βββ

#### catch λ©μλ
+ ν΄λΉ Promise κ° μ€ν¨νμ λμ λμμ μ§μ νλ€.
+ thenκ³Ό catch λ©μλλ μ²΄μΈ ννλ‘ νμ©ν  μ μλ€.
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

  













