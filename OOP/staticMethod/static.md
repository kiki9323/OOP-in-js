# 정적(static) 메서드

## 정적(static) 메서드란?

정적 메서드는 **클래스의 인스턴스를 생성하지 않고도** *직접 클래스 이름을 통해 호출할 수 있는 메서드*이다.
이 메서드들은 클래스의 **인스턴스와 상관없이 동작**하며, 클래스 자체에 관련된 작업을 처리할 때 사용된다.

## 활용

클래스의 인스턴스 생성 없이 바로 사용가능하다.
이는 해당 메서드가 클래스와 관련된 일반적인 기능을 수행하며, 특정 인스턴스의 상태에 의존하지 않기 떄문이다.
따라서 클래스의 메서드들은 객체지향 프로그래밍의 개념을 사용하되, 인스턴스를 생성하지 않아도 각 메서드를 독립적으로 사용할 수 있다.

## 예시

```js
// class/Person.js
class Person {
  constructor(name) {
    this.name = name;
  }

  // 정적 메서드
  // : method 앞에 static을 붙여준다.
  static sayHi() {
    console.log('인스턴스 없이 바로 호출 가능!');
  }
}

export default Person;
```

## 호출 방법

**인스턴스 없이** class로 호출한다.

```js
// index.js
Person.sayHi(); // 인스턴스 없이 바로 호출 가능!
```

인스턴스로 호출하면 `TypeError` 발생

```js
// index.js
const me = new Person('noodle');
me.sayHi(); // TypeError: me.sayHi is not a function
```

## 정리

정적 메서드는 클래스에 바인딩된 메서드가 된다.  
클래스는 **클래스 정의가 평가되는 시점**에 **함수 객체**가 되므로 인스턴스와 달리 **별다른 생성과정이 필요가 없어진다.**

## static method vs prototype method

<table style="text-align: center">
  <tr>
    <th>static method </th>
    <th>prototype method</th>
  </tr>
  <tr>
    <td colspan="2">자신이 속해 있는 프로토타입 체인이 다르다</td>
  </tr>
  <tr>
    <td>인스턴스 프로퍼티를 참조할 수 없다.</td>
    <td>인스턴스 프로퍼티를 참조할 수 있다.</td>
  </tr>
  <tr>
    <td>클래스로 호출 (= 클래스 binding)  <br /> this <span style="font-weight:900">사용하지 않을 땐</span> 정적 메서드로 정의 </td>
    <td>인스턴스로 호출 (= 인스턴스 객체 binding)  <br /> </td>
  </tr>
  <tr>
    <td>유틸리티 함수를 제공하거나, <br /> 클래스와 관련이 있는 특정 계산을 수행하는 메서드 정의시 사용</td>
    <td>인스턴스 프로퍼티를 참조하여 상태를 조작하거나 <br /> 인스턴스와 관련된 행동을 정의할 때 쓴다.</td>
  </tr>
</table>

### 언제 정적 메서드와 프로포타입 메서드를 사용하나요?

```js
Class Square {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  // 프로토타입 메서드 : 인스턴스 프로퍼티를 참조해야 한다면 프로토타입 메서드를 사용.
  area() {
    return this.width * this.height;
  }

  // 정적 메서드 : 인스턴스 프로퍼티를 참조하지 않는 경우 사용한다.
  static hi() {
    console.log('안녕 I am 스퀘어예요.');
  }
}

// 정적 메서드 호출
// : Class에 바인딩 됨을 알 수 있다.
Square.hi(); // 안녕 I am 스퀘어예요.

// 프로토타입 메서드 사용을 위해 인스턴스 생성
// : 인스턴스에 바인딩 됨을 알 수 있다.
const squareInstance = new Square();

// 프로토타입 메서드 호출
const squareArea = squareInstance(10, 10);
console.log(squareArea); // 100

```

**자주 사용하는 표준 빌트인 정적 메서드**

```js
Math.max(1, 2, 3); // 3
Number.isNaN(NaN); // true
JSON.stringify({ a: 1 }); // {'a': 1}
Object.is({}, {}); // false
Reflect.has({ a: 1 }, 'a'); // true
```

이처럼 클래스 또는 생성자 함수를 하나의 네임스페이스로 사용하여 정적 메서드를 모아 놓으면 이름 충돌 가능성을 줄이고 관련 함수들을 구조화할 수 있다.
애플리케이션 전역에서 사용할 유틸리티 함수를 전역 함수로 정의하지 않고 메서드를 구조화한다.

<br />
<br />
<br />

**예시) 생성자 함수의 경우 정적 메서드 생성**

```js
// 생성자 함수
function Person(name) {
  this.name = name;
}

// 정적 메서드
Person.sayHi = function () {
  console.log('생성자 함수의 정적 메서드 추가');
};

// 정적 메서드 호출
Person.sayHi();
```
