# Private 변수

### JS의 클래스 문법에서 프라이빗 변수는 클래스 내부에서만 접근 가능한 변수를 의미한다.

1. 프라이빗 변수는 클래스 외부에서 직접 접근할 수 없다.
2. 클래스의 메서드를 통해서만 조작할 수 있다.

```js
class MyClass {
  #privateVariable;

  constructor(value) {
    this.#privateVariable = value;
  }

  getPrivateVariable() {
    return this.#privateVariable; // 외부로 리턴해주는 메서드
  }

  setPrivateVariable(newValue) {
    this.#privateVariable = newValue; // 메서드로 값 조작
  }
}

let myObject = new MyClass(42);
console.log(myObject.getPrivateVariable()); // 출력: 42

// 직접 프라이빗 변수에 접근하려고 하면 에러가 발생한다.
console.log(myObject.#privateVariable); // 에러 발생: SyntaxError
```

### 특징

1. 정보 은닉 (Encapsulation)

   - 내부 상태 캡슐화
   - 무단 접근 방지

=> 클래스의 내부 구현을 감추고, 클래스의 메서드를 통해서만 프라이빗 변수에 접근하도록 제한한다.
