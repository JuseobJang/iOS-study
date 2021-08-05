# Nested Types

Enumerations 는 특정 클래스 또는 구조체의 기능을 지원하기 위해 생성된다. 유사하게 더 복잡한 타입의 컨텍스트 내에서 사용하기 위해 순수하게 유틸리티 클래스와 구제체를 정의하는 것이 편리 할 수 있다. 이를 위해 Swift는 Nested Types를 정의 할 수 있다. 타입의 정의 내에서 enumerations, class, structure를 중첩 할 수 있다.



## Nested Types in Action

```swift
// 블랙잭 카드 구조체
struct BlackjackCard {

  // nested Suit enumeration
  enum Suit: Character {
    case spades = "♠", hearts = "♡", diamonds = "♢", clubs = "♣"
  }

  // nested Rank enumeration
  enum Rank: Int {
    case two = 2, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king, ace
    
    struct Values {
      let first: Int, second: Int?
    }
    var values: Values {
      switch self {
        case .ace:
        return Values(first: 1, second: 11)
        case .jack, .queen, .king:
        return Values(first: 10, second: nil)
        default:
        return Values(first: self.rawValue, second: nil)
      }
    }
  }

  // BlackjackCard properties and methods
  let rank: Rank, suit: Suit
  
  var description: String {
    var output = "suit is \(suit.rawValue),"
    output += " value is \(rank.values.first)"
    if let second = rank.values.second {
      output += " or \(second)"
    }
    return output
  }
}
```



```swift
let theAceOfSpades = BlackjackCard(rank: .ace, suit: .spades)
print("theAceOfSpades: \(theAceOfSpades.description)")
// Prints "theAceOfSpades: suit is ♠, value is 1 or 11"
```

## Reffering to Nested Types

정의된 컨텍스트 외부에서 중첩된 타입을 사용하기 위해서는 해당이름에 중첩된 타입의 이름을 접두사로 붙인다.

```swift
let heartsSymbol = BlackjackCard.Suit.hearts.rawValue
// heartsSymbol is "♡"
```

