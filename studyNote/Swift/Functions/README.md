# Functions

## Defining & Calling Functions

```Swift
func greeting(person: String) -> String{ //함수 선언
  let greeting = person + ", hello!"
  return greeting 
}

print(greeting(person: "Juseob")) // Juseob, hello!
```



## Function Parameters and Return Value

### Functions Without Parameters

```Swift
func greeting() -> String { // 매개변수가 존재하지 않아도됨
  return "Hello!"
}
print(greeting()) // Hello!
```



### Functions With Multiple Parameters

```Swift
func greet(person: String, alreadyGreeted: Bool) -> String { // 두 개의 매개 변수 존재
    if alreadyGreeted { 
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true)) // Hello, againg, Tim!
```



### Functions Without Return Values

```Swift
func printGreeting(person: String){ // return value가 존재 하지 않아도 됨, Void type
  print("Hello!, \(person)") 
}
printGreeting("juseob") // Hello!, juseob
```



###  Functions with Multiple Return Values

```Swift
func minMax(array: [Int]) -> (min: Int, max: Int) { // return 될 tuple의 변수 이름 지정
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax) // 여러 값을 리턴하기 위해 tuple을 리턴
}

let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)") // 함수 선언시 tuple의 각값에 이름을 지어 줬기 때문에 해당 이름 으로 참조 가능
```



### Functions With an Implicit Return

```Swift
func greeting(for person: String) -> String {
    "Hello, " + person + "!" // function이 한줄로 표현이 가능하다면 'return'을 생략 할 수 있다.
}
print(greeting(for: "jsueob")) //Hello, juseob!
```



## Function Argument Labels & Parameters Names

```swift
func something(param1: Int, param2: Int){ // parameter name 명시
  // code 
}
somthing(param1: 10, param2: 20) // parameter name으로 매개변수 전달
```



### Specifying Argument Labels

```Swift
func something(one param1:Int, two param2: Int){ // argument label 명시
  print(param1 + param2) // 함수 내에서는 parameter name 사용
}
something(one: 1, two: 2) // argument label 지정시 해당 label로 변수를 전달
```



### Omitting Argument Labels

```Swift
func something(_ param1: Int, _ param2: Int){ // _ 사용하여 argument label 표현
  // code
}
something(1,2) // _ 사용시 label을 명시하지 않고 변수를 전달 가능
```



### Default Parameter Value

```swift
func something(paramWithDefault: Int = 10){
  print(parmaWithDefault)
}
somthing() // 10
somthing(20) // 20
```



### Variadic Parameters

```swift
func sum(_ numbers: Double...) -> Double { // ... 으로 연속된 값이 들어 올 수 있음 을 표현
  var total: Double = 0
  for num in numbers { // 실제로 numbers는 Array<Double> 타입을 갖게 됨
    total + num
  }
  return total
}

sum(2.1, 3.5, 5.8) // 11.4
```



### In-Out Parameters

보통 함수의 인자로 받은 매개변수는 함수 내에서 상수(let)이기 때문에 값을 변경하는 것이 불가능 하다. 하지만 해당 매개변수를 변경하고 값을 유지 하기 위해서 In-Out Parameters를 사용 할 수 있다.

```swift
func swap(_ a: inout Int, _ b: inout Int){ // inout parameter 사용
  let temp = a
  a = b // 값을 변경 가능
  b = temp
}
var num1 = 100
var num2 = 200
swap(&num1, &num2) // inout paramter는 함수 사용시 앞에 & 를 붙여 줘야한다.
print("num1: \(num1), num2: \(num2)") // num1: 200, num2: 100
```



## Function Types

모든 함수는 매개변수 타입과 어떤 타입을 반환해야 할지를 갖고 있는데 이것을 묶어서 함수 타입이라고 한다. 

```Swift
func add(_ num1: Int, _ num2: Int) -> Int {
  return num1 + num2
}

func printHello(){
  print("hello")
}
```

만약 이러한 함수들이 있다면 각각의 Function Type은 **(Int, Int) -> Int, ( ) -> Void** 라고 말 할 수 있다.



### Using Function Types

```Swift
func add(_ num1: Int, _ num2: Int) -> Int {
  return num1 + num2
}

var mathFunc: (Int, Int) -> Int = add // 이런 식으로 함수 타입을 명시 하고 함수를 변수에 할당 가능 하다 + 물론 타입을 명시해주지 않아도 타입 추론도 가능하다.

mathFunc(1,3) // 4
mathFunc(2,5) // 7
```



### Function Types as Parameter Type

함수의 파라미터로 Function을 Function Type을 명시해주고 매개변수로 전달할 수 있다.

```swift
func add(_ num1: Int, _ num2: Int) -> Int {
  return num1 + num2
}

func printAdd(_ mathFunc:(Int, Int) -> Int, num1: Int, num2: Int ){ 
  print(mathFunc(num1, num2))
}

printAdd(add, num1: 3, num2: 6) // 9 // 함수를 매개변수로 전달
```



### Function Type Return Types

리턴 타입으로 Function Type을 사용할 수 있다.

```swift
func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}

func chooseStepFunction(backward: Bool) -> (Int) -> Int { // (Int) -> Int function type 리턴
    return backward ? stepBackward : stepForward
}
```



## Nested Functions

Function 안에 간단한 Function을 선언하여 사용할 수 있다.

```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}
```















