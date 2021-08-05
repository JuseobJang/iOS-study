# Optional Chaining

옵셔널 체이닝은 현재 nil일 수 있는 옵셔널 속성, 메서드 그리고 서브 스크립트를 조회 하고 호출하기 위한 과정이다. 옵셔널에 값이 포함되어 있으면(nil 값이 아니라면) 호출에 성공한다. 여러개의 쿼리가 함께 연결 될 수 있고 하나의 채인이라도 nil값을 갖는가면 전체 체인이 실패하게 된다.



## Optional Chaining as an Alternative to Force Unwrapping

옵셔널이 nil이 아닌 경우 속성 메서드 서브스크립트를 호출하려는 옵셔널 값 뒤에 `?` 를 붙혀 옵셔널 체이닝을 지정한다. 이것은 옵셔널 값 뒤에 `!` 붙혀 강제 언래핑하는 것과 매우 유사하다. 이 두가지의 차이점은 옵셔널이 nil일 때 옵셔널 체이닝은 실패하는 반면 강제 언래핑은 런타임 에러가 발생한다.

옵셔널 체이닝은 nil 값이 반환될 수 있다는 사실을 표시하기 위해 조회 하는 속성 메서드 서브 스크립트 값이 옵셔널이 아니더라도 항상 옵셔널 값을 반환한다. 또한 이러한 성질을 이용하여 옵셔널 반환 값으로 옵셔널 체이닝이 호출 성공 했는지 실패 했는지 확인 가능 하다.

```swift
class Person {
  var residence: Residence?
}

class Residence {
  var numberOfRooms = 1
}

let john = Person() // residence 값은 nil 이다
let roomCount = john.residence!.numberOfRooms // 여기서 강제 언래핑을 수행하면 런터임 에러가 발생한다.

// ! 강제 언래핑 대신 ? 옵셔널 체이닝을 사용하여 접근
if let roomCount = john.residence?.numberOfRooms { // residence 값이 nil이 아니면 numOfRooms 조회
  print("John's residence has \(roomCount) room(s).")
} else { // residence 값이 nil인 경우
  print("Unable to retrieve the number of rooms.") // print
}

// john 인스턴스의 residence값에 Residence 인스턴스 할당
john.residence = Residence()

// residence값이 이제 nil 값이 아님
if let roomCount = john.residence?.numberOfRooms {
  print("John's residence has \(roomCount) room(s).") } // print
else {  
  print("Unable to retrieve the number of rooms.")
}
```



## Defining Model Classes for Optional Chaning

One level deep 이상의 속성 메서드 서브 스크립트를 호출하기 위해 옵셔널 체이닝을 사용할 수 있다. 복잡한 모델 내에서 하위 속성으로 내려 갈 수 있으며 해당 하위 속성의 속성 메서드 서브 스크립트에 접근 가능 한지 확인 가능하다.

```swift
// Person class 안의 하위속성으로 residence가 있고 옵셔널 값이다.
class Person {
    var residence: Residence?
}
```

```swift
class Residence {
  var rooms = [Room]() // stored property
  var numberOfRooms: Int { // computed property
    return rooms.count
  }
  subscript(i: Int) -> Room {
    get {
      return rooms[i]
    }
    set {
      rooms[i] = newValue
    }
  }
  func printNumberOfRooms() {
    print("The number of rooms is \(numberOfRooms)")
  }
  var address: Address? // Optional stored property
}
```

```swift
class Address {
  var buildingName: String?
  var buildingNumber: String?
  var street: String?
  func buildingIdentifier() -> String? {
    if let buildingNumber = buildingNumber, let street = street { // nil값인지 확인
      return "\(buildingNumber) \(street)"
    } else if buildingName != nil {
      return buildingName
    } else {
      return nil
    }
  }
}
```



## Accessing Properties Through Optional Chaining

옵셔널 값의 속성에 접근하고 속성에 접근하는 것이 성공하면 이것을 검사하기 위해 옵셔널 체이닝을 사용할 수 있다. 

새로운 `Person` 인스턴스를 생성하기 위해 위에 정의된 클래스를 사용하고 이전 처럼 `numberOfRooms` 에 접근하고자 한다.

```swift
let john = Person() // Person 인스턴스 생성
if let roomCount = john.residence?.numberOfRooms { // 당연히 john.residence는 nil이다.
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.") // print 
}
```

```swift
let someAddress = Address() // Adress 인스턴스 생성
someAddress.buildingNumber = "29" // 옵셔널인 속성 정의 
someAddress.street = "Acacia Road" // 옵셔널인 속성 정의
// 아직 someAdress.buildingName 정의 하지 않음
john.residence?.address = someAddress // 아직 john.residence 값이 nil 이기 때문에 실패
```

