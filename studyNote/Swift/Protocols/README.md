# Protocols

프로토콜은은 메서드, 속성 그리고 특정 작업이나 기능의 일부에 대한 요구사항의 청사진을 정의한다. 프로토콜은 요구사항의 구현을 제공하기 위해 클래스 , 구조체, 또는 enum 을 활용할 수 있다. 프로토콜의 요구사항에 충족하는 모든 타입은 프로토콜에 준수(conform) 한다고 한다.



## Protocol Syntax

```swift
protocol SomeProtocol{
   // protocol 정의
}
```

```swift
// 프로토콜을 사용할 땐 클래스 또는 구조체 뒤에 : 붙혀 사용 할 수 있다.
struct SomeStructure : FirstProtocol, AnotherProtocol {
  
}
// 클래스의 경우 상속 받는 슈퍼클래스가 존재한다면 모든 프로토콜 앞에 위치 시킨다.
class SomeClass : SomeSuperClass, FirstProtocol, AnotherProtocol{
  
}
```



## Property Requirements

속성은 이름과 타입을 가진 인스턴스 속성 또는 타입 속성을 제공하기 위해 준수하는 타입을 요구 할 수 있다. 프로토콜은 요구된 속성의 이름과 타입만 지정하고 stored property 또는 computed property 에 관해서는 지정하지 않는다. 또한 프로토콜은 각 속성이 (gettable) 또는 (gettable, settable) 인지 지정해야 한다.

- (gettable, settable) : 속성 요구사항은 stored property , 상수 또는 read only computed property는 아니다.
- (gettable) : 해당 요구사항은 모든 종류의 프로퍼티가 가능하다.

```swift
// 속성 요구사항은 항상 var 키워드로 시작한다.
protocol SomeProtocol {
    var mustBeSettable: Int { get set } // gettable & settable
    var doesNotNeedToBeSettable: Int { get } // gettable
}

protocol AnotherProtocol {
    static var someTypeProperty: Int { get set } // type property 정의 시에는 static 붙힘
}
```

단일 속성을 갖는 프로토콜 예시

```swift
protocol FullyNamed {
    var fullName: String { get }
}

struct Person: FullyNamed { // Person struct 는 FullyNamed protocol을 채택
    var fullName: String
}
let john = Person(fullName: "John Appleseed")
```

```swift
class Starship: FullyNamed { // Starship class 는 FullyNamed protocol을 채택
    var prefix: String?
    var name: String
    init(name: String, prefix: String? = nil) {
        self.name = name
        self.prefix = prefix
    }
    var fullName: String { // fullName 속성을 computed property로 정의한다.
        return (prefix != nil ? prefix! + " " : "") + name
    }
}
var ncc1701 = Starship(name: "Enterprise", prefix: "USS")
// ncc1701.fullName is "USS Enterprise"
```



## Method Requirements

프로토콜의 메서드 요구사항 정의는 중괄호가 없거나 메서드의 바디가 존재하지 않는다. 일반적인 메서드와 같은 규칙에 따라 가변 파라미터는 허용된다. 

```swift
protocol SomeProtocol {
    static func someTypeMethod() // type method 정의시 static
}
protocol RandomNumberGenerator {
    func random() -> Double // 중괄호, 메서드 바디가 존재하지 않음
}

class LinearCongruentialGenerator: RandomNumberGenerator { // RandomNumberGenerator protocol 
    var lastRandom = 42.0
    let m = 139968.0
    let a = 3877.0
    let c = 29573.0
    func random() -> Double { // protocl method를 채택한 클래스 내에서 정의 해준다.
        lastRandom = ((lastRandom * a + c)
            .truncatingRemainder(dividingBy:m))
        return lastRandom / m
    }
}
let generator = LinearCongruentialGenerator()
print("Here's a random number: \(generator.random())")
// Prints "Here's a random number: 0.3746499199817101"
print("And another one: \(generator.random())")
// Prints "And another one: 0.729023776863283"
```



## Mutating Method Requirements

