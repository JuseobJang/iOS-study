# Methods

Methods는 특정한 타입과 관련된 함수이다. Class, Structure 및 Enumeration은 모두 인스턴스 메서드를 정의 할 수 있으며, 메서드는 지정된 유형의 인스턴스로 작업하기 위하 특정 작업 및 기능을 캡슐화 할 수 있다. Class, Structure 및 Enumeration는 타입 자체와 연관된 타입 메서드를 정의 할 수 있다.

## Instance Methods

```swift
class Counter {
  var count = 0
  func increment() { // instance method 1
    count += 1
  }
  func increment(by amount: Int) { // instance method 2
    count += amount
  }
  func reset() { // instance method 3
    count = 0
  }
}

let counter = Counter() // instance 생성, count = 0
counter.increment() // count = 1
counter.increment(by: 5) // count = 6
counter.reset() // count = 0
```



### The self Property

모든 인스턴스에는 인스턴스 자체와 동일한 `self`라는 암시적 속성이 존재한다. Self Property를 사용하여 인스턴스 메서드 내에서 현재 인스턴스를 참조 할 수 있다.

```swift
func increment() {
    self.count += 1 // self property 사용
}
```

실제로 코드에서 `self`를 자주 사용할 필요는 없다 명시적으로 `self`를 사용하는 것을 명시하지 않으면 Swift 는 현재 인스턴스의 속성이나 메서드를 참조한다고 가정한다. 하지만 인스턴스 메서드 매개변수 이름이 인스턴스 속성 이름과 같은 경우 예외가 발생한다. 이러한 경우 매개 변수 이름을 우선으로 하기 때문에 인스턴스 속성을 사용하기 위해서는 `self`를 명시하여야 한다.

```swift
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOf(x: Double) -> Bool {
        return self.x > x // 인스턴스 속성 x와 매개변수 x가 이름이 같기 때문에 self를 사용하여 인스턴스의 속성임을 명시
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOf(x: 1.0) {
    print("This point is to the right of the line where x == 1.0")
}
```



### Modifying Value Types from Within Instance Methods

Structure와 Enumerationsms 는 Value Types이다. 일반적으로 Value Type의 속성은 인스턴스 메서드 내에서 수정될 수 없다.

하지만 특정 메서드 내에서 structure 또는 enumeration의 속성을 수정해야 하는 경우 해당 메서드에 대한 `mutating` 동작을 선택할 수 있다. 이렇게 하면 메서드 내에서 속성을 변경 할 수 있으며 메서드가 종료되면 변경 내용이 기록 된다.

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) { // mutating 속성 추가
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// Prints "The point is now at (3.0, 4.0)"
```



### Assigning to Self Within a Mutating Method

메서드는 암시적 `self` 속성에 완전히 새로운 인스턴스를 할당할 수도 있으며, 메서드가 종료되면 새로운 인스터스가 기존 인스턴스를 대체한다.

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY) // 인스턴스 자체를 새로운 인스턴스로 대체한다.
    }
}
```



## Type Methods

타입 자체에서 호출 되는 메서드를 정의 할 수 있다. 이러한 종류의 메서드를 Type Method라고 한다. 메서드의 `func` 키워드 앞에 `static` 키워드를 작성하여 메서드를 나타낸다. Class 는 `static` 대신 `class` 키워드를 사용하여 하위 클래스가 해당 메서드의 구현을 재정의 할 수 있다.

```swift
class SomeClass {
    class func someTypeMethod() {
        // type method implementation goes here
    }
}
SomeClass.someTypeMethod()
```



















