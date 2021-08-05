# Type Casting

타입 캐스팅이란 인스턴스의 타입을 확인하거나 해당 인스턴스를 클래스 계층구조의 다른 계층의 상위클래스 또는 하위 클래스로 취급하는 방법이다. 

Swift에서 타입 캐스팅은 `is` 그리고 `as` 연산자로 구현된다. 이 두가지 연산자는 값의 타입을 확인하거나 값을 다른 타입으로 캐스트 하는 방법을 제공한다.

## Defining a Class Hierachy for Type Casting

클래스와 하위 클래스의 계층도와 함께 타입 캐스팅을 사용하여 특정 클래스 인스턴스의 타입을 확인하고 같은 계층 내에서 다른 클래스로 캐스트 할 수 있다. 

```swift
// 기본 클래스
class MediaItem {
  var name: String
  init(name: String) {
    self.name = name
  }
}

// 기본클래스인 MediaItem을 상속받은 Movie와 Song(하위 클래스)
class Movie: MediaItem {
  var director: String
  init(name: String, director: String) {
    self.director = director
    super.init(name: name)
  }
}

class Song: MediaItem {
  var artist: String
  init(name: String, artist: String) {
    self.artist = artist
    super.init(name: name)
  }
}
```

```swift
let library = [
    Movie(name: "Casablanca", director: "Michael Curtiz"),
    Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
    Movie(name: "Citizen Kane", director: "Orson Welles"),
    Song(name: "The One And Only", artist: "Chesney Hawkes"),
    Song(name: "Never Gonna Give You Up", artist: "Rick Astley")
]
```



## Checking Type

인스턴스가 특정 하위 클래스 타입인지 확인하기 위해서 `is` 를 사용한다.

```swift
var movieCount = 0
var songCount = 0

// type이 Movie인지 Song인지 판별하여 갯수 카운트
for item in library {
  if item is Movie {
    movieCount += 1
  } else if item is Song {
    songCount += 1
  }
}

print("Media library contains \(movieCount) movies and \(songCount) songs")
// Prints "Media library contains 2 movies and 3 songs"
```



## Down Casting

특정 클래스 타입의 상수 또는 변수는 하위클래스의 인스턴스를 참조할 수 있다. 이러한 경우 타입 캐스트 연산자 `as?` 또는 `as!` 를 사용하여 하위클래스 타입으로 다운 캐스트 할 수 있다.

다운 캐스팅은 실패 할 수 도 있으므로 타입 캐스트 연산자는 2가지 형태로 제공된다. `as?` 의 경우 다운캐스트 할려고 할 때 타입의 옵셔널 값을 반환한다. `as!` 은 다운 캐스트를 시도하고 강제 언래핑한다.

다운 캐스트를 성공할 확신이 없다면 `as?` 를 사용한다. 이 연산자는 항상 옵셔널 값을 반환하고 다운캐스트 불가능 하면 nil을 반환한다. 이를 이용하여 다운 캐스트 성공여부를 체크 할 수 있다.

만약 다운 캐스트를 성공할 자신이 있다면 `as!` 를 사용하여 강제 언래핑하고 만약 유효하지 않은 타입으로 다운캐스팅 할 시 런타임 에러를 발생하게 된다.

```Swift
// library 타입은 [MediaItem] 이다. 
for item in library {
  if let movie = item as? Movie { // item을 Movie로 다운캐스팅 할 수 있다면
    print("Movie: \(movie.name), dir. \(movie.director)")
  } else if let song = item as? Song { // item을 Song으로 다운캐스팅 할 수 있다면
    print("Song: \(song.name), by \(song.artist)")
  }
}
```



## Type Casting for Any and AnyObject 

Swift는 비특정 타입 작업을 위해 2가지 특별한 타입을 제공한다.

- Any는 함수타입을 포함하여 모든 타입의 인스턴스를 나타 낼 수 있다.
- AnyObject는 모든 클래스 타입의 인스턴스를 나타낼 수 있다.

```swift
var things = [Any]()

// things 배열안에 어떤 타입의 값이든 들어 올 수 있다.
things.append(0)
things.append(0.0)
things.append(42)
things.append(3.14159)
things.append("hello")
things.append((3.0, 5.0))
things.append(Movie(name: "Ghostbusters", director: "Ivan Reitman"))
things.append({ (name: String) -> String in "Hello, \(name)" })
```

```swift
// Any 타입을 타입 캐스팅
for thing in things {
    switch thing {
    case 0 as Int:
        print("zero as an Int")
    case 0 as Double:
        print("zero as a Double")
    case let someInt as Int:
        print("an integer value of \(someInt)")
    case let someDouble as Double where someDouble > 0:
        print("a positive double value of \(someDouble)")
    case is Double:
        print("some other double value that I don't want to print")
    case let someString as String:
        print("a string value of \"\(someString)\"")
    case let (x, y) as (Double, Double):
        print("an (x, y) point at \(x), \(y)")
    case let movie as Movie:
        print("a movie called \(movie.name), dir. \(movie.director)")
    case let stringConverter as (String) -> String:
        print(stringConverter("Michael"))
    default:
        print("something else")
    }
}

// zero as an Int
// zero as a Double
// an integer value of 42
// a positive double value of 3.14159
// a string value of "hello"
// an (x, y) point at 3.0, 5.0
// a movie called Ghostbusters, dir. Ivan Reitman
// Hello, Michael
```

