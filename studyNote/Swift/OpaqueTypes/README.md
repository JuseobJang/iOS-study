# Opaque Types

불투명한 반환 타입이 있는 함수 또는 메서드는 반환값의 타입 정보를 가린다. **함수의 반환 타입으로 구체적인 타입을 제공하는 대신에 반환값을 지원하는 프로토콜 측면으로 설명한다.** 반환값의 기본 타입이 비공개로 유지될 수 있으므로 모듈과 모듈을 호출하는 코드 사이의 경계에서 타입 정보를 숨기는 것이 유용하다. 타입이 프로토콜 타입인 값을 반환하는 것과 달리 붙투명한 타입은 타입 정체성을 보존한다. 컴파일러는 타입 정보에 접근 할 수 있지만 모듈의 클라이언트는 그럴수 없다. 

## The Problem That Opaque Types Solve

예를 들어 ASCII 그림 모양을 그리는 모듈을 작성한다고 가정한다. ASCII 그림 모양의 기본 특성은 `shape`  프로토콜에 대한 요구사항으로 사용될 수 있는 모양의 문자열 표현을 반환하는 `draw()` 함수이다.

```swift
protocol Shape {
  func draw() -> String
}

struct Triangle: Shape {
  var size: Int
  func draw() -> String {
    var result: [String] = []
    for length in 1...size {
      result.append(String(repeating: "*", count: length))
    }
    return result.joined(separator: "\n")
  }
}
let smallTriangle = Triangle(size: 3)
print(smallTriangle.draw())
// *
// **
// ***
```

아래 코드와 같이 제너릭을 사용하여 모양을 수직으로 뒤집는 것과 같은 작업을 구현할 수 있다. 그러나 이 접근 방식에는 중요한 제한이 있다. **뒤집힌 결과는 이를 생성하는데 정확한 제너릭 타입을 노출하게 되는 것이다.**

```swift
struct FlippedShape<T: Shape>: Shape {
  var shape: T
  func draw() -> String {
    let lines = shape.draw().split(separator: "\n")
    return lines.reversed().joined(separator: "\n")
  }
}
let flippedTriangle = FlippedShape(shape: smallTriangle)
print(flippedTriangle.draw())
// ***
// **
// *
```

아래의 코드와 같이 두개의 모양을 수직으로 결합하는 `JoinedShape<T: Shape, U: Shape>` 구조체를 정의하는 이 접근 방식은 뒤집힌 삼각형을 다른 삼각형과 결합하는`JoinedShape<FlippedShape<Triangle>, Triangle>` 과 같은 타입을 생성한다.

```swift
struct JoinedShape<T: Shape, U: Shape>: Shape {
  var top: T
  var bottom: U
  func draw() -> String {
    return top.draw() + "\n" + bottom.draw()
  }
}
let joinedTriangles = JoinedShape(top: smallTriangle, bottom: flippedTriangle)
print(joinedTriangles.draw())
// *
// **
// ***
// ***
// **
// *
```

모양 생성에 대한 자세한 내용을 표출하면 전체 반환타입을 명시해야 하므로 ASCII 그림 모듈의 공개 인터페이스에 포함되지 않는 타입이 유출 될 수 있다. 모듈내에 코드는 다양한 방법으로 같은 모양을 구축할 수 있으면 모양을 사용하는 모듈 바깥에서의 다른 코드는 변환 목록에 대한 세부 구현정보를 고려할 필요가 없다. **`JoinedShape` 와 `FlippedShape` 와 같은 래퍼 타입은 모듈의 사용자에게 중요하지 않으며 표시되지 않아야 한다.** 모듈의 공개 인터페이스는 모양을 결합하고 뒤집는 것과 같은 작업으로 구성 되며 이러한 작업는 다른 `Shape` 값을 반환한다.

## Returning an Opaque Type

불투명한 타입을 사용하면 함수를 호출하는 코드에서 추상화된 방식으로 반횐되는 값의 타입을 선택 할 수 있다. 예를 들어 다음의 예제에서 함수는 모양의 기본타입을 노출하지 않고 사다리꼴을 반환한다.

