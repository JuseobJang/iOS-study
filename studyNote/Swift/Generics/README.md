# Generics

제너릭 코드(Generic Code)는 정의한 요구사항에 따라 모든 타입에서 동작할 수 있는 유연하고 재사용 가능한 함수와 타입을 작성할 수 있게 해준다. 

제너릭은 스위프트의 강력한 특징 중 하나이다. 스위프트 표준 라이브러리 대부분은 제너릭 코드로 되어있이다. 예를 들어 스위프트의 `Array` 와 `Dictionary ` 타입 둘다 제너릭 콜렉션이다. 

## The Problem That Generics Solve

```swift
// 두 Int 타입의 스왑 메서드
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
  let temporaryA = a
  a = b
  b = temporaryA
}
// 두 String 타입의 스왑 메서드
func swapTwoStrings(_ a: inout String, _ b: inout String) {
    let temporaryA = a
    a = b
    b = temporaryA
}
// 두 Double 타입의 스왑 메서드
func swapTwoDoubles(_ a: inout Double, _ b: inout Double) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

해당 코드 처럼 작성하면 각 타입에 따라 스왑을 하기위해 다른 메서드를 사용한다. 제너릭을 사용하면 모든타입의 2개의 값을 바꾸는 단일함수로 작성하여 더 유용하고 유연하게 할 수 있다.

## Generic Functions

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
  let temporaryA = a
  a = b
  b = temporaryA
}
```

제너릭 함수를 사용하기 위해서는 함수의 이름 앞에 `<T>` 처럼 임의의 타입이 "<>" 안에 들어가 있어야 한다는 것이다. 

`swapTwoValues(_: _:)`는 인자로 들어오는 두 값이 서로 같은 타입이면 어떠한 타입이 들어와도 가능하다. 또한 `T` 는 `swapTwoValues()` 가 호출 될 때 마다 인자로 들어온 값의 타입으로 부터 유추된다.

## Type Parameters

위의 `swapTwoValues(_: _:)` 의 임의 타입 `T` 는 타입 파라미터의 예시이다. 타입 파라미터는 임의의 타입을 지정하고 이름을 지정하며 "<>" 안에 표시되며 함수의 이름 뒤에 작성해야한다.

타입 파라미터를 지정하면 함수의 매개변수의 타입을 정의하거나 반환 타입 또는 바디내에서 타입 주석으로 사용할 수 있다. 타입파라미터는 함수가 호출될 때마다 실제 차입으로 대체된다.

꺾쇠 괄호 안에 여러개의 타입파라미터를 작성하여 여러개의 타입파라미터를 사용할 수 있다.

## Generic Types

제너릭 함수 외에도 스위프트는 고유한 제너릭 타입을 정의할 수 있다. `Array` 또는 `Dictionary` 처럼 모든 타입에서 동작 할 수 있는 사용자 정의 클래스, 구조체, 열거형을 정의할 수 있다.

**Stack Example**

<p align="center">
  <img src="https://docs.swift.org/swift-book/_images/stackPushPop_2x.png" width="400px" />
</p>

1. 스택에 3개의 값이 있다.
2. 4번째 값이 스택의 상단에 푸쉬
3. 스택은 4개의 값을 갖게 되며 최근 값이 가장 상단에 위치
4. 스택의 최상단 항목을 팝 한다.
5. 값을 팝 한 후에 스택은 다시 3개의 값만 갖는다.

```swift
struct Stack<Element> {
  var items: [Element] = []
  mutating func push(_ item: Element) {
    items.append(item)
  }
  mutating func pop() -> Element {
    return items.removeLast()
  }
}
```

`<Element>` 는 나중에 제공할 타입에 대한 임의의 이름을 정의한다. 이 미래의 타입은 구조체의 정의 내 어디서나 `Element` 로 참조 될 수 있다. 

```swift
// Element -> String
var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")
stackOfStrings.push("cuatro")
// the stack now contains 4 strings
```

<p align="center">
  <img src="https://docs.swift.org/swift-book/_images/stackPushedFourStrings_2x.png" width="400px" />
</p>

```swift
let fromTheTop = stackOfStrings.pop()
```

<p align="center">
  <img src="https://docs.swift.org/swift-book/_images/stackPoppedOneString_2x.png" width="400px" />
</p>



