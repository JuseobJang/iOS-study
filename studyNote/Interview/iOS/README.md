# iOS Develop

## Interview List

- [Bounds 와 Frame 의 차이점을 설명하시오.](#bounds-와-frame-의-차이점을-설명하시오)

- [실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.](#실제-디바이스가-없을-경우-개발-환경에서-할-수-있는-것과-없는-것을-설명하시오)
- [앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?](#앱의-콘텐츠나-데이터-자체를-저장보관하는-특별한-객체를-무엇이라고-하는가)
- [앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?](#앱-화면의-콘텐츠를-표시하는-로직과-관리를-담당하는-객체를-무엇이라고-하는가)
- App thinning에 대해서 설명하시오.
- 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?
- @Main에 대해서 설명하시오.
- 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?
- 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.
- 앱이 In-Active 상태가 되는 시나리오를 설명하시오.
- scene delegate에 대해 설명하시오.
- UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?
- App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.
- NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.
- GCD API 동작 방식과 필요성에 대해 설명하시오.
- Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.
- iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가?
- Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.
- Delegate란 무언인가 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.
- NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
- UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?
- App Bundle의 구조와 역할에 대해 설명하시오.
- 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?
- 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.
- View 객체에 대해 설명하시오.
- UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.
- UIWindow 객체의 역할은 무엇인가?
- UINavigationController 의 역할이 무엇인지 설명하시오.
- TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.
- 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.
- setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.
- NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.
- URLSession에 대해서 설명하시오.
- prepareForReuse에 대해서 설명하시오.
- 다크모드를 지원하는 방법에 대해 설명하시오.

## Bounds 와 Frame 의 차이점을 설명하시오.

- **Frame** : superview의 좌표계를 기준으로 해당 view가 위치하는 location 과 size를 나타내는 속성이다.(superview는 **한 단계** 상위뷰를 의미)
- **Bounds** : 자기 자신의 좌표계를 기준으로 location 과 size를 나타내는 속성이다.

Location :

- Frame 의 경우 superview의 왼쪽 상단을 기준으로 해당 view의 왼쪽 상단과 x축, y축 으로 만큰 떨어진 값으로 계산된다.

- Bounds의 경우에는 superview 상관없이 자기 자신만의 좌표계를 갖기 때문에 origin 은 항상 (0, 0) 이다.

Size :

​	사이즈의 두 속성 모두 동일하다고 생각할 수 있고 일반적으로는 그러하다.

​	하지만 만약 뷰가 회전된 상태라고 한다면, 

​	Frame은 상위 뷰와 x축, y축으로 평행하게 해당 뷰를 감쌀 수 있는 틀의 사이즈를 나타내고 Bounds의 경우에는 회전 되기 전의 자체 뷰 사이즈를 갖는다.

**어떤상황에 무엇을 사용하는가?**

- Frame 의 경우 일반적위 View의 위치나 크기를 설정 할 때 사용한다.
- Bounds 의 경우 내부에 그림을 그리거나, transformation 후 view의 크기를 알고 싶을 때 등 내부적으로 변경하는 경우에 사용

> Bounds 의 origin x, y 를 변경하면 superview가 움직이는 것 처럼 보이는 현산은 superview의 frame이 변하는 것이 아니라, subview들을 그리는 좌표계의 기준이 달라지기 때문이다.

[Reference] 

https://sihyungyou.github.io/iOS-frame-bounds/



## 실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.

**하드웨어**

- 가속도, 가압계, 주변광, GPS 센서 기능을 이용할 수가 없다.
- 마우스로 시뮬레이터를 터치하기 때문에 두 손가락으로 동작하는 줌인 줌아웃 등의 기능을 사용할 수 없다.
- 카메라를 지원하지 않는다.
- 마이크를 지원하지 않는다.
- 전화 기능을 사용 할 수 없다.

**API**

- Apple의 푸시 알림 받기와 보내기를 지원하지 않는다.
- 사진, 연락처, 캘린더에 액세스하기 위해 개인정보 보호 알림을 지원하지 않는다.
- Handoff 기능을 지원하지 않는다.
- MessageUI 기능을 지원하지 않는다.

**ETC**

- 맥의 성능이 아이폰의 성능보다 훨씬 뛰어나기 때문에 실제 CPU나 메모리 부담이 얼마나 되는지 정확히 파악 할 수 없다.
- 네트워크 속도 테스트를 할 수 없다.
- 페이스 아이디로 직접 얼굴 인식은 할 수 없지만, 인식이 됐는지 않됐는지 처리는 가능 하다.

[Reference] 

[fomaios 티스토리 포스팅](https://fomaios.tistory.com/entry/%EC%8B%A4%EC%A0%9C-%EB%94%94%EB%B0%94%EC%9D%B4%EC%8A%A4%EA%B0%80-%EC%97%86%EC%9D%84-%EA%B2%BD%EC%9A%B0-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EA%B2%83%EA%B3%BC-%EC%97%86%EB%8A%94-%EA%B2%83)



## 앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?

*Archive*(아카이브) 란? 객체의 아카이빙이란 그 객체의 프로퍼티를 모두 기록하고 파일 시스템에 그 내용을 저장한다는 뜻

**UserDefault**

- Key-value 쌍으로 디바이스에 데이터를 저장하는 기능을 제공하는 인터페이스
- 주로 앱의 설정 값을 저장하고 나중에 읽기 위해 사용
- 스위프트에서 제공하는 기본 데이터 타입이면 별도의 작업 없이 저장 가능

**NSCoding** (저장 하기 위한 클래스는 해당 프로토콜을 준수해야함)

- NSKeyedArchiver, NSKeyedUnarchiver 등 하위 구현체를 사용
- `func encode(with aCoder: NSCoder)` : 인코딩을 하기 위한 메서드
- `required init?(coder aDecoder: NSCoder)` : 디코딩 하기 위한 메서드

[Reference/ Example] 

https://jinios.github.io/ios/2018/03/30/archive/



## 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?

**VIewController** : 앱 구조의 뼈대, 모든 앱에 반드시 하나 이상의 view controller로 이루어져 있다.

### Responsibility

1. View Hierarchical Management 

   모든 ViewController 마다 root view 를 지니며 화면에 표시하기 위해서는 해당 root view 내에 속해야 한다.

   [View Controller 종류]

   - Content View Controller : 모든 뷰를 단독으로 관리하는 뷰 컨트롤러

     Ex) UIViewController, UITableViewController, UICollectionViewController...

   - Container View Controller : 자체 뷰 뿐만 아니라 하나 이상의 자식 뷰 컨트롤러를 가진 루트뷰를 관리, 컨테이너는 컨텐츠를 관리하는 것이 아니라 컨테이너 내의 루트 뷰만 관리

     Ex) UINavigationController, UITabbarController, UIPageViewController...

2. 뷰에서 일어나는 User Interaction 을 받음

   View에서 일어나는 모든 사용자 이벤트는 View Controller가 각 View에 따라 관련 action 메서드나 Delegate를 통해 처리

3. Resource Management

   ViewController 가 생성한 모든 뷰와 객체들은 ViewController에게 책임이 있다.

   LifeCycle에 따라 생성되었다가 자동을 소멸 되기도 하지만 ARC 개념에 맞게 관리가 필요하다.

   메모리 부족시 *didReceiveMemoryWarning* 메서드에서 필수적으로 유지하지 않아도 되는 메모리 정리



### Life Cycle

<details>
<summary>Init(coder: )</summary>
<p>
스토리보드를 사용하여 뷰 컨트롤러를 초기화 하는 경우
</p>
</details>

<details>
<summary>Init(nibName: bundel: ) </summary>
<p>
스토리보드가 아닌 .nib 파일로 뷰 컨트롤러를 초기화 하는 경우
</p>
</details>

<details>
<summary>loadView( ) </summary>
<p>
본격적으로 화면에 띄어질 View를 만드는 메서드, outlet과 action이 메서드에서 생성 되고 연결 
</p>
</details>

<details>
<summary>viewDidLoad() </summary>
<p>
모든 outlet들은 메모리에 위치하고 있음 그러므로 화면이 보여지기 전 데이터를 뿌려주는 행위에 대한 코드를 작성 이 메서드는 뷰 컨트롤러 생명주기에서 오로지 <b>한번만 호출</b> 되기 때문에 오로지 한번만 일어날 행위들을 정의
</p>
</details>

<details>
<summary>viewWillAppear( )</summary>
<p>
화면이 올라오고 난 이후에 호출되는 메서드, 애니메이션 실행, 비디오, 소리를 재생하는 행위 그리고 데이터 업데이트를 수행 , 화면 전환을 통해 현재의 화면으로 돌아올때 viewWillAppear( ) 실행
</p>
</details>

<details>
<summary>viewDidAppear(_: )</summary>
<p>
뷰와 데이터와 함께 완전히 화면에 나타난 후 호출되는 메서드
</p>
</details>

<details>
<summary>didReceiveMemoryWarning()</summary>
<p>
iOS 기기들은 제한된 메모리 크기와 전원을 갖고 있음, 메모리가 채워지기 시작하면 일반적인 컴퓨터의 운영체제와는 다르게 메모리가 부족하면 메모리의 데이터를 하드디스크로 옮기는 작업을 하지 않음
<br>
<br>
>어플리케이션의 메모리 사용량을 줄여야하는 책임, 어플리케이션이 너무 많은 메모리를 사용한다면 iOS는 이를 알리게 됨
<br>
<br>
>View Controller가 자원 관리를 하고 있는 동안 이러한 알람들은 이 메소드를 통해 그들에게 전달 
<br>
<br>
이러한 방식으로 여러분은 몇몇의 메모리를 해지하는 등의 행동을 취할 수 있음, 
이러한 경고 알림을 무시하고 여러분의 어플리케이션의 메모리 사용량이 일정 한계치를 넘어가게 된다면 iOS는 여러분의 어플리케이션을 강제로 끝내게 됨, 반드시 피해야 함!
</p>
</details>

<details>
<summary>viewWillDisappear(_:)</summary>
<p>
다음 View Controller로 화면이 전환되기 전, Original View Controller가 화면에서 사라질 때 이 메소드가 호출 
이 시점에서 해야할 일반적인 작업들은 거의 없기 때문에 굳이 override 할 필요는 없음
</p>
</details>

<details>
<summary>viewDidDisappear(_:)</summary>
<p>
View Controller들이 화면에서 사라지고 나서 이 메소드가 호출됨
<br>
<br>
화면에서 View Controller가 사라진 이후에는 멈추어야할 작업들 이 메소드를 override하여 작성할 수 있음 
<br>
<br>
예를 들어 notification을 듣는 행위를 멈추기, 다른 객체의 속성을 observing하는것을 멈추기, 디바이스의 센서를 점검하거나 네트워크를 호출하는 행위 등을 멈춤
</p>
</details>

<details>
<summary>deinit()</summary>
<p>
다른 모든 객체와 마찬가지로 View Controller가 메모리에서 사라지기 전 이 메소드가 호출됩니다. 대개 여러분은 이 메소드를 할당 받은 자원 중 ARC에 의해 해지가 불가능한 자원들을 해제하기 위해 재정의 할 수 있다. 또한 백그라운드에서 돌리기 위해 이전의 메소드에서 멈추지 못하였던 행위들을 이 메소드 내에서 멈출 수 있습니다.
<br>
<br>
View Controller가 화면에서 사라지는 것이 메모리에서 해지된다는 것을 의미하지 않는다는 것을 명심해야한다. 즉 화면에서 사라진다고 메모리에서 해제되는 것은 아니다. 많은 Container View Controller들이 그들의 View Controller들을 메모리에서 유지하고 있기 때문이다.</p>
</details>
[Reference]

https://www.notion.so/467df350a438455785ccb86e6a551070






## App thinning에 대해서 설명하시오.

## 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?

## @Main에 대해서 설명하시오.

## 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?

## 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.

## 앱이 In-Active 상태가 되는 시나리오를 설명하시오.

## scene delegate에 대해 설명하시오.

## UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?

## App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.

## NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.

## GCD API 동작 방식과 필요성에 대해 설명하시오.

## Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.

## iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가?

## Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.

## Delegate란 무언인가 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.

## NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.

## UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?

## App Bundle의 구조와 역할에 대해 설명하시오.

## 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?

## 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.

## View 객체에 대해 설명하시오.

## UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.

## UIWindow 객체의 역할은 무엇인가?

## UINavigationController 의 역할이 무엇인지 설명하시오.

## TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.

## 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.

## setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.

## NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.

## URLSession에 대해서 설명하시오.

## repareForReuse에 대해서 설명하시오.

## 다크모드를 지원하는 방법에 대해 설명하시오.