# Structures and Classes

Structures & Classes 는 코드 블록으로 구성되는 유연한 구조이다. 상수나 변수를 선언하는 것과 같은 방식으로 Structures & Classes 안에 속성과 메서드를 정의할 수 있다. 

다른 프로그래밍 언어과 다르게 Swift는 커스텀 structures & classes 를 만드는데 분리된 interface 및 implements 파일을 요구하지 않는다. Swift에서 structures & classes를 단일 파일에 정의하면 해당 structure 또는 class 에 대한 외부 인터페이스를 다른 코드가 사용할 수 있도록 자동으로 설정된다.



## Comparing Structures and Classes

Swift의 Structures & Classes 공통점

- 값을 저장할 속성을 정의
- 기능을 제공하는 메서드 정의
- Subscripts 문법을 사용하여 값에 접근 할 수 있도록 하는 subscripts 정의
- 초기상태를 세팅하기 위한 initializers 정의
- 기본적인 구현 이상으로 기능을 확장가능
- 특정한 표준 기능을 제공하기 위한 프로토콜 준수

Swift의 Structure & Classes 차이점(Class 의 추가적인 기능)

- 상속을 사용하여 다른 클래스의 특성들을 상속 받을 수 있다.
- Type casting을 사용할 수 있어서 클래스 인스턴스에 대해서 런 타임시 타입을 체크하고 해석할 수 있다.
- Deinitializer를 사용하여 할당된 리소스들을 해제 할 수 있다.
- Reference counting를 허용하여 클래스 인스턴스에 대해서 참조를 두개 이상도 허용 된다.

Classes가 지원하는 추가적인 기능들을 복잡성을 증가 시킬 수 있기 때문에 일반적으론 더 쉬운 structures를 더 선호 하지만 적절하게 필요할 땐 classes를 써야만 한다.



### Definition Syntax

```swift
// structure 정의
struct Resolution {
    var width = 0 
    var height = 0
}

// class 정의
class VideoMode {
    var resolution = Resolution() // Resolution Structure 인스턴스를 속성으로 가짐
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```



### Structure and Class Instances

```swift
// Structures & Classes instance 생성
let someResolution = Resolution()
let someVideoMode = VideoMode()
```



### Accessing Properties

```swift
print("The width of someResolution is \(someResolution.width)") // The width of someResolution is 0

print("The width of someVideoMode is \(someVideoMode.resolution.width)") // The width of someVideoMode is 0
```

```swift
someVideoMode.resolution.width = 1280 // width 값 변경
print("The width of someVideoMode is now \(someVideoMode.resolution.width)") // The width of someVideoMode is now 1280
```



### Memberwise Initializers for Structure Types

모든 structures에는 자동으로 생성된 memberwise initializer가 있으며, 이를 사용하여 새로운 인스턴스의 멤버 속성을 초기화할 수 있다. 새 인스턴스의 속성에 대한 초기 값은 이름으로 memberwise initializer에 전달할 수 있다.

```swift
let vga = Resolution(width: 640, height: 480)
```



## Structures and Enumerations Are Value Types

Value Type은 변수나 상수에 할당 되거나 함수에 전달 될 때 복사되어지는 타입이다. 

실제로 Swift의 기본적인 타입(integer, floating-point numbers, booleans, strings, arrays, dictionaries)는 Value Type이다.

모든 structures 와 enumerations느 Value Type 이다. 이것은 생성한 어떠한 structure 와 enumeration instance 라도 항상 전달 될 때 복사 되어진다는 것이다.

```swift
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd

cinema.width = 2048

print("\(cinema.width)")
// 2048

print("\(hd.width)")
// 1920 cinema는 hd가 복사되어 할당 된것이므로 cinema.width가 변경된다고 hd.width가 변경 되지는 않는다.
```

```swift
enum CompassPoint {
    case north, south, east, west
    mutating func turnNorth() {
        self = .north
    }
}
var currentDirection = CompassPoint.west
let rememberedDirection = currentDirection
currentDirection.turnNorth()

print("The current direction is \(currentDirection)")
print("The remembered direction is \(rememberedDirection)")
// Prints "The current direction is north"
// Prints "The remembered direction is west"
// enumeration도 마찬가지로 currentDirection을 rememberedDirection에 할당할 때 Value Type이기 때문에 복사되어 할당 된다. 
```



## Classes Are Reference Types

Value Type과 다르게 Reference Type은 변수나 상수에 할당 되거나 함수에 전달 될 때 복사되는 것이 아니라 같은 인스턴스를 참조하여 사용하게 된다.

```swift
// tehnEighy 라는 VideoMode class의 instance 생성 및 값 설정
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0
```

```swift
// alsoTenEighty 에 tenEighty 할당 (같은 instance 참조)
let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0
```

```swift
// alsoTenEighty의 frameRate 값을 변경 했지만 같은 instance를 참조 하기 때문에 tenEighty.framRate를 출력했을 때 값이 변한 것을 알 수 있음
print("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
//"The frameRate property of tenEighty is now 30.0
```



### Identify Operators

Classes는 reference type이기 때문에 여러 변수나 상수가 같은 instance를 참조하고 있을 수 있다. 해당 연산자는 이러한 변수나 상수가 같은 instance를 참조하고 있는지 판별 할 수 있다.

- Identical to : ===
- Not identical to : !==

```swift
// 두 변수는 같은 (클래스)인스턴스를 참조하고 있기 때문에 해당 프린트 문이 출력됨
if tenEighty === alsoTenEighty {
    print("tenEighty and alsoTenEighty refer to the same VideoMode instance.")
}
```













