# Proterties

Properties는 class, structure 또는 enumeration 과 연관이 있다. Stored Properties는 인스턴스에 상수 또는 변수에 저장된다. 반면에 Computed Properties는 값을 계산한다(저장 되지는 않음). Computed Propertiessms class, structure 그리고 enumeration에서 제공 되고 Stored properties는 오직 class 와 structure에서만 제공된다.

Stored 및 Computed properties는 보통 특정 타입의 인스턴스와 연결되지만 타입 그 자체와도 연결 될 수 있다. 이러한 properties를 type properties라고 한다.

또한 property의 변화를 모니터링하기 위한 property observers 정의하여 사용자가 정의하는 커스텀 액션으로 처리 할 수 있다. Property Observer는 stored property에 추가 할 수 있고 superclass를 상속한 subclass의 속성에도 추가 할 수 있다.

또한 Property wrapper를 사용하여 여러 속성의 getter 와 setter내의 코드를 재사용할 수 있다.



## Stored Properties

```swift
// 가장 간단한 형태의 속성
struct FixedLengthRange {
  var firstValue: Int 
  let length: Int
}
var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
// the range represents integer values 0, 1, and 2
rangeOfThreeItems.firstValue = 6
// the range now represents integer values 6, 7, and 8
```



### Stored Properties of Constant Structure Instances

```swift
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
// 비록 firstValue가 var 이여도 인스턴스 자체가 let으로 선언 했기 때문에 속성을 변경 할 수 없다.
rangeOfFourItems.firstValue = 6 // error
```



### Lazy Stored Properties

Lazy Properties는 처음 사용될 때 까지 초기 값이 계산 되어지지 않는 속성이다. Lazy Properties은 초기값이 인스턴스의 초기화가 완료 되기 전까지 값을 알 수 없는 외부 요인에 종속된 경우 또는 초기값이 필요 없거나 필요할 때까지 수행해서는 안되는 복잡하거나 계산적으로 비용이 많이 드는 설정을 할 때 유용하다.

```swift
class DataImporter {
  var filename = "data.txt"
}

class DataManager {
  lazy var importer = DataImporter()
  var data: [String] = []
}

// DataManager의 인스턴스 manager의 importer는 아직 생성되지 않음.
let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")

// importer를 사용하는 이 순간에 생성 됨.
print(manager.importer.filename)
```



## Computed Properties

Stored properties 뿐만 아니라 classes, structures 그리고 enumerationssms Computed Properties를 정의 할 수있다. Computed Properties는 실제로 값이 저장되는 것은 아니지만 다른 속성 및 값을 간접적으로 검색하고 선택 할 수 있도록 필요에 따라서 getter와 setter을 제공한다.

```swift
struct Point {
  var x = 0.0, y = 0.0
}
struct Size {
  var width = 0.0, height = 0.0
}
struct Rect {
  var origin = Point()
  var size = Size()

  // Computed Properties
  var center: Point {
    get { // 해당 계산으로 center 속성을 반환한다.
      let centerX = origin.x + (size.width / 2)
      let centerY = origin.y + (size.height / 2)
      return Point(x: centerX, y: centerY)
    }
    set(newCenter) { // 새로운 center속성을 통해 관련된 origin의 속성을 바꿀 수 있다.
      origin.x = newCenter.x - (size.width / 2)
      origin.y = newCenter.y - (size.height / 2)
    }
  }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
                  size: Size(width: 10.0, height: 10.0))

let initialSquareCenter = square.center // Point(x: 5.0, y: 5.0)
square.center = Point(x: 15.0, y: 15.0) // set()에 의하여 center값 변경
print("square.origin is now at (\(square.origin.x), \(square.origin.y))") // Point(x: 10.0, y: 10.0)
```



### Shorthand Setter Declaration

```swift
// 만약 새로운 값의 이름을 따로 설정하지 않는다면 default로 newValue로 표현 할 수 있다.
set {
  origin.x = newValue.x - (size.width / 2) 
  origin.y = newValue.y - (size.height / 2)
}
```



### Shorthand Getter Declataion