메서드가 속한 인스턴스를 수정 또는 변경해야 하는 경우가 있다. Struct 또는 Enum 에 대한 인스턴스 메서드의 경우 메서드 `func` 앞에 `mutating` 키워드를 사용한다. 이처럼 프로토콜 또한 `mutating` 키워드를 `func` 앞에 붙혀 인스턴스 속성이 변경될 수 있음을 표시한다.

```swift
protocol Togglable {
    mutating func toggle() // mutating 속성을 수정할 수 있음
}

enum OnOffSwitch: Togglable {
    case off, on
    mutating func toggle() { // OnOffSwift를 on/off 반전 시킴
        switch self {
        case .off:
            self = .on
        case .on:
            self = .off
        }
    }
}
var lightSwitch = OnOffSwitch.off
lightSwitch.toggle()
// lightSwitch is now equal to .on
```



## Initializer Requirements

프로토콜은 지정된 초기화 구문을 요구 할 수 있다. 메서드와 마찬가지로 중괄호와 바디 부분은 존재하지 않는다.

```swift
protocol SomeProtocol {
    init(someParameter: Int)
}
```



### Class Implementations of Protocol Initializer Requirements

```swift
class SomeClass: SomeProtocol {
    required init(someParameter: Int) { // protocol initializer의 경의 앞에 required 키워드를 붙힘
        // initializer implementation goes here
    }
}
```



슈퍼클래스 상속에 대한 override initializer 프로토콜 준수에 대한 두가지 initializer가 요구 되는 경우

```swift
protocol SomeProtocol {
    init()
}

class SomeSuperClass {
    init() {
        // initializer implementation goes here
    }
}

class SomeSubClass: SomeSuperClass, SomeProtocol {
// 프로토콜 : required , 슈퍼클래스 : override 두 키워드를 둘다 사용한다.
  required override init() {
        // initializer implementation goes here
    }
}
```



## Protocol as Types

프로토콜 자체는 어떤 기능도 구현하지 않는다. 그럼에도 불구하고 프로토콜은 코드에서 타입으로써 사용할 수 있다. 타입으로 프로토콜을 사용한것은 어떤 타입이 해당 프로토콜을 준수한다는 것이다 이것을 **existaential type**이라고 한다.

```swift
class Dice {
  let sides: Int
  let generator: RandomNumberGenerator // existaential type 을 사용하여 속성 타입 정의
  init(sides: Int, generator: RandomNumberGenerator) {
    self.sides = sides
    self.generator = generator
  }
  func roll() -> Int {
    return Int(generator.random() * Double(sides)) + 1
  }
}

// generator에 RandomNumberGenerator 프로토콜을 준수하는 LinearCongruentialGenerator()인스턴스를 할당한다.
var d6 = Dice(sides: 6, generator: LinearCongruentialGenerator())
for _ in 1...5 {
  print("Random dice roll is \(d6.roll())")
}
// Random dice roll is 3
// Random dice roll is 5
// Random dice roll is 4
// Random dice roll is 5
// Random dice roll is 4
```



## Delegation

**위임(Delegation)** 은 클래스 또는 구조체가 책임의 일부를 다른 타입의 인스턴스에 위임할 수 있도록 하는 디자인 패턴이다. 이 디자인 패턴은 위임된 기능을 제공하기 우해 준수하는 타입이 보장되도록 위임된 책임을 캡슐화하는 프로토콜을 정의하여 구현한다. 위임은 특정 작업에 응답하거나 해당 소스의 기본 타입을 알 필요 없이 외부 소스에서 데이터를 검색하는데 사용할 수 있다.

```swift
protocol DiceGame { // 모든 게임에 의해 채택 될 수 있음
  var dice: Dice { get }
  func play()
} 
protocol DiceGameDelegate: AnyObject { // DiceGame을 추적하기 위해 사용, AnyObject를 상속 받음으로써 클래스 전용 프로토콜(Class only protocol)이다.
  func gameDidStart(_ game: DiceGame)
  func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)
  func gameDidEnd(_ game: DiceGame)
}
```



