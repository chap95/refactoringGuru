# Factory Method pattern

부모 클래스에서 객체들을 생성할 수 있는 인터페이스를 제공하지만, 자식 클래스들이 생성될 객체들의 유형을 변경할 수 있도록 하는 생성패턴이다.

이 패턴은 코드 확장성과 관련있다. 예를 들어서 물류 관리 시스템을 만든다고 가정해보자. 처음에는 `Truck` 에 대한 물류만 처리했기에 `Truck` 클래스에 모든 로직을 구현해 놓았다. 하지만 서비스가 유명해지면서 또 다른 운송수단에 대한 확장이 필요해진 상황이 발생했다. `Truck` 클래스에 모든 로직이 붙어있기 때문에 새로운 운송수단 클래스를 추가하기에는 코드 베이스를 변경해야한다.

이 때 팩토리 메소드 패턴을 사용하면 된다. 해당 패턴은 객체 생성 직접 호출들을 특별한 팩토리 메소드에 대한 호출들로 대체하는 것을 제안한다.

아래는 예제에 대한 의사코드이다.

```ts
class Logistics {
  //... some code here
  constructor() {
    // ... some code here
  }

  planDelivery() {}

  createTransport(): Transport<T> {}
}

class Truck extends Logistics {
  constructor() {}

  // ... some code here

  planDelivery() {}

  createTransport(): Transport<Truck> {
    return new Truck();
  }
}

class Ship extends Logistics {
  constructor() {}

  // ... some code here
  planDelivery() {}

  createTransport(): Transport<Ship> {
    return new Ship();
  }
}
```

`Truck`과 `Ship` 은 `createTransport` 를 오버라이드 하지만 `return` 타입은 각기 다르며 `planDelivery` 라는 메소드를 공통으로 가지고 있지만 세부구현은 다를 수 있다. `Truck`은 상자에 담아 육로로 배송을 진행한다고 하면 `Ship` 은 컨테이너에 담아서 해상으로 배송을 진행한다는 차이점이 `planDelivery` 세부 구현으로 표현이 가능하다.
