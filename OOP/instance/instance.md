# 클래스 인스턴스 생성 과정

```js
Class Square {
  // 생성자
  constructor(width, height) {
    // 1. 암묵적으로 인스턴스 생성되고 this에 바인딩.
    console.log(this); // Person {}
    console.log(Object.getPrototypeOf(this) === Person.prototype); // true

    // 2. this에 바인딩되어 있는 인스턴스 초기화.
    this.width = width;
    this.height = height;

    // 3. 완성된 "인스턴스가 바인딩된 this"가 암묵적으로 반환.
  }
}

```
