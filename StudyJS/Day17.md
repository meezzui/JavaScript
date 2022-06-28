#### `EventEmitter`란❓❓
+ 이벤트를 내보내는 모든 객체는 `EventEmitter` 클래스의 인스턴스이다.
+ `EventEmitter`의 인스턴스는 `EventEmitter` 인스턴스 자체 내에서 이벤트와 연결된 모든 이벤트와 리스너를 추적한다.

#### 관련 메소드
+ `this.emitter.emit()`: 이벤트를 보낼 때 사용한다.
  + 중요🎇 `this.emitter.emit()`과 `this.$emit()` 다른점은 무엇일까❓❓
    + `this.$emit()` : 자식 컴포넌트에서 부모 컴포넌트로 이벤트를 전달할 때 사용한다. 이벤트를 전달함으로써 부모 컴포넌트는 자식 컴포넌트에서 전달받은 값을 사용할 수 있다.
    + `this.emitter.emit()` : 자식과 부모관계에 상관없이 이벤트를 전달할 수 있다.

+ `this.emitter.on()`
  + 이벤트를 생성해주는 메소드로 `this.emitter.emit()`를 사용하기 위해선 `this.emitter.on()`으로 등록을 해주어야 한다.
  + 즉, 특정 상황에 실행시킬 리스너 함수를 `Emitter` 안에 등록한다는 의미를 갖고 있다. 