```swift
class SnakesAndLadders: DiceGame { // DiceGame 프로토콜 채택
  let finalSquare = 25 
  let dice = Dice(sides: 6, generator: LinearCongruentialGenerator()) // 속성 요구사항 할당
  var square = 0
  var board: [Int]
  init() {
    board = Array(repeating: 0, count: finalSquare + 1)
    board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
    board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
  }
  weak var delegate: DiceGameDelegate? // 진행사항에 대해 알리기 위해 DiceGameDelegate를 약한 참조로 선언
  func play() { // 메서드 요구사항 구현
    square = 0
    delegate?.gameDidStart(self)
    gameLoop: while square != finalSquare {
      let diceRoll = dice.roll()
      delegate?.game(self, didStartNewTurnWithDiceRoll: diceRoll)
      switch square + diceRoll {
        case finalSquare:
        break gameLoop
        case let newSquare where newSquare > finalSquare:
        continue gameLoop
        default:
        square += diceRoll
        square += board[square]
      }
    }
    delegate?.gameDidEnd(self)
  }
}
```

**DiceGameDelgegate 구현**

```swift
class DiceGameTracker: DiceGameDelegate { // DiceGameDelegate를 채택
  var numberOfTurns = 0
  // DiceGameDelegate의 경우 세가지 메서드를 구현해야함
  // game 시작
  func gameDidStart(_ game: DiceGame) { 
    numberOfTurns = 0
    if game is SnakesAndLadders {
      print("Started a new game of Snakes and Ladders")
    }
    print("The game is using a \(game.dice.sides)-sided dice")
  }
  // 게임 중
  func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int) {
    numberOfTurns += 1
    print("Rolled a \(diceRoll)")
  }
  // 게임 끝
  func gameDidEnd(_ game: DiceGame) {
    print("The game lasted for \(numberOfTurns) turns")
  }
}
```

```swift
let tracker = DiceGameTracker() 
let game = SnakesAndLadders()
game.delegate = tracker // game.delegate에 DiceGameTracker() 인스턴스를 할당
game.play() 
// Started a new game of Snakes and Ladders
// The game is using a 6-sided dice
// Rolled a 3
// Rolled a 5
// Rolled a 4
// Rolled a 5
// The game lasted for 4 turns
```



## Adding Protocol Conformance with an Extension

기존 타입에 대해 소스코드에 접근 할 수는 없지만 새로운 프로토콜을 채택하고 준수하기 위해 기존타입을 확장 할 수는 있다. 확장은 기존 타입에 새로운 속성 메서드 서브스크립트를 추가 할 수 있다. 

```swift
protocol TextRepresentable {
  var textualDescription: String { get }
}

extension Dice: TextRepresentable { // Dice는 TextRepresentable 프로토콜을 준수하기 위해 확장됨
  var textualDescription: String {
    return "A \(sides)-sided dice"
  }
}
```



### Conditionally Conforming to a Protocol

General Type은 일반 파라미터가 프로토콜을 준수하는 경우와 같은 특정 조건에서만 프로토콜 요구사항을 충족 시키도록 할 수 있다. 타입을 확장할 때 제약조건을 나열하여 General Type이 프로토콜을 조건적으로 준수할 수 있도록 한다. 일반적인 `where` 절을 작성하여 채택중인 프로토콜의 이름 뒤에 제약조건을 작성한다. 

```swift
// Array의 element가 TextRepresentable 프로토콜을 준수하는 경우 
extension Array: TextRepresentable where Element: TextRepresentable {
  var textualDescription: String {
    let itemsAsText = self.map { $0.textualDescription }
    return "[" + itemsAsText.joined(separator: ", ") + "]"
  }
}
// d6, d12는 TextRepresentable 프로토콜을 준수하기 때문에 textualDescription을 사용할 수 있다.
let myDice = [d6, d12]
print(myDice.textualDescription)
```



### Declaring Protocol Adoption with an Extension

```swift
// TextRepresentable 프로토콜 채택하는 것을 extension을 활용하여 뒤에 명시
struct Hamster { 
  var name: String
  var textualDescription: String { // TextRepresentable 프로토콜 속성 요구사항
    return "A hamster named \(name)"
  }
}
extension Hamster: TextRepresentable {}
```



## Adopting a Protocol Using a Synthesized Implementation