## Extending a Generic Type

제너릭 타입을 확장할 때 확장의 정의 부분에 타입 파라미터의 목록을 제공하지는 않는다. 하지만 기존 타입 정의의 타입 파라미터 목록은 확장의 바디 내에서도 그대로 사용 가능하다.

```swift
// 타입 파라미터 목록은 제공하지 않지만 그대로 사용가능
extension Stack {
  var topItem: Element? {
    return items.isEmpty ? nil : items[items.count - 1]
  }
}
```



## Type Constraints

위의 `swapTwoValues(_: _:)` 와 `Stack` 은 모든 타입과 함께 동작 가능 하다. 하지만 가끔 제너릭 함수와 제너릭 타입으로 사용될 수 있는 타입에 제약을 강제로 포함 해야 할 수 도 있다. 타입 제약은 타입 파라미터가  특정 클래스를 상속하거나 특정 프로토콜을 준수해야함을 지정 해야 한다.

예를 들어 스위프트의 `Dictionary` 타입은 딕셔너리에 대해 키로 사용될 수 있는 타입에 제한을 둔다. 딕셔너리의 키 타입은 *hashable* 이어야 한다. 즉, 고유하게 표현할 수 있는 방법을 제공 해야한다. `Dictionary` 는 특정 키에 대해 값이 이미 포함되어 있는 지 확인 할 수 있도록 키를 해시 할 수 있어야 한다. 이 요구사항을 만족하지 않는다면 `Dictionary` 는 특정 키에 대해 값을 삽입 또는 대체해야 하는지 알 수 없으며 이미 딕셔너리에 있는 주어진 키에 대한 값을 찾을 수 없다.

사용자 정의 제너릭 타입을 생성할 때 고유 타입 제약을 정의 할 수 있고 이러한 제약은 제너릭 프로그래밍에 많은 기능을 제공한다. `Hashable` 같은 추상 개념은 구체적인 타입이 아닌 개념적 특성 측면에서 타입을 활성화 한다.

### Type Constraint Syntax

타입 파라미터 목록에서 타입 파라미터 이름 뒤에 콜론으로 구분하여 단일 클래스 또는 프로토콜을 위치하여 타입 제약을 작성한다. 

```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U){
  // function body
}
```

`T` 는 `SomeClass` 의 하위 클래스임을, `U` 는 `SomeProtocol` 을 준수해야 하는 타입 제약이 있다.

### Type Constraints in Action

제너릭이 아닌 `findIndex(ofString: in:)`

배열에서 일치하는 문자열을 찾으면 그 인덱스를 반환하고 그렇지 않으면 `nil` 을 반환한다.

```swift
func findIndex(ofString valueToFind: String, in array: [String]) -> Int? {
  for (index, value) in array.enumerated() {
    if value == valueToFind {
      return index
    }
  }
  return nil
}
```

제너릭을 이용한 `findIndex(of: in:)` 

`String` 뿐만아니라 다른 타입에 대해서도 단일함수 하나로 작성 가능

```swift
func findIndex<T>(of valueToFind: T, in array:[T]) -> Int? {
  for (index, value) in array.enumerated() {
    if value == valueToFind {
      return index
    }
  }
  return nil
}
```

하지만 해당 함수는 `if value == valueToFind` 에서의 동등성 검사 부분 때문에 컴파일 에러가 발생한다. 스위프트의 모든 타입이 동등 연산자를 사용할 수 있는 것이 아니다. 따라서 2개의 값을 비교하기 위해 동등 연산자와 비동등 연산자를 구현하기 위해 채택하는 `Equatable` 프로토콜을 정의한다.

`T` 가 프로토콜 `Equatable` 을 준수하는 타입 제약을 가진 제너릭 함수

```swift
func findIndex<T: Equatable>(of valueToFind: T, in array:[T]) -> Int? {
  for (index, value) in array.enumerated() {
    if value == valueToFind {
      return index
    }
  }
  return nil
}
```

`Equatable` 을 준수하는 모든 타입에 대해 해당 함수를 사용 할 수 있다.

```swift
let doubleIndex = findIndex(of: 9.3, in: [3.14159, 0.1, 0.25])
// doubleIndex is an optional Int with no value, because 9.3 isn't in the array
let stringIndex = findIndex(of: "Andrea", in: ["Mike", "Malcolm", "Andrea"])
// stringIndex is an optional Int containing a value of 2
```