```swift
// getter의 코드가 한줄로 표현이 가능 하다면 return이 생략 가능하다.
get {
  Point(x: origin.x + (size.width / 2),
        y: origin.y + (size.height / 2))
}
```



### Read-Only Computed Properties

getter은 있지만 setter이 없는 Computed Properties를 Read-Only Computed Properties라고 한다. 해당 값은 값에 접근해 값을 반환하는것은 가능하지만 다른 값으로 설정 할 순 없다. 또한 Computed Properties를 사용할때는 속성을 var로 설정 해야한다. 또한 getter만 존재하기 때문에 `get`을 지우고 `{}`를 사용하여 간단하게 표현 할 수 있다.

```swift
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double { // get 을 명시하지 않고 간단하게 표현 
        return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
print("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
```



## Property Obsevers

Property Obsevers 는 값의 변화를 관찰하고 이에 대응한다. Property Obsevers는 새 값이 현재 값과 동일하더라도  Property 값이 설정 될 때 마다 호출된다.

다음 위치에 Property Obsevers를 추가 할 수 있다.

- Stored properties that you define
- Stored properties that you inherit
- Computed properties that you inherit

상속된 속성의 경우 하위 클래스에서 해당 속성을 override 하여 Property Observer를 추가한다. 정의한 Computed Property에 대해서는 Observer를 만들지 않고 속성의 setter을 사용하여 값 변경을 관찰하고 대응한다. 

- `willSet` 는 값이 저장되기 직전에 호출된다
- `didSet` 새 값이 저장되는 즉시 호출된다.

`willSet` Observer를 구현하면 새 속성 값이 상수 매개변수로 저달된다. `willSet` 구현의 일부로 이 매개변수 이름과 괄호를 쓰지 않으려면 매개 변수를 `newValue` 를 기본 매개변수 이름으로 사용 할 수 있다.

`didSet` Observer를 구현하면 이전 속성 값이 포함된 상수 매개변수가 전달된다. 매개변수의 이름을 지정하거나 `oldValue` 를 기본 매개변수 이름으로 사용 할 수 있다.

```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// print "About to set totalSteps to 200"
// print "Added 200 steps"
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```



### Property Wrappers

Property Wrappers는 속성이 저장되는 방식을 관리하는 코드와 속성을 정의하는 코드 사이에 구분 계층을 추가한다. 예를 들어, 스레드 안전성 검사를 제공하거나 기본 데이터를 데이터베이스에 저장하는 속성이 있는 경우 모든 속성에 해당 코드를 작성해야한다. Property Wrappers는 wrapper를 정의 할 때 관리코드를 한번 작성한 다음 여러 속성에 적용하여 해당 관리코드를 재사용한다.

```Swift
@propertyWrapper //Property Wrapper
struct TwelveOrLess { 
  private var number = 0
  var wrappedValue: Int { // 래핑되는 값이 항상 12보다 작거나 같은 숫자를 갖도록 보장한다.
    get { return number }
    set { number = min(newValue, 12) }
  }
}
```



```swift
struct SmallRectangle {
    @TwelveOrLess var height: Int // @TwelveOrLess 사용
    @TwelveOrLess var width: Int
}

var rectangle = SmallRectangle()
print(rectangle.height) // 초기값 0
// Prints "0"

rectangle.height = 10
print(rectangle.height) 
// Prints "10"

rectangle.height = 24
print(rectangle.height) // 12이상의 값은 12로 설정한다.
// Prints "12"
```



```swift
// @TwelveOrLess 를 사용하지 않고 TwelveOrLess의 속성을 명시적으로 나타 낼 수 있다.
struct SmallRectangle {
    private var _height = TwelveOrLess()
    private var _width = TwelveOrLess()
    var height: Int {
        get { return _height.wrappedValue }
        set { _height.wrappedValue = newValue }
    }
    var width: Int {
        get { return _width.wrappedValue }
        set { _width.wrappedValue = newValue }
    }
}
```



### Setting Initial Values for Wrapped Properties

