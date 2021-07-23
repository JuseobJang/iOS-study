# Closures

Closures 는 일반적으로 다른 프로그래밍 언어에서 사용되는 lamda와 비슷한 개념이다.

Global & Nested Functions는 실제로 넓은 의미의 Clousres의 특수한 케이스이다.

1. Global Functions : 이름이 존재하고 어떠한 값도 흭득하지 않는 함수
2. Nested Functions : 이름이 존재하고 함수 내부의 값을 흭득할 수 있는 함수

3. Closures : 이름이 없고 주변 문맥에 따라 함수 내부의 값을 흭득 할 수 있는 문법적으로 축약된 표현

Closures는 간결하고 깔끔한 구문을 작성할 수 있도록 최적화된 명확한 스타일을 가지고 있다

- Inferring parameter and return value types from context
- Implicit returns from single-expression closures
- Shorthand argument names
- Trailing closure syntax



## Clousres Expressions

### The Sorted Method

```swift
let names = ["Chris","Alex","Ewa","Barry","Daninella"]
```

```swift
func desc(_ s1: String, _ s2: String) -> {
  return s1 > s2
}

var descNames = names.sorted(by: backward) // by 는 (String, String) -> Bool 인 Function type을 넣어 주어야함
```



### Closure Expression Syntax

```
{(parameters) -> return type in
		statements
} 
```

```swift
var descNames = names.sorted(by: {(s1: String, s2: String) -> Bool in
                                 return s1 > s2})
```



### Inferring Type From Context

(String, String) -> Bool 라는 function type은 이미 이전에 명시가 되어있기 때문에 생략하고 closure를 작성해도 추론이 가능하다.

```Swift
var descNames = names.sorted(by: {s1, s2 in return s1 > s2})
```



### Implicit Returns from Single-Expression Closures

한줄로 표현가능한 clousure는 'return'을 생략 해주어도 알아서 반환이 된다.

```swift
var descNames = names.sorted(by: {s1, s2 in s1 > s2})
```



### Shorthand Argument Names

$0, $1, $2 ... 를 사용하여 순서에 맞게 매개변수로 들어오는 파라미터를 표현할 수 있다. 

```swift
var descNames = names.sorted(by {$0 > $1})
```



## Trainling Closures

함수의 마지막 인자가 Clousure일 때 함수의 마지막에 Closure를 표현하느 Trailing Closures를 사용 가능 하다.

```swift
func someNeedClosure(closure: () -> Void) // 인자의 마지막이 closure

// General Closure
someNeedClosure(closure: { 
	// code
})

// Trailing Closure1
someNeedClosure(){
  // code
}

// Trailing Closure2 
someNeedClosure{ // ()에 인자가 따로 없기 때문에 ()도 생략가능
  // code
}

// Exmaple
var descNames = names.sorted{$0 > $1}
```



```swift
func loadPicture(from server: Server, completion: (Picture) -> Void, onFailure: () -> Void) // copletion, onFailure closure를 인자로 받음 
{ 
    if let picture = download("photo.jpg", from: server) {
        completion(picture) // 성공시 completion 실행
    } else {
        onFailure() // 실패시 onFailure 실행
    }
}


loadPicture(from: someServer) { picture in
    someView.currentPicture = picture // trailing closure 를 사용하여 첫번째 Closure인 completion 코드 작성
} onFailure: { // 두번째 closure 부터는 이름을 명시해주어야 함.
    print("Couldn't download the next picture.")
}
```



## Capturing Values

Closeure는 정의된 주변 컨텍스트의 상수와 변수를 캡쳐 할 수 있다. 원래의 상수나 변수가 사라져도 closure안에 남아서 그 값을 다시 활용 할 수 있다.

```Swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount // runningTotal caturing : runningTotal 다시 활용 가능
        return runningTotal
    }
    return incrementer
}


let incrementByTen = makeIncrementer(forIncrement: 10) // 0 부터 10씩 증가
let incrementBySeven = makeIncrementer(forIncrement: 7) // 0부터 7 씩 증가

incrementByTen() // 10 
incrementByTen() // 20
incrementByTen() // 30 내부의 runningTotal 값은 사라지지 않고 계속 갱신 되고 있다.

incrementBySeven() // 7
incrementBySeven() // 14
incrementBySeven() // 21 incrementByTen()과 다른 incrementer이기 때문에 다른 runningTotal을 사용한다.
```



## Closures Are Refernce Types

Closure는 reference type이기 때문에 다른 변수에 할당 시 해당 closure의 주소 값을 가르키기 때문에 결과적으로 같은 capturing value를 사용한다고 할 수 있다.

```swift
// 이전에 runningTotal이 30까지 증가된 상태
let alsoIncrementByTen = incrementByTen // refence type이기 때문에 같은 runningTotal을 사용한다.
alsoIncrementByTen() // 40
incrementByTen() // 50
```



## Escaping Closures

Closure 매개 변수 앞에 **@escaping**을 붙이 므로서 Escaping Closure를 사용할 수 있다. Escaping Closure는 말그래도 해당 함수 밖에서 해당 Closure를 사용하겠다는 것이다. 이렇게 Closeure를 함수 밖에서 사용한다는 것은 해당 함수가 완전히 종료 된 이후에 해당 Closure가 실행 된다는 것인데 이것은 통신과 같은 비동기적인 작업을 할 때 유용하게 사용 가능 하다.

```swift
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler) // 해당 closure를 함수 밖에 있는 completeHandlers에 추가 해주기 때문에 escaping을 사용해야 한다.
}
```