```swift
// Address 인스턴스를 반환하는 함수
func createAddress() -> Address {
    print("Function was called.")

    let someAddress = Address()
    someAddress.buildingNumber = "29"
    someAddress.street = "Acacia Road"

    return someAddress
}
// residence 값이 nil 이기 때문에 우항은 애초에 평가 되지 않는다.
john.residence?.address = createAddress()
//따라서 createAddress()가 실행되지 않기 때문에 "Function was called." 는 출력되지 않는다.
```



## Calling Methods Through Optional Chaining

옵셔널 값의 메서드를 호출하고 메서드 호출이 성공적인지 확인하기 위해 옵셔널 체이닝을 사용할 수 있다. 해당 메서드가 반환값을 정의하지 않아도 사용할 수 있다.

```swift
// Residence class 내부 메서드 ; 반환값이 지정 되어 있지 않음
func printNumberOfRooms() {
    print("The number of rooms is \(numberOfRooms)")
  }
```

```swift
// 함수 호출이 가능한지 불가능한지 옵셔널 채이닝을 통해 판별
if john.residence?.printNumberOfRooms() != nil {
    print("It was possible to print the number of rooms.")
} else {
    print("It was not possible to print the number of rooms.") // print
}

// 값 할당이 가능한지 옵셔널 체이닝을 통해 판별
if (john.residence?.address = someAddress) != nil {
    print("It was possible to set the address.")
} else {
    print("It was not possible to set the address.") // print
}
```



## Accessing Subscripts Through Optional Chaining

옵셔널 값의 서브스크립에서 값을 조회하고 설정하고 해당 서브 스크립트 호출이 성공했는지 확인하기 위해 옵셔널 체이닝을 사용 할 수 있다.

```swift
if let firstRoomName = john.residence?[0].name {
  print("The first room name is \(firstRoomName).")
} else {
  print("Unable to retrieve the first room name.") // print
} 
// john.residence는 nil이므로 else문이 실행된다.

john.residence?[0] = Room(name: "Bathroom") // 마찬가지로 정의를 실패하게 된다.
```



```swift
let johnsHouse = Residence() // 드디어 정의 
johnsHouse.rooms.append(Room(name: "Living Room"))
johnsHouse.rooms.append(Room(name: "Kitchen"))
john.residence = johnsHouse

// john.residence 값 존재
if let firstRoomName = john.residence?[0].name {
    print("The first room name is \(firstRoomName).")
} else {
    print("Unable to retrieve the first room name.")
}
// The first room name is Living Room
```



### Accessing Subscripts of Optional Type

서브 스크립트가 Swift의 Dictionary 타입의 서브 스크립트와 같이 옵셔널 타입의 값을 반하는 경우 옵셔널 반환값을 연결하기 위해 서브스크립트의 닫는 대괄호 뒤에 물음표를 추가한다.

```swift
var testScores = ["Dave": [86, 82, 84], "Bev": [79, 94, 81]]
testScores["Dave"]?[0] = 91
testScores["Bev"]?[0] += 1
testScores["Brian"]?[0] = 72

// "Dave" : [91, 82, 84]
// "Bev" : [80, 94, 81]
// 마지막 Brian은 존재 하지 않으므로 호출 실패 한다.
```



## Linking Multiple Lavels of Chaning

여러 단계의 옵셔널 체이닝을 연결하여 모델 내에서 속성, 메서드, 서브스크립트로 깊게 접근할 수 있다. 그러나 여러 단계의 옵셔널 체이닝은 반환된 값에 더 많은 단계의 옵셔널을 추가 하지 않는다.

- 조회하려는 타입이 옵셔널이 아니면 옵셔널 체이닝 떄문에 옵셔널이된다.
- 조회하려는 타입이 이미 옵셔널이면 옵셔널 체이닝 때문에 더 많은 옵셔널이 추가 되진 않는다.

```swift
if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
// 현재 john.residence는 값이 존재 하지만 address값이 존재 하지 않아 실패 하게 된다.
```

```swift
let johnsAddress = Address()
johnsAddress.buildingName = "The Larches"
johnsAddress.street = "Laurel Street"
john.residence?.address = johnsAddress // johnAddress 추가

if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
// 모든 값이 존재 하므로 "John's street name is Laurel Street."가 출력된다.
```



## Chaining on Methods with Optional Return Values

옵셔널 체이닝은 옵셔널 타입의 값을 반환하는 메서드를 호출하고 필요하다면 메서드의 반환값을 연결하기 위해 사용한다.

```swift
// buildingIdentifier() -> String?
if let buildingIdentifier = 
john.residence?.address?.buildingIdentifier() {
  print("John's building identifier is \(buildingIdentifier).")
}
// nil 이 반환되지 않기 때문에, "John's building identifier is The Larches." 출력

// 메서드 반환값에 대해 옵셔널 체이닝을 수행할 시
if let beginsWithThe =
    john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {
    if beginsWithThe {
        print("John's building identifier begins with \"The\".")
    } else {
        print("John's building identifier does not begin with \"The\".")
    }
}
```