## Associated Types

프로토콜을 정의할 때 연관된 타입(associate types) 를 선언하는 것이 더 유용한 경우가 있다. 연관된 타입(associcated types)은 프로토콜의 부분으로 사용되는 타입의 임의의 이름을 제공한다. 연관된 타입에 사용할 실제 타입은 프로토콜이 채택되기까지는 지정되지 않는다. 연관된 타입은 `associatedtype`  키워드와 함께 지정한다.



### Associated Types in Action

다음은 `Item` 이라는 연관된 타입을 선언하는 `Container` 라는 프로토콜의 예이다.

```swift
protocol Container {
  associatedtype Item
  mutating func append(_ item: Item)
  var count: Int { get }
  subscript(i: Int) -> Item { get }
}
```

`Container` 프로토콜은 모든 컨테이너가 준수해야하는 3가지 필수 요건을 정의한다.

- `append(_: )` 메서드를 사용하여 컨테이너에 새로운 항목을 추가 할 수 있어야 한다.
- `Int` 값을 반환하는 `count` 속성을 통해 컨테이너 항목의 카운트에 접근 할 수 있어야한다.
- `Int` 인덱스 값을 사용하는 서브 스크립트로 컨테이너의 각 항목을 조회 할 수 있어야 한다.

해당 프로토콜은 컨테이너에 항목을 저장하는 방법 또는 허용되는 타입을 지정하지 않는다. 해당 프로토콜은 `Container` 로 간주되기 위해 모든 타입이 제공되는 3가지의 기능만 지정하면 된다. 해당 프로토콜을 준수하는 타입은 이 3가지 요구사항을 준수하는 한 추가적인 기능을 제공 할 수 있다.

`Container`  프로토콜을 준수하는 모든 타입은 저장하는 값의 타입을 지정할 수 있어야한다. 특히, 올바른 타입의 항목만 컨테이너에 추가되어야 하며 서브스크립트에 의해 반환된 항목에 타입을 명확하게 해야 한다.

이러한 요구사항을 정의하기 위해 `Container`  프로토콜은 특정 컨테이너에 대한 타입이 무엇인지 알지 못해도 컨테이너가 보유할 항목의 타입을 참조할 방법이 필요하다. `Container` 프로토콜은 `append(_ : )`  메서드에 저달된 모 값이 컨테이너의 요소 타입과 같은 타입을 가져야 하며 컨테이너의 서브스크립트에 의해 반환된 값은 컨테이너의 요소 타입과 같은 타입으로 지정해야 한다.

이를 달성하기 위해 `Container` 프로토콜은 `associatedtype Item` 으로 작성한 `Item` 이라는 연관된 타입을 선언한다. 이 프로토콜은 `Item` 이 무엇인지 정의하지 않고 해당 정보는 모든 준수하는 타입이 제공할 수 있도록 남겨진다. 그럼에도 불구하고 `Item` 별칭은 `Container` 의 항목에 타입을 참조하고 `append(_ : )`  메서드와 서브스크립트에서 사용하는 타입을 정의하고 모든 `Container` 의 동작이 예상되도록 방법을 제공한다.

```swift
struct Stack<Element>: Container {
  
  // original Stack<Element> implementation
  var items: [Element] = []
  mutating func push(_ item: Element) {
    items.append(item)
  }
  mutating func pop() -> Element {
    return items.removeLast()
  }
  
  
  // conformance to the Container protocol
  mutating func append(_ item: Element) {
    self.push(item)
  }
  var count: Int {
    return items.count
  }
  subscript(i: Int) -> Element {
    return items[i]
  }
}
```



### Extending an Existing Type to Specify an Associated Type

프로토콜을 준수성을 추가하기 위해 기존 타입을 확장할 수 있다. 여기에는 연관된 타입이 있는 프로토콜도 포함된다.

스위프트의 `Array` 타입은 이미 `append(_:)`  메서드, `count` 속성 그리고 `Int` 인덱스에 대한 서브스크립트를 제공한다. 이 3가지 기능은 `Container` 프로토콜의 요구사항과 일치한다. 이것은 `Array` 가 프로토콜을 채택하도록 선언하는 것으로 간단하게 `Container` 프로토콜을 준수하도록 `Array` 를 확장할 수 있다는 의미이다. 빈 확자을 사용하여 이작업을 수행 할 수 있다.(이미 준수성을 만족 하였지만 명시하기 위해)