Swift는 많은 경우에 `Equatable`, `Hashable`, `Comparable` 에 대한 프로토콜 준수성을 자동으로 제공할 수 있다. 합성된 구현을 사용하면 프로토콜 구현을 위해 반복저인 상용구 코드를 작성할 필요가 없다.

**Equatable**

- `Equatable` 프로토콜을 준수하는 저장된 프로토콜만 있는 구조체
- `Equatable` 프로토콜을 준수하는 연관된 타입만 있는 열거형
- 연관된 타입이 없는 열거형

`==` 에 대한 Synthesized Implementation 을 받기 휘해 `==` 연산자를 직접 구현하지 않고 `Equatable` 프로토콜에 대한 준수성을 선언한다.

```swift
struct Vector3D: Equatable {
  var x = 0.0, y = 0.0, z = 0.0
}

let twoThreeFour = Vector3D(x: 2.0, y: 3.0, z: 4.0)
let anotherTwoThreeFour = Vector3D(x: 2.0, y: 3.0, z: 4.0)
// Equatable 프로토콜을 준수하므로 두 구조체는 따로 == 연산에 대한 구현 없이 ==를 사용하여 같고 틀림을 판단할 수 있다.
if twoThreeFour == anotherTwoThreeFour {
  print("These two vectors are also equivalent.")
}
// Prints "These two vectors are also equivalent."
```



**Hashable**

- `Hashable` 프로토콜을 준수하는 저장된 프로퍼티만 가지는 구조체
- `Hashable` 프로토콜을 준수하는 연관된 타입만 가지는 열거형
- 연관된 타입이 없는 열거형

`hash(into: )` 에 대한 Synthesized Implementation 을 위해서 `hash(into: )` 를 사용하지 않고 `Hashable` 프로토콜에 대한 준수성을 선언한다.



**Comparable**

-  원시값이 없는 열거형

열거형이 연관된 타입을 가지고 있다면 연관된 타입은 `Comparable` 프로토콜을 준수해야한다. 

```swift
enum SkillLevel: Comparable {
  case beginner
  case intermediate
  case expert(stars: Int) // 연관된 타입(Int)이 Comparable 프로토콜을 준수하기 때문에 OK
}
var levels = [SkillLevel.intermediate, SkillLevel.beginner,
              SkillLevel.expert(stars: 5), SkillLevel.expert(stars: 3)]
for level in levels.sorted() {
  print(level)
}
```



## Collections of Protocol Types

위의 Protocols as Types에서 설명한것과 같이 프로토콜을 콜렉션에 저장되기 위한 타입으로 사용할 수 있다. 

```swift
let things: [TextRepresentable] = [game, d12, simonTheHamster]

for thing in things {
  print(thing.textualDescription)
}
// A game of Snakes and Ladders with 25 squares
// A 12-sided dice
// A hamster named Simon
```



## Protocol Inheritance

프로토콜은 하나 또는 그 이상의 다른 프로토콜을 상속 할 수 잇고 상속한 요구사항을 더 추가 할 수 있다. 프로토콜 상속에 대한 구문은 클래스 상속에 대한 구문과 유사하지만 `,` 로 구분하여 여러개의 상속된 프로토콜을 목록화 하는 옵션을 가지고 있다.

```swift
// 여러개의 프로토콜을 상속
protocol InheritingProtocol: SomeProtocol, AnotherProtocol {
    // protocol definition goes here
}
```



```swift
protocol PrettyTextRepresentable: TextRepresentable {
  var prettyTextualDescription: String { get }
}

// TextRepresentable을 상속하는 PrettyTextRepresentable을 준수한다.
// SnakesAndLadder는 TextRepresentable과 PrettyTextRepresentable 두가지를 모두 만족해야한다.
extension SnakesAndLadders: PrettyTextRepresentable {
  var prettyTextualDescription: String {
    var output = textualDescription + ":\n"
    for index in 1...finalSquare {
      switch board[index] {
        case let ladder where ladder > 0:
        output += "▲ "
        case let snake where snake < 0:
        output += "▼ "
        default:
        output += "○ "
      }
    }
    return output
  }
}
```



## Class-Only Protocols

