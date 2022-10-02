#### append()와 appendChild() 공통점
+ `append()`와 `appendChild()`는 모두 부모 노드에 자식 노드를 추가하는 메서드이다.


#### append()와 appendChild() 차이✨
+ `append()`
  +  여러 개의 노드와 문자를 추가 할 수 있다.
  ```node
  const div = document.createElement('div');
  const span = document.createElement('span');
  const p = document.createElement('p');

  document.body.append(div, 'hello', span, p);

  // result
  <body>
    <div></div>
    hello
    <span></span>
    <p></p>
  </body>
  ```
+ `appendChild()`
  + 오직 Node 객체만 받을 수 있다.
  ```node
  // Node object 삽입
  const parent = document.createElement('div');
  const child = document.createElement('p');
  parent.appendChild(child);

  // <div><p></p></div>
  ```
  + 한번에 오직 하나의 노드만 추가 할 수 있다.
