# Enumerations

Enumerations는 관련된 값들의 그룹을 정의하는데 사용되고 이러한 값들을 type-safe하게 사용할 수 있도록 해준다.

또한 각 enumerations 케이스는 서로다른 각 케이스 값과 함께 모든 유형의 관련된 값을 지정할 수 있다. 공통적으로 관련된 케이스 집합을 하나의 enumeration으로 정의 할 수 있고 각 enumerations 에는 서로 다른 유형의 값의 집합이 연관되어 있다.

Swift의 Enumerations는 First- Class 이다. 이것은 enumeration의 현재 값에 대한 추가 정보를 제공하기 위한 계산된 속성이나 enumerations에 나타내는 값과 관련된 기능을 제공하기 위한 인스턴스 메소드 등 클래스에서 지원되는 많은 기능을 제공한다. Enumerations는 초기 case값을 제공하도록 Initializer를 정의 할수도 있고 원래 구현 이상으로 기능을 확장 할 수 도 있으며, 프로토콜을 준수하여 표준 기능을 제공 할 수 도 있다.



## Enumeration Syntax

```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}

// multiple case는 ','로 구별하여 정의 할 수 있다.
enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
}

var direction = CompassPoint.east // type을 명시하지 않을시 
var direcion2: CompassPoint = .east // type을 명시 할 시 .east로 바로 접근 가능

direction = .east // 위에서 타입추론이 되었기 때문에 .east로 가능
```



## Matching Enumeration Value with a Swift Statement

```swift
// switch 문을 이용하여 enumerations 의 case에 따른 동작을 매칭
directionToHead = .south
switch directionToHead {
case .north:
    print("Lots of planets have a north")
case .south:
    print("Watch out for penguins")
case .east:
    print("Where the sun rises")
case .west:
    print("Where the skies are blue")
}
```

```swift
let somePlanet = Planet.earth
switch somePlanet {
case .earth:
    print("Mostly harmless")
default:
    print("Not a safe place for humans")
}
```



## Iterating over Enumeration Cases

일부 enumerations의 경우 **: CaseIterable**을 뒤에 붙혀 enumerations의 모든 case들을 수집(Collection)하는데 사용될 수 있다. 

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}
let numberOfChoices = Beverage.allCases.count
print("\(numberOfChoices) beverages available") // 3 beverages available

for beverage in Beverage.allCases { // Baverate.allCases 의 type은 [Baverage]
    print(beverage)
}
// coffee
// tea
// juice
```



## Associated Values

앞에서는 enumerations의 case 에서 정의 및 입력된 값을 사용하는 방법을 보여준다. 이것은 상수 또는 변수를 Planet.earth로 설정하고 나중에 이 값을 확인하는 것이 가능하다. 하지만 경우에 따라서 다른 type의 값들을 이러한 case와 함께 저장할 수 있다. 이러한 추가 정보를 Associtated Values라고 한다. 

지정된 type의 associated values를 저장하도록 Swift enumerations를 정의할 수 있으며 필요한 경의 각 case에 대해 value type이 다를 수 있다.

예를 들어 재고추적 시스템에서 서로 다른 두가지 유형의 바코드를 기준으로 제품을 추적해야 한다고 하면 일부 제품에는 숫자 0~9를 사용하는 UPC 형식의 1-dimension 바코드가 레이블로 표시되어 있다. 

다른 제품에는 ISO 8859-1 문자를 사용 할 수 있고 최대 2,953 자의 문자열을 인코딩 할 수 있는 QR code 형식의 2-dimension 바코드가 있다.

재고추적 시스템은 UPC 바크도는 4개의 정수로 이루어진 튜플로, QR 바코드는 임의의 길이의 문자열로 저장하는 것이 편리하다.

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

var productBarcode = Barcode.upc(8, 85909, 51226, 3)
productBarcode = .qrCode("ABCDEFGHIJKLMNOP") // qrCode(String) 으로 대체
```



또한 스위치 문을 사용하여 Associated 값을 추출할 수 있다.

```swift
switch productBarcode {
case .upc(let numberSystem, let manufacturer, let product, let check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
case .qrCode(let productCode):
    print("QR code: \(productCode).") // ABCDEFGHIJKLMNOP
}


//"let"은 생략 가능
switch productBarcode {
case let .upc(numberSystem, manufacturer, product, check):
    print("UPC : \(numberSystem), \(manufacturer), \(product), \(check).")
case let .qrCode(productCode):
    print("QR code: \(productCode).") // ABCDEFGHIJKLMNOP
}
```



## Raw Values

Enumerations case가 모두 동일한 type인 기본값(Raw Values)으로 미리 채워질 수 있다.

```swift
// 동일한 type으로 지정해야 하며 type을 명시해야 한다.
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}

enum Number: Int {
    case one = 1
    case two = 2
    case three = 3
}
```



### Implicitly Assigned Raw Values

정수 또는 문자열 raw value를 저장하는 enumerations를 사용할 때는 어떠한 경우에 대해서는 명시적으로 할당할 필요가 없다. Swift가 자동으로 값을 할당 한다. 

```swift
// 1씩 증가하는 경우
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}

// 변수명 자체를 rawvalue로 지정할 경우
enum CompassPoint: String {
    case north, south, east, west
}

let earthsOrder = Planet.earth.rawValue // 3
let sunsetDirection = CompassPoint.west.rawValue // west
```



### Initializing from a Raw Value

Raw value의 타입을 가지고 enumeration을 정의하는 경우 enumeration은 raw value의 타입을 "rawValue"라는 매개변수로 자동으로 수신하고 enumeration 또는 0을 반환한다. 이 initializer를 사용하여 enumeration의 새로운 instance를 생성할 수 있다.

```swift
let possiblePlanet = Planet(rawValue: 7) // uranus

let positionToFind = 11
if let somePlanet = Planet(rawValue: positionToFind) {
    switch somePlanet {
    case .earth:
        print("Mostly harmless")
    default:
        print("Not a safe place for humans")
    }
} else {
    print("There isn't a planet at position \(positionToFind)") // 11에 해당하는 enumeration은 없기 때문에 해당 문구 출력 
} 
```



## Recursive Enumerations

Recursive enumerations는 enumeration의 인스턴스를 하나 이상의 enumeration case의 associated value로 갖는 enumeration이다. 이러한 enumeration은 case 앞에 "indirect"를 붙혀 재귀적임을 나타낸다.

```swift
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression) // associated value로 ArithmeticExpression instance를 가짐
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}

// enum 앞에 indirect를 붙이면 case 앞에 붙히는 것은 생략 가능
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```

```swift
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))
```

```swift
// 재귀적으로 ArithmeticExpression이 Instance가 사용됨
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

print(evaluate(product)) // 18
```