```swift
@propertyWrapper
struct SmallNumber {
    private var maximum: Int
    private var number: Int

    var wrappedValue: Int {
        get { return number }
        set { number = min(newValue, maximum) }
    }

    init() { // 매개변수 없을 때 해당 값으로 init
        maximum = 12
        number = 0
    }
    init(wrappedValue: Int) { // wrappedValue에 대한 init 값이 주어 질 때
        maximum = 12
        number = min(wrappedValue, maximum)
    }
    init(wrappedValue: Int, maximum: Int) {// wrappedValue와 maximum에 대한 init 값이 주어 질 때
        self.maximum = maximum
        number = min(wrappedValue, maximum)
    }
}
```



```swift
//init() example
struct UnitRectangle {
    @SmallNumber var height: Int = 1
    @SmallNumber var width: Int = 1
}

var unitRectangle = UnitRectangle()
print(unitRectangle.height, unitRectangle.width)
// Prints "1 1"

// init(wrappedValue: Int, maximum: Int) exmaple
struct NarrowRectangle {
    @SmallNumber(wrappedValue: 2, maximum: 5) var height: Int // Property Wrapper init
    @SmallNumber(wrappedValue: 3, maximum: 4) var width: Int
}

var narrowRectangle = NarrowRectangle()
print(narrowRectangle.height, narrowRectangle.width)
// Prints "2 3"

narrowRectangle.height = 100
narrowRectangle.width = 100
print(narrowRectangle.height, narrowRectangle.width) // maximum을 5, 4로 했기 때문 5, 4 출력
// Prints "5 4"
```



### Projecting a Value From a Property Wrapper

Property Wrapper는 `wrappedValue` 외에도 `projectedValue` 를 정의하여 추가 할 수 있다. 아래 SmallerNumber 예제에서 `projectedValue ` 는 너무 큰 값이 들어와 자체적으로 조정이 들어가 갔는지 아닌지 판단하는 여부를 추적 할 수 있는 값이다. 또한 `projectedValue` 는 `$` 표시로 접근 할 수 있다.

```swift
@propertyWrapper
struct SmallNumber {
    private var number = 0
    var projectedValue = false
    var wrappedValue: Int {
        get { return number }
        set {
            if newValue > 12 {
                number = 12
                projectedValue = true // 너무 큰 값이 들어와 조정되었는지 확인
            } else {
                number = newValue
                projectedValue = false
            }
        }
    }
}
struct SomeStructure {
    @SmallNumber var someNumber: Int
}
var someStructure = SomeStructure()

someStructure.someNumber = 4 
print(someStructure.$someNumber) // someNumber 에 대한 projectedValue 접근
// Prints "false"

someStructure.someNumber = 55
print(someStructure.$someNumber)
// Prints "true"
```



## Type Properties

인스턴스 속성은 특정 타입의 인스턴스에 속하는 속성이다. 해당 타입의 새로운 인스턴스를 만들 때마다 해당 인스턴스는 다른 인스턴스와 별도로 고유한 속성 값을 갖는다.

또한  해당 타입의 인스턴스 하나에 속하는 속성이 아니라 타입 자체에 속하는 속성을 정의 할 수 도 있다. 해당 타입의 인스턴스 수에 관계없이 이러한 속성의 복사본은 항상 하나만 있게 된다. 이러한 속성을 Type Properties라고 한다.

Type Properties는 특정 타입의 모든 인스턴스가 사용하는 보편적인 값을 정의하는데 유용하다.

### Type Property Syntax

Type Property를 정의하기 위해서는 변수나 상수 앞에 `static` 을 명시한다.

```swift
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 6
    }
}
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypeProperty: Int {
        return 107
    }
}

```



### Query and Setting Type Properties

```swift
print(SomeStructure.storedTypeProperty)
// Prints "Some value."
SomeStructure.storedTypeProperty = "Another value." // Type Property 변경
print(SomeStructure.storedTypeProperty) 
// Prints "Another value."
print(SomeEnumeration.computedTypeProperty)
// Prints "6"
print(SomeClass.computedTypeProperty)
// Prints "27"
```