```swift
extension Array: Container {}
```

모든 `Array` 를 `container` 로 사용할 수 있다.



### Adding Constraints to an Associated Type

연관된 타입에 제약조건을 추가할 수 있다.

```swift
protocol Container {
  // 연관타입 Item에 Equatable 프로토콜을 준수해야한다는 제약조건을 추가
  associatedtype Item: Equatable
  mutating func append(_ item: Item)
  var count: Int { get }
  subscript(i: Int) -> Item { get }
}
```



### Using a Protocol in Its Associated Type's Constraints

프로토콜은 자체 요구사항의 일부로 나타낼 수 있다.

```swift
protocol SuffixableContainer: Container {
  associatedtype Suffix: SuffixableContainer where Suffix.Item == Item
  func suffix(_ size: Int) -> Suffix
}
```

해당 프로토콜에서 `suffix`는 위의 `Container`예제에서 `Item`타입과 같은 연돤된 타입이다. `Suffix` 는 두가지 제약 조건을 가지고 있다.

1. `SuffixableContainer` 프로토콜을 준수
2. `Item`타입은 컨테이너의 `Item`타입과 동일

```swift
extension Stack: SuffixableContainer {
    func suffix(_ size: Int) -> Stack {
        var result = Stack()
        for index in (count-size)..<count {
            result.append(self[index])
        }
        return result
    }
    // Inferred that Suffix is Stack.
}
var stackOfInts = Stack<Int>()
stackOfInts.append(10)
stackOfInts.append(20)
stackOfInts.append(30)
let suffix = stackOfInts.suffix(2)
```



## Generics Where Clauses

제너릭 where 절을 정의하여 연관된 타입에 대한 요구사항을 정의 할 수 있다. 제너릭 where 절을 사용하면 연관된 타입이 특정 프로토콜을 준수해야하 하거나 특정 타입 파라미터와 연관된 타입이 동일 해야한다고 요구사항을 정의 할 수 있다. 제너릭 where절은 `where` 키워드로 시작하고 이어서 연관된 타입 또는 타입과 연관된 타입 사이의 동등 관계에 대한 제약이 따라온다. 타입 또는 함수의 바디의 여는 중괄호 바로 전에 where 절을 작성한다.

아래 예제는 2개의 `Container ` 인스턴스가 같은 순서로 같은 항목을 가지고 있는지 확인하는 `allItemMatch`  라는 제너릭 함수를 정의한다. 

확인할 2개의 컨테이너는 같은 타입의 컨테이너 일 필요는 없지만 같은 타입의 항목을 가지고 있어야 한다. 이 요구사항은 타입 제약과 제너릭 where 절의 조합으로 표현된다.

```swift
// C1, C2 는 제너릭 타입은 Container 프로토콜을 준수해야함
func allItemsMatch<C1: Container, C2: Container>
(_ someContainer: C1, _ anotherContainer: C2) -> Bool
// C1.Item 과 C2.Item이 같은 타입이고 Equatable 프로토콜을 준수해야한다.
where C1.Item == C2.Item, C1.Item: Equatable {

  // Check that both containers contain the same number of items.
  if someContainer.count != anotherContainer.count {
    return false
  }

  // Check each pair of items to see if they're equivalent.
  for i in 0..<someContainer.count {
    if someContainer[i] != anotherContainer[i] {
      return false
    }
  }

  // All items match, so return true.
  return true
}
```

```swift
var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")

var arrayOfStrings = ["uno", "dos", "tres"]

if allItemsMatch(stackOfStrings, arrayOfStrings) {
    print("All items match.")
} else {
    print("Not all items match.")
}
// Prints "All items match."
```



## Extensions with a Generic Where Clause

확장의 부분으로 제너릭 where 절을 사용할 수도 있다.

```swift
// extenstion 에서 where 절을 사용하여 Element의 Equatable 준수성 확인
extension Stack where Element: Equatable {
  func isTop(_ item: Element) -> Bool {
    guard let topItem = items.last else {
      return false
    }
    return topItem == item
  }
}
```