```swift
struct Square: Shape {
  var size: Int
  func draw() -> String {
    let line = String(repeating: "*", count: size)
    let result = Array<String>(repeating: line, count: size)
    return result.joined(separator: "\n")
  }
}

// opaque type 사용
func makeTrapezoid() -> some Shape {
  let top = Triangle(size: 2)
  let middle = Square(size: 2)
  let bottom = FlippedShape(shape: top)
  let trapezoid = JoinedShape(
    top: top,
    bottom: JoinedShape(top: middle, bottom: bottom)
  )
  return trapezoid
}

// 불필요한 기본 타입을 노출하지 않는다.
let trapezoid = makeTrapezoid()
print(trapezoid.draw())
// *
// **
// **
// **
// **
// *
```

불투명한 반환 타입은 제너릭과도 결합할 수도 있다. 다음의 코드의 함수는 모두 `shape`  프로토콜을 준수하는 일부 타입의 값을 반환한다.

```swift
// 불투명한 타입을 사용하여 호출하는 부분에서 명확한 제너릭 타입을 노출하지 않아도됨.
func flip<T: Shape>(_ shape: T) -> some Shape {
  return FlippedShape(shape: shape)
}
func join<T: Shape, U: Shape>(_ top: T, _ bottom: U) -> some Shape {
  JoinedShape(top: top, bottom: bottom)
}

let opaqueJoinedTriangles = join(smallTriangle, flip(smallTriangle))
print(opaqueJoinedTriangles.draw())
// *
// **
// ***
// ***
// **
```

`opaqueJoinedTriangles` 의 값은 이전의 `joinedTriangles` 와 동일하다. 그러나 `flip(_:)` 과 `join(_: _:)` 은 불투명한 반환 타입으로 반환하는 제너릭 모양 연산자인 기본 타입을 래핑하여 해당 타입이 표시되지 않도록 한다. 두 함수는 의존하는 타입이 제너릭이고 함수에 대한 타입 파라미터가 `FlippedShape` 와 `JoinedShape` 에 필요한 타입 정보를 전달하기 때문에 모두 제너릭이다.

불투명한 반환 타입을 가진 함수가 여러위치에서 반환하는 경우 가능한 모든 반환 값은 동일한 타입을 가져야 한다. 제너릭 함수의 경우 해당 반환 타입은 함수의 제너릭 타입 파라미터로 사용할 수 있지만 여전히 단일 타입 이어야 한다. 

```swift
// 여러 위치에서 다른 타입을 반환하기 때문에 에러가 난다. 불투명한 타입을 사용 할 경우 반환 되는 타입은 모두 같아야 한다.
func invalidFlip<T: Shape>(_ shape: T) -> some Shape {
  if shape is Square {
    return shape // Error: return types don't match
  }
  return FlippedShape(shape: shape) // Error: return types don't match
}
```

## Differences Between Opaque Types and Protocol Types

불투명한 타입을 반환하는 것은 함수의 반환 타입으로 프로토콜을 타입을 사용하는 것과 매우 유사하지만 이 두 종류의 반환 타입은 타입 정체성을 유지하는지 여부가 다르다. **불투명한 타입은 하나의 특정 타입을 참조하지만 함수 호출자는 어떤 타입인지 볼 수 없다.** 프로토콜 타입은 프로토콜을 준수하는 모든 타입을 참조할 수 있습니다. 일반적으로 프로토콜 타입은 저장하는 기본 타입에 대해 더 많은 유연성을 제공하고 불투명한 타입을 사용하면 이러한 기본타입에 대해 더 강력한 보증을 할 수 있다.

다음 예시는 프로토콜 타입을 사용하는 `flip(_:)` 이다.

```swift
func protoFlip<T: Shape>(_ shape: T) -> Shape {
  return FlippedShape(shape: shape)
}
```

`protoFlip(_ :)` 은 `flip(_ :)` 과 같은 바디를 가지고 항상 같은 타입의 값을 반환한다. 하지만 `flip(_ :)` 과 다르게 `protoFlip(_:)` 이 반환하는 값은 항상 같은 타입을 가질 필요가 없으며 `Shape` 프로토콜을 준수하기만 하면된다. 따라서 API 계약을 느슨하게 만들고 이것은 여러 타입의 값을 반환하는 유연성을 보유한다.

