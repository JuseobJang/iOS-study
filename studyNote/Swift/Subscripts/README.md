# Subscripts

Class, Structure 그리고 Enumeration 은 collection, list 또는 sequence의 요소에 접근할수 있는 단축키인 subscripts를 정의 할 수 있다. 설정과 검색을 위한 별도의 메서드 없이 인덱스로 값을 설정하고 조회하기 위해 서브 스크립트를 사용한다. 

단일 타입을 위한 여러개 서브 스크립트를 정의할 수 있고 적절한 서브 스크립트 오버로드는 서브 스크립트에 전달하는 인덱스 값의 타입에 따라 선택된다. 서브 스크립튼 단일 차원으로 제한되지 않고 여러개의 입력 파라미터로 서브 스크립트를 정의 할 수 있다.



## Subscript Syntax

서브 스크립트를 사용하면 인스턴스 이름 뒤에 대괄호에 하나 이상의 값을 작성하여 인스턴스를 조회 할 수 있다. 이구문은 인스턴스 메서드 구문이나 Computed Ptoperty 구문과 유사하다. `subscript` 키워드를 사용하여 서브스크립트를 정의한다. 또한 인스턴스 메서드와는 달리 Compted Property 와 같은 방법으로 getter & setter를 통해 동작하기 때문에 read-write 뿐만아니라 read-only로 정의 할 수 도 있다.

```swift
subscript(index: Int) -> Int {
  get {
    // Return an appropriate subscript value here.
  }
  set(newValue) { 
    // Perform a suitable setting action here.
  }
}
```

`newValue` 의 타입은 서브스크립트의 반환 값과 동일하다. Computed Property와 마찬가지로 `newValue` 를 명시하지 않아도 setter의 기본 파라미터로 `newValue` 라는 기본 파라미터를 제공한다.

```swift
// read-only 의 경우 중괄호와 getter, setter에 대한 명시를 생략 할 수 있다.
subscript(index: Int) -> Int {
  // Return an appropriate subscript value here.
}
```

Example

```swift
struct TimesTable {
  let multiplier: Int
  subscript(index: Int) -> Int {
    return multiplier * index
  }
}
let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is \(threeTimesTable[6])")
// Prints "six times three is 18"
```



## Subscript Usage

**서브스크립트** 의 정확한 의미는 사용되는 컨텍스트에 따라 다르다. 서브 스크립트는 콜렉션, 목록, 또는 시퀀스의 요소에 접근하는 바로가기의 역할로 사용된다. 특정 클래스 또는 구조체의 기능에 가장 적합한 방식으로 서브스크립트를 자유롭게 구현 할 수 있다.

예를들어, swift의 `Dictionary` 타입은 `Dictionary` 인스턴스에 저장된 값을 설정하고 조회하기 위한 서브스크립트를 구현한다. 서브스크립트 대괄호 내에 딕셔너리의 키값을 넣고 딕셔너리의 밸류 값을 서브스크립트에 할당하여 딕셔너리에 값을 설정할 수 있다.

```swift
var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
numberOfLegs["bird"] = 2
```



## Subscript Options

서브 스크립트는 여러개의 입력 파라미터를 가질 수 있고 입력 파라미터는 어떤 타입도 가능하며 어떤 타입도 반환 할 수 있다. 대신 함수와 다르게 `inout` 파라미터를 사용할 수는 없다.

서브스크립트는 필요한 값의 타입에 따라서 적절한 서브스크립트를 제공할 수 있다. 이러한 여러개의 서브 스크립트 정의를 **subscript overloading** 이라 한다.

```swift
struct Matrix {
  let rows: Int, columns: Int
  var grid: [Double]
  init(rows: Int, columns: Int) {
    self.rows = rows
    self.columns = columns
    grid = Array(repeating: 0.0, count: rows * columns)
  }
  
  func indexIsValid(row: Int, column: Int) -> Bool {
    return row >= 0 && row < rows && column >= 0 && column < columns
  }
  
  subscript(row: Int, column: Int) -> Double {
		// row, column 의 값이 적절한지 판단하기 위한 assert추가
    get {
      assert(indexIsValid(row: row, column: column), "Index out of range")
      return grid[(row * columns) + column]
    }
    set {
      assert(indexIsValid(row: row, column: column), "Index out of range")
      grid[(row * columns) + column] = newValue
    }
  }
}
```

```swift
var matrix = Matrix(rows: 2, columns: 2) // [[0.0, 0.0], [0.0, 0.0]]
```

```swift
// 정의한 subscript를 사용하여 Matrix 인스턴스내의 요소를 설정
matrix[0, 1] = 1.5
matrix[1, 0] = 3.2
```



## Type Subscripts

타입 자체에서 호출되는 서브스크립트 또한 정의할 수 있다. 이런 종류의 서브스크립트를 **타입 서브스크립트** 라고한다. `subscript` 키워드 이전에 `static` 키워드를 사용하여 나타낸다. 클래스의 경우에는 하위 클래스가 상위 클래스의 서브스크립트 구현읠 재정의 할수 있게 `class` 라는 키워드를 사용할 수있다. 

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
    static subscript(n: Int) -> Planet {
        return Planet(rawValue: n)!
    }
}
let mars = Planet[4]
print(mars)
```