제너릭 where 절을 사용하여 확장에 새로운 요구사항을 추가 할 수 있다. 확장은 스택의 Item이 `Equatable` 프로토콜을 준수할 때만  `isTop(_: )`  메서드를 추가한다.

```swift
if stackOfStrings.isTop("tres") {
print("Top element is tres.")
} else {
print("Top element is something else.")
}
// Prints "Top element is tres."
```

`Equatable` 을 준수하지 않는 경우 에러가 발생한다.

```swift
struct NotEquatable { }
var notEquatableStack = Stack<NotEquatable>()
let notEquatableValue = NotEquatable()
notEquatableStack.push(notEquatableValue)
notEquatableStack.isTop(notEquatableValue)  // Error
```



```swift
// 마찬가지로 Item이 Equatable을 준수하는 경우만 startWith 메서드를 사용 할 수 있음
extension Container where Item: Equatable {
  func startsWith(_ item: Item) -> Bool {
    return count >= 1 && self[0] == item
  }
}
```

```swift
// Int 는 Equatable을 준수하므로 정상적으로 함수가 실행됨
if [9, 9, 9].startsWith(42) {
  print("Starts with 42.")
} else {
  print("Starts with something else.")
}
// Prints "Starts with something else."
```

특정 타입을 요구하도록 제너릭 where 절을 작성할 수 도 있다.

```swift
// Item이 Double 타입인 경우에만 average 메서드 추가
extension Container where Item == Double {
  func average() -> Double {
    var sum = 0.0
    for index in 0..<count {
      sum += self[index]
    }
    return sum / Double(count)
  }
}
print([1260.0, 1200.0, 98.6, 37.0].average())
// Prints "648.9"
```



## Contextual Where Clauses

제너릭 타입을 사용하여 이미 컨텍스트에서 사용중일 경우 원래의 제너릭 타입에 제약조건을 추가하지 않고 부분적으로 제너릭 where절을 사용하여 필요한 것을 추가할 수 있다.

```swift
extension Container {
  // Item 의 타입이 Int인 경우에만 해당 average 메서드를 추가
  func average() -> Double where Item == Int {
    var sum = 0.0
    for index in 0..<count {
      sum += Double(self[index])
    }
    return sum / Double(count)
  }
  // Item 이 Equtable 을 준수하는 경우에만 endsWith 메서드를 추가
  func endsWith(_ item: Item) -> Bool where Item: Equatable {
    return count >= 1 && self[count-1] == item
  }
}
let numbers = [1260, 1200, 98, 37]
print(numbers.average())
// Prints "648.75"
print(numbers.endsWith(37))
// Prints "true"
```

메서드 별로 제너릭 where 절을 작성하지 않고 extension 구문 뒤에 써서 합칠 수 있다.

```swift
extension Container where Item == Int {
  func average() -> Double {
    var sum = 0.0
    for index in 0..<count {
      sum += Double(self[index])
    }
    return sum / Double(count)
  }
}
extension Container where Item: Equatable {
  func endsWith(_ item: Item) -> Bool {
    return count >= 1 && self[count-1] == item
  }
}
```


## Associated Types with Generics Where Clauses

연관된 타입에 제너릭 where절을 포함 할 수 있다. 

```swift
protocol Container {
  associatedtype Item
  mutating func append(_ item: Item)
  var count: Int { get }
  subscript(i: Int) -> Item { get }

  // 연관된 타입에 where절을 추가
  associatedtype Iterator: IteratorProtocol where Iterator.Element == Item
  func makeIterator() -> Iterator
}
```



## Generic Subscripts

서브 스크립트는 제너릭 일 수 있고 제너릭 where 절을 포함 할 수 있다. `subscript`  다음 꺾쇠 괄호 안에 임의의 타입이름을 작성하고 서브 스크립트의 바디의 열린 중괄호 전에 제너릭을 where 절을 작성한다.

```swift
extension Container {
  // Indices 는 Sequence 를 준수하는 타입이어야 함
  subscript<Indices: Sequence>(indices: Indices) -> [Item]
  // 시퀀스의 반복자는 Int 타입의 요소를 가져야 함 
  where Indices.Iterator.Element == Int {
    var result: [Item] = []
    for index in indices {
      result.append(self[index])
    }
    return result
  }
}
```