```swift
// 위의 Opaque Type 으로 반환할 시에는 해당 함수는 에러가 났지만 여기서는 더 느슨한 조건을 가지기 때문에 Shape 프로토콜을 준수하기만 한다면 에러가 나지 않는다.
func protoFlip<T: Shape>(_ shape: T) -> Shape {
  if shape is Square {
    return shape
  }
  return FlippedShape(shape: shape)
}
```

하지만 이처럼 구체적이지 않은 반환 타입은 타입 정보에 의존하는 많은 작업이 반환된 값에서 사용 할 수 없음을 의미한다. 예를 들어 이 함수에 의해 반환된 결과를 비교한 `==` 연산자를 작성 할 수 없다.

```swift
let protoFlippedTriangle = protoFlip(smallTriangle)
let sameThing = protoFlip(smallTriangle)
protoFlippedTriangle == sameThing  // Error
```

`==` 와 같은 연산자는 일반적으로 프로토콜을 채택하는 구체적인 타입과 일치하는 `Self` 타입의 인수를 사용하지만 프로토콜에 `Self` 요구사항을 추가하면 프로토콜을 타입으로 사용할 때 발생하는 타입 삭제가 허용되지 않는다.

함수의 반환 타입으로 프로토콜 타입을 사용하면 프로토콜을 준수하는 모든 타입을 유연하게 반환 할 수 있다. 하지만 이러한 유연성의 대가는 반환된 값에 대해 일부 작업을 수행할 수 없도록 한다. 위 예제 처럼 프로토콜 타입을 사용하여 보존되지 않는 특정 타입 정보에 따라 `==` 연산자를 사용할 수 없다.

또한 프로토콜 반환은 모양 변형이 중첩되지 않는다. 삼각형을 뒤집은 결과는 `Shape` 타입의 값이고 `protoFlip(_:)` 함수는 `Shape` 프로토콜을 준수하는 일부 타입의 인수를 가진다. 하지만 프로토콜 타입 `protoFlip(_:)` 에 의해 반환된 값은 `Shape` 를 준수하지 않는다. 따라서 여러 변형이 적용된 `protoFlip(protoFlip(smallTriangle))` 는 유효하지 않는 인수가 들어가게 되기 때문에 불가능 하다.

**반대로 불투명한 타입은 기본타입의 정체성을 보존 할 수 있다.** Swift는 연관된 타입(Associated Type)을 유추 할 수 있으므로 프로토콜 타입을 반환값으로 사용할 수 없는 위치에 불투명한 반환값을 사용 할 수 있다. 다음은 *Generic* 의 `Container` 프로토콜 버전 예시이다.

```swift
protocol Container {
  associatedtype Item
  var count: Int { get }
  subscript(i: Int) -> Item { get }
}
extension Array: Container { }
```

프로토콜은 연관된 타입을 가지고 있으므로 함수의 반환 타입으로 `Container` 를 사용 할 수 없다. 또한 제너릭 타입이 필요한지 추론하기 위해 함수바디의 외부에 충분한 정보가 없으므로 제너릭 반환 타입의 제약 조건으로 사용할 수 없다.

```swift
// Error: Protocol with associated types can't be used as a return type.
func makeProtocolContainer<T>(item: T) -> Container {
    return [item]
}

// Error: Not enough information to infer C.
func makeProtocolContainer<T, C: Container>(item: T) -> C {
    return [item]
}
```

반환타입으로 불투명한 타입을 사용하면 함수는 컨테이너를 반환하지만 컨테이너의 타입 지정을 거부 하므로 원하는 API 가 표현된다.

```Swift
func makeOpaqueContainer<T>(item: T) -> some Container {
    return [item]
}
let opaqueContainer = makeOpaqueContainer(item: 12)
let twelve = opaqueContainer[0]
print(type(of: twelve))
// Prints "Int"
