# Static Method

[➡️ 블로그 포스팅](https://euncoding.tistory.com/49)

static method(정적 메소드)란 생성자의 프로토타입 속성에 할당되어있지 않고 클래스 자체에 직접 할당되어있는 메소드이다.

정적 메소드를 만드는 방법은 다음과 같다.

1. 클래스로 생성자를 구현할 때 정적 메소드를 정의하는 방법

```jsx
class Person () {
  static staticMethod() {
    return this === User;
  }
}

Person.staticMethod(); //true
```

2. 생성자 함수로 생성자를 구현할 때 정적 메소드를 정의하는 방법

```jsx
function Person() {}

Person.staticMethod = function () {
  return this === User;
}

Person.staticMethod(); //true
```

- 정적 메소드는 클래스(Person) 자체에서만 접근이 가능하다.

- new키워드를 이용해 인스턴스를 생성하는 부분과는 무관하다. 클래스 자체에서 직접적으로 접근할 때에만 의미가 있다.

### static메소드를 언제, 왜 사용할까?

정적 메소드는 특정한 인스턴스가 아닌 클래스에 속한 함수를 구현하고자 할 때 주로 사용된다.

즉 여러 인스턴스들 간의 관계를 이용해 어떤 기능을 수행하거나, 주어진 인자에 대해 소속 여부 확인, 소속 부여 등 "전체"적인 관점에서 어떤 동작을 정의하는 메소드를 만드는 데 사용된다.

- Array.isArray() : 이 메소드는 판별하고자 하는 대상의 데이터타입이 array인지를 판단하는 메소드이다. 자기자신(인스턴스)의 데이터타입이 배열이 맞는지를 판단하는 메소드가 자기자신(인스턴스) 내에 속해있는 것은 적절하지 않다. 따라서 이 메소드는 static메소드로 구현되어야 한다.

- Array.from() : 이 메소드는 다른 자료구조를 배열로 바꾸는 역할을 한다. 즉 Array생성자로 만들어지지 않은 다른 객체를 배열로 만들어주는 메소드 또한 인스턴스 내에 속해있는 것은 적절하지 않다.
