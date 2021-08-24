# Inheritance

클래스는 다른 클래스에서 메서드, 속성 그리고 다른 특성들을 상속할 수 있다. 클래스가 다른 클래스로 부터 상속될 떄 상속하는 클래스를 하위 클래스(subclass), 상속된 클래스를 상위 클래스(superclass) 라고 한다. 상속은 Swift에서 다른 타입과 클래스를 구분하는 기본동작이다.

Swift에서 클래스는 상위클래스에 속하는 메서드, 속성 그리고 서브 스크립트를 호출 및 접근 할 수 있으며 각각의 동작을 재정의(override) 할 수 있다.

클래스는 프로퍼티의 값이 변경될 때 알려주기 위해서 상속된 속성에 속성 관찰자를 추가 할수도 있다. 속성 관찰자는 기존 속성이 저장된 속성(stored property) 또는 계산된 속성(computed property)인지 상관없이 추가될 수 있다.

## Defining a Base Class

다른 클래스에서 상속하지 않은 클래스를 기본 클래스(base class) 라고 한다.

```swift
class Vehicle {
  var currentSpeed = 0.0
  var description: String {
    return "traveling at \(currentSpeed) miles per hour"
  }
  
  // 현재 클래스에서는 아무 동작도 하지 않지만 하위 클래스에서 필요하다면 사용할 수 있다. 
  func makeNoise() {
    // nothing
  }
}
```

```swift
// 새로운 인스턴스 생성
let someVehicle = Vehicle()

print("Vehicle: \(someVehicle.description)")
// Vehicle: traveling at 0.0 miles per hour
```

`Vehicle` 클래스는 임의의 탈 것에 대한 공통 특성을 정의하지만, 그 자체로는 일반적으로 많이 사용되지 않는다. 더 유용하게 사용하기 위해 더 구체적인 탈 것 종류를 설명하기 위한 수정이 필요하다.

## Subclassing

하위클래스(Subclassing) 는 기존 클래스를 기반으로 새로운 클래스를 만드는 작업이다. 하위클래스는 기존 클래스 특성을 상속하고 수정할 수 있다. 물론 새로운 특성을 추가 할 수도 있다.

하위클래스가 상위클래스를 상속한다는 것을 나타내기 위해 `:` 콜론을 사용하여 작성한다.

`Bicycle` 클래스는 기본적으로 `Vehicle` 클래스의  `currentSpeed`, `description` 속성과 `makeNoise()` 메서드를 자동적으로 갖게 된다.

상속한 특성외에도 `hasBasket` 이라는 새로운 속성을 갖는다.

```swift
class Bicycle: Vehicle {
  var hasBasket = false
}

bicycle.currentSpeed = 15.0
print("Bicycle: \(bicycle.description)")
// Bicycle: traveling at 15.0 miles per hour
```

`Tandem` 은 `Bicycle` 의 모든 속성과 메서드를 상속하고 또한 `Vehicle` 의 모든 속성과 메서드를 상속한다. 또한 `currentNumberOfPassengers` 라는 새로운 속성을 갖는다. 

```swift
class Tandem: Bicycle {
  var currentNumberOfPassengers = 0
}

let tandem = Tandem()
tandem.hasBasket = true
tandem.currentNumberOfPassengers = 2
tandem.currentSpeed = 22.0
print("Tandem: \(tandem.description)")
// Tandem: traveling at 22.0 miles per hour
```



## Overriding

하위 클래스는 상위클래스에서 상속할 여러 특성들을 하위 클래스에서 자체적으로 구현할 수 있다. 이것을 재정의(overriding) 이라 한다.

상속될 특성을 재정의 하려면 재정의 할 정의 앞에 `override` 키워드를 추가한다. 

### Accessing Superclass Methods, Properties, and Subscripts

하위클래스에는 메서드, 속성, 서브스크립트 재정의를 제공할 때 재정의 일부로 상위 클래스 구현을 사용하는 것이 유용할 때가 있다. 예를 들어 기존 구현의 동작을 구체화 하거나 기존 상속된 변수에 수정된 값을 저장 할 수 있다.

이것이 적절한 경우 `super` 접두어를 사용하여 상위 클래서의 기본 메서드, 속성, 또는 서브스크립트 버전에 접근한다.

- someMethod() -> super.someMethod()
- someProperty -> getter, setter 내에서 super.someProperty
- someIndex -> super[someIndex] (서브스크립트)

### Overriding Methods

상속된 인스턴스 또는 타입 메서드를 재정의 하여 하위 클래스 내에서 메서드의 맞춤형 또는 대체 구현을 제공한다.

```swift
class Train: Vehicle {
  override func makeNoise() {
    print("Choo Choo")
  }
}
let train = Train()
train.makeNoise()
// Prints "Choo Choo"
```

### Overriding Properties

속성에 고유한 사용자 정의 getter와 setter를 제공하거나 기본 속성 값이 변경 될 때 재정의 한 속성이 관찰할 수 있도록 속성 관찰자를 추가 하기위해 상속된 인스턴스 또는 타입 프로퍼티를 재정의 할 수 있다.

#### Overriding Property Getters and Setters

상속된 속성이 소스에서 stored & computed property 로 구현되었는지 여부와 상관 없이 모든 상속된 속성을 재정의 하기 위해 사용자 지정 getter 와 setter를 제공할 수 있다. 상속된 속성이 stored인지 computed 인지는 하위클래스에서 알 수 없다. 단지 상속된 속성의 이름과 타입만 알고 있다. 

하위 클래스에서 getter와 setter를 통해

- (상위) read-only -> (하위) read-write 가능하다.
- (상위) read-write -> (하위) read-only 불가능하다.

```swift
class Car: Vehicle {
  var gear = 1
  // 속성 재정의
  override var description: String {
    // 상위 클래스 속성을 가져와서 사용
    return super.description + " in gear \(gear)"
  }
}
```

```swift
let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")
// Car: traveling at 25.0 miles per hour in gear 3
```

#### Overriding Property Obsevers

상속된 속성에 속성 관찰자를 추가하기 위해 속성을 재정의 할 수 있다. 이것은 기존에 구현된 속성이 어떻든 상관없이 속성의 값이 변경될 때 알림을 받을 수 있다. 

```swift
class AutomaticCar: Car {
  override var currentSpeed: Double {
    // 현재 차속도에 기반하여 자동으로 기어를 설정
    didSet {
      gear = Int(currentSpeed / 10.0) + 1
    }
  }
}
```

```swift
let automatic = AutomaticCar()
automatic.currentSpeed = 35.0
print("AutomaticCar: \(automatic.description)")
// AutomaticCar: traveling at 35.0 miles per hour in gear 4
```



## Prventing Overrides

final 표시를 사용하여 실수로 메서드, 속성 또는 서브스크립트를 재정의 하는 것을 방지 할 수 있다. `final var`, `final func`, `final class func`, `final subscript` 와 같은방법으로 작성한다.

하위 클래스에서 final 메서드, 속성 또는 서브스크립트를 재정의 하면 컴파일 시 에러가 발생한다. Extension Class 에서 추가된 메서드, 속성 또는 서브스크립트 또한 final을 사용할 수 있다.

클래스를 정의하느 `class` 키워드 이전에 `final` 키워드를 표시하여 클래스의 상속 자체를 목하도록 막들 수도 있다.