```swift
// AnyObject 프로토콜을 추가하여 Struct 와 Enum이 아닌 Class만 채택할 수 있도록 제한한다.
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
  // class-only protocol definition goes here
}
```



## Protocol Composition

여러개의 프로토콜을 준수하는 경우 동시에 요구하는 것이 유용할 수 있다. 프로토콜 구성을 사용하여 여러 프로토콜을 단일 요구사항으로 결합할 수 있다. 프로토콜 구성은 모든 프로토콜의 요구사항을 가진 임시 로컬 프로토콜이 정의된 것처럼 동작한다.  

프로토콜 구성은 `protocol1 & protocol2` 형식으로 `&` 를 활용하여 프로토콜을 목록화 할 수 있다.

```swift
protocol Named {
  var name: String { get }
}
protocol Aged {
  var age: Int { get }
}
// Person struct는 Named 와 Aged를 모두 준수한다.
struct Person: Named, Aged {
  var name: String
  var age: Int
}
// celebrator : Named & Aged로 두가지 프로토콜을 모두 준수하는 객체를 매개변수로 받는다.
func wishHappyBirthday(to celebrator: Named & Aged) {
  print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
}
let birthdayPerson = Person(name: "Malcolm", age: 21)
wishHappyBirthday(to: birthdayPerson)
// Prints "Happy birthday, Malcolm, you're 21!"
```

```swift
class Location {
  var latitude: Double
  var longitude: Double
  init(latitude: Double, longitude: Double) {
    self.latitude = latitude
    self.longitude = longitude
  }
}
class City: Location, Named {
  var name: String
  init(name: String, latitude: Double, longitude: Double) {
    self.name = name
    super.init(latitude: latitude, longitude: longitude)
  }
}
// 이경우에는 Location의 모든 하위 클래스와 Named 프로토콜을 준수하는 모든 타입이다.
func beginConcert(in location: Location & Named) {
  print("Hello, \(location.name)!")
}

let seattle = City(name: "Seattle", latitude: 47.6, longitude: -122.3)
beginConcert(in: seattle)
// Prints "Hello, Seattle!"
```



## Checking for Protocol Conformance

프로토콜 준수성에 대해 확인하고 특정 프로토콜로 캐스팅하기 위해 `is` 와 `as` 연산자를 사용 할 수 있다.

```swift
protocol HasArea {
  var area: Double { get }
}     

// HasArea를 준수하는 두개의 클래스
class Circle: HasArea {
  let pi = 3.1415927
  var radius: Double
  var area: Double { return pi * radius * radius }
  init(radius: Double) { self.radius = radius }
}
class Country: HasArea {
  var area: Double
  init(area: Double) { self.area = area }
}

// HasArea를 준수하지 않는 Animal 클래스
class Animal {
  var legs: Int
  init(legs: Int) { self.legs = legs }
}
```

```swift
let objects: [AnyObject] = [
  Circle(radius: 2.0),
  Country(area: 243_610),
  Animal(legs: 4)
]

for object in objects {
  // 프로토콜을 준수하는지 as? 를 사용하여 체크
  if let objectWithArea = object as? HasArea {
    print("Area is \(objectWithArea.area)")
  } else {
    print("Something that doesn't have an area")
  }
}
// Area is 12.5663708
// Area is 243610.0
// Something that doesn't have an area
```



## Optional Protocol Requirements

프로토콜에 옵셔널 요구사항을 정의 할 수 있다. 해당 요구사항은 프로토콜을 준수하기위 무조건 구현될 필요는 없다. 옵셔널 요구사항은 정의 앞 부분에 `optioanl` 키워드를 붙힌다. 옵셔널 요구사항은 Objective-C와 상호작용하는 코드를 작성 할 수 있다. 그러기 위해서는 프로토콜과 옵셔널 요구사항 앞에 `@objc` 키워드를 사용해야 한다. 

옵셔널 요구사항인 속성이나 메서드는 자동으로 타입이 옵셔널이 된다. 예를 들어 `(Int) -> String` 으로 정의 해도 `((Int) -> String)?` 이 된다. 함수 타입의 경우는 메서드의 반환값이 옵셔널이되는 것이 아니라 전체가 옵셔널로 래핑된다.

```swift
@objc protocol CounterDataSource {
  // optional requirements
  @objc optional func increment(forCount count: Int) -> Int
  @objc optional var fixedIncrement: Int { get }
}

class Counter {
  var count = 0
  var dataSource: CounterDataSource?
  func increment() {
		// dataSource는 CounterDataSource? 이므로 값이 존재하는 체크 하고 increment도 optional 이기 때문에 increment()가 구현되어 있는지 체크를 해야만 한다.
    if let amount = dataSource?.increment?(forCount: count) {
      count += amount
    } else if let amount = dataSource?.fixedIncrement {
      count += amount
    }
  }
}
```

```swift
class ThreeSource: NSObject, CounterDataSource {
  let fixedIncrement = 3
}

// 이 경우 dataSource는 존재하지만 increment()가 구현되지 않고 fixedIncrement만 정의 되었기 때문에 두번째 조건문으로 가서 3씩 증가시켜 주게 된다.
var counter = Counter()
counter.dataSource = ThreeSource() 
for _ in 1...4 {
  counter.increment()
  print(counter.count)
}
// 3
// 6
// 9
// 12
```

```swift
class TowardsZeroSource: NSObject, CounterDataSource {
  func increment(forCount count: Int) -> Int {
    if count == 0 {
      return 0
    } else if count < 0 {
      return 1
    } else {
      return -1
    }
  }
}

// 위와 마찬가지로 dataSource는 존재하고 이번에는 increment가 구현되었으므로 첫번째 조건문으로가 구문을 실행한다.
counter.count = -4
counter.dataSource = TowardsZeroSource()
for _ in 1...5 {
  counter.increment()
  print(counter.count)
}
// -3
// -2
// -1
// 0
// 0
```



## Protocol Extensions

프로토콜을 준수하는 타입에 제공하기 위해 메서드, 초기화 구문, 서브 스크립트, 계산된 속성을 확장을 통해서 구현할 수 있다. 이를 통해 각 타입의 개별 적합성 또는 전역 함수가 아닌 프로토콜 자체에 동작을 정의 할 수 있다.

```swift
// RandomNumberGenerator 프로토콜을 extension을 통하여 randomBool() 함수를 자체 동작으로 실행할 수 있도록 구현 하였다.
extension RandomNumberGenerator {
    func randomBool() -> Bool {
        return random() > 0.5
    }
}

// 따로 구현 없이 바로 실행 시킬 수 있다.
let generator = LinearCongruentialGenerator()
print("Here's a random number: \(generator.random())")
// Prints "Here's a random number: 0.3746499199817101"
print("And here's a random Boolean: \(generator.randomBool())")
// Prints "And here's a random Boolean: true"
```



### Providing Default Implementations

해당 프로토콜의 모든 메서드 또는 게산된 요구사항에 기본 구현을 제공하기 위해 확장을 사용 할 수 있다.

```swift
// TextRepresent 프로토콜을 상속하는 PrettyTextReprentable 프로토콜은 상위 프로토콜의 속성 접근의 결과를 반환하기 위해 PrettyTextRepresentable	 속성의 기본 구현을 제공한다.
extension PrettyTextRepresentable  {
    var prettyTextualDescription: String {
        return textualDescription
    }
}
```



### Adding Contsraints to Protocol Extensions

프로토콜 확장을 정의 할 때 확장 메서드와 프로퍼티를 사용하기 전에 타입이 충족해야만 하는 제약 조건을 지정 할 수 있다. 일반 적인 `where` 절을 작성하여 확장되는 프로토콜의 이름뒤에 제약조건을 작성한다. 

```swift
// Collection내의 원소가 Equatable 프로토콜을 준수하는 경우 해당 메서드를 사용할 수 있다.
extension Collection where Element: Equatable {
  func allEqual() -> Bool {
    for element in self {
      if element != self.first {
        return false
      }
    }
    return true
  }
}

let equalNumbers = [100, 100, 100, 100, 100]
let differentNumbers = [100, 100, 200, 100, 200]

print(equalNumbers.allEqual())
// Prints "true"
print(differentNumbers.allEqual())
// Prints "false"
```

















