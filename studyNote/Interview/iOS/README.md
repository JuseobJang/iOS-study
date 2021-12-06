# iOS Develop

## Interview List

- [Bounds 와 Frame 의 차이점을 설명하시오.](#bounds-와-frame-의-차이점을-설명하시오)
- [실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.](#실제-디바이스가-없을-경우-개발-환경에서-할-수-있는-것과-없는-것을-설명하시오)
- [앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?](#앱의-콘텐츠나-데이터-자체를-저장보관하는-특별한-객체를-무엇이라고-하는가)
- [앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?](#앱-화면의-콘텐츠를-표시하는-로직과-관리를-담당하는-객체를-무엇이라고-하는가)
- [App thinning에 대해서 설명하시오.](#app-thinning에-대해서-설명하시오)
- [@Main에 대해서 설명하시오.](main에-대해서-설명하시오)
- [앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?](#앱이-foreground에-있을-때와-background에-있을-때-어떤-제약사항이-있나요)
- [상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.](#상태-변화에-따라-다른-동작을-처리하기-위한-앱델리게이트-메서드들을-설명하시오)
- [앱이 In-Active 상태가 되는 시나리오를 설명하시오.](#앱이-in-active-상태가-되는-시나리오를-설명하시오)
- [scene delegate에 대해 설명하시오.](#scene-delegate에-대해-설명하시오)
- [App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.](#app의-not-running-inactive-active-background-suspended에-대해-설명하시오)
- [NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.](#nsoperationqueue-와-gcd-queue-의-차이점을-설명하시오)
- [GCD API 동작 방식과 필요성에 대해 설명하시오.](#gcd-api-동작-방식과-필요성에-대해-설명하시오)
- [Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.](#global-dispatchqueue-의-qos-에는-어떤-종류가-있는지-각각-어떤-의미인지-설명하시오)
- [iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가?](#ios-앱을-만들고-user-interface를-구성하는-데-필수적인-프레임워크-이름은-무엇인가)
- [Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.](#foundation-kit은-무엇이고-포함되어-있는-클래스들은-어떤-것이-있는지-설명하시오)
- [Delegate란 무언인가 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.](#delegate란-무언인가-설명하고-retain-되는지-안되는지-그-이유를-함께-설명하시오)
- [NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.](#notificationcenter-동작-방식과-활용-방안에-대해-설명하시오)
- [UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?](#uikit-클래스들을-다룰-때-꼭-처리해야하는-애플리케이션-쓰레드-이름은-무엇인가)
- [App Bundle의 구조와 역할에 대해 설명하시오.](#app-bundle의-구조와-역할에-대해-설명하시오)
- [모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?](#모든-view-controller-객체의-상위-클래스는-무엇이고-그-역할은-무엇인가)
- [자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.](#자신만의-custom-view를-만들려면-어떻게-해야하는지-설명하시오)
- [View 객체에 대해 설명하시오.](#view-객체에-대해-설명하시오)
- [UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.](#uiview-에서-layer-객체는-무엇이고-어떤-역할을-담당하는지-설명하시오)
- [UIWindow 객체의 역할은 무엇인가?](#uiwindow-객체의-역할은-무엇인가)
- [UINavigationController 의 역할이 무엇인지 설명하시오.](#uinavigationcontroller-의-역할이-무엇인지-설명하시오)
- [TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.](#tableview를-동작-방식과-화면에-cell을-출력하기-위해-최소한-구현해야-하는-datasource-메서드를-설명하시오)
- [하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.](#하나의-view-controller-코드에서-여러-tableview-controller-역할을-해야-할-경우-어떻게-구분해서-구현해야-하는지-설명하시오)
- [setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.](#setneedslayout와-setneedsdisplay의-차이에-대해-설명하시오)
- [NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.](#nscache와-딕셔너리로-캐시를-구성했을때의-차이를-설명하시오)
- [URLSession에 대해서 설명하시오.](#urlsession에-대해서-설명하시오)
- [prepareForReuse에 대해서 설명하시오.](#prepareforreuse에-대해서-설명하시오)
- [다크모드를 지원하는 방법에 대해 설명하시오.](#다크모드를-지원하는-방법에-대해-설명하시오)



## Interview Contents

### Bounds 와 Frame 의 차이점을 설명하시오.

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



### 실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.

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



### 앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?

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



### 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?

**VIewController** : 앱 구조의 뼈대, 모든 앱에 반드시 하나 이상의 view controller로 이루어져 있다.

#### Responsibility

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



#### Life Cycle

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





### App thinning에 대해서 설명하시오.

앱이 디바이스에 설치 될 때, 앱스토어와 운영체제가 디바이스의 특성에 맞게 설치되도록 하는 **설치 최적화 기술**을 의미한다. 

장점 : 최소한의 디스크 사용과 빠른 다운로드 제공

방식 : 슬라이싱, 비트코드, 주문형 리소스



**슬라이싱(slicing)**

앱이 지원하는 여러 디바이스에 대해 각각의 조각 어플리케이션 번들을 생성하고, 해당 디바이스에 가장 적합한 조각을 전달하는 기술 

아이폰 기종별 또는 아이패드와 같이 다른 기종에 대해서 가장 알맞는 조각(app variant)를 다운로드 하는 것이다.



**비트코드(bitcode)**

비트코드는 기계언어로 번역되기 이전 단계의 중간표현을 말한다. 현재 iOS에서는 기본 설정으로 되어있다. 

비트코드 사용하여 업로드 할 경우 : 애플이 앱을 재컴파일하여 앱바이너리를 생성하는데 이는 여러 디바이스 환경에 최적화가 가능 하다.

비트코드 사용하지 않고 업로드 하는 경우 : 모든 경우의 디바이스 환경을 고려한 팻 바이너리를 생성한다.



**주문형 리소스**

필요할 때 다운로드 받는 방식이다. 예를 들어 인앱 구매를 하면 해당 리소스를 다운 받을 수 있다.

[Reference]

https://ttuk-ttak.tistory.com/42



### @Main에 대해서 설명하시오.

xcode 이전버전의 `@UIAllicationMain` 과 같은 것으로, C언어 계열인 objective-c 에서도 main() 함수가 필요한데 해당 역할을 하여 앱의 진입점을 표시하고 커스터마이징 할 수 있다.

`UIApplaction` 객체의 인스턴스를 생성하고, 해당 객체의 앱으로서 기능하기 위한 기반을 마련하는데 이를 로딩 프로세스라고 한다.

[Reference]

https://jinshine.github.io/2018/05/28/iOS/%EC%95%B1%EC%9D%98%20%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0(App%20Life%20Cycle)%EC%99%80%20%EC%95%B1%EC%9D%98%20%EA%B5%AC%EC%A1%B0(App%20Structure)/



### 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?

**Foreground** : 메모리 및 기타 시스템 리소스에 높은 우선순위를 가지며 시스템은 이러한 리소스를 사용할 수 있도록 필요에 따라 background에 있는 앱을 종료 할 수 있다.

**Background** : 가능한 적은 메모리 공간을 사용해야한다. 시스템 메모리를 해제 하여야하고 사용자 이벤트를 받기 어렵다.



[Reference]

https://exception-log.tistory.com/184



### 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.

```swift
// 앱 실행 :
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool

// 앱 활성화 :
// 앱이 화면에 뜬 이후에 실행
// 백그라운드로 갔다가 다시 포어그라운드로 돌아와도 실행
func applicationDidBecomeActive(_ application: UIApplication) 

// 앱 비활성화 :
// 포어그라운드에서 백그라운드로 갈때 실행
// 공유 자원 해제 또는 유저 데이터 저장 등의 로직을 구현
func applicationDidEnterBackground(_ application: UIApplication) 

// 다시 앱 실행(메모리에 아직 남아 있는 경우)
// 앱의 상태 갱신 구현
func applicationWillEnterForeground(_ application: UIApplication)
```



[Reference]

http://monibu1548.github.io/2018/08/28/appdelegate/



### 앱이 In-Active 상태가 되는 시나리오를 설명하시오.

앱이 실행되는 경우, 포어그라운와 백그라운드사이를 왔다갔다 하는 경우 보톤 해당 Inactive 상태를 거침

Example

1. Not running - **Inactive** - Active
2. Active - **Inactive** - Background
3. Background - **Inactive** - Active



### scene delegate에 대해 설명하시오.

- iOS 13 이전에는 하나의 앱에 하나의 `window` 를 가졌지만, iOS 13부터는 window의 개념의 `scene` 으로 대체 되고 하나의 앱에서 여러개의 `scene` 화면을 가질 수 있다.

- 원래는 `AppDelegate` 에서 하는 UI의 상태를 알 수 있는 UILifeCycle에 대한 부분을 **SceneDeleage** 가 하게 되었다.

> Application: willEnterForegound -> Scene: willEnterForegound
>
> Application: didEnterBackground -> Scene: didEnterBackground
>
> Application: willResignActive -> Scene: wiiResignActive
>
> Application: didBecomeActive  -> Scene: didBecomeActive

- 대신 AppDelegate에서는 Scene Sesstion을 통해 Scene의 정보를 관리한다.

- **Scene** 과 **Scene Session**

  Scene : windows와 viewControllers를 가지고 있다. UIWindowSceneDelegate객체를 통해 UIKit과 앱간의 상호작용을 조정 하는데 사용한다.

  Scene Session : Scene의 고유 런타임 인스턴스를 관리한다.

- iOS 13 부터 AppDelegate 역할

  1. 앱의 가장 중요한 데이터 구조를 초기화
  2. 앱의 scene을 환경 설정 하는 것
  3. 앱 밖에서 발생한 알림에 대응하는 것
  4. 특정한 scene, view에 한정되지 않고 앱자체를 타겟하는 이벤트에 대응하는 것
  5. 애플 푸시 알림 서비스오 같이 실행시 요구되는 서비스를 등록하는 것

    

[Reference]

https://velog.io/@dev-lena/iOS-AppDelegate%EC%99%80-SceneDelegate



### App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.

- Not running : 앱이 실행중이지 않을 때
- Foreground : 앱이 실행중이고 사용자에게 보여지고 있는 상태
  - Inactive : 앱이 실행중이지만 아직 아무런 이벤트를 받지 않는 상태, 앱 사용중 전화가 오거나, 잠금화면 멀티태스킹 스크린 등에서 해당 상태를 가짐
  - Active : 앱이 실행중이고 현재 이벤트를 받고 있거나 발생한 상태
- Background : 앱이 백그라운드에 있지만 여전히 실행중인 코드가 있는 상태
- Suspend : 앱이 백그라운드에 있고 실행되는 코드가 없는 상태



### NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.

**NSOperationQueue** : 

- Operation Queue에 추가된 작업은 작업이 완료될때 까지 대기열에 남아있다. 작업이 한번 추가된 후에는 대기열에서 직접 제거 할 수 없다.

- 모든 작업이 끝나지 않은 상태에서 Operation Queue를 중지시키면 메모리 릭이 발생할 수 있다.

- GCD는 할 수 없는 기능들(재개, 취소, 중지) 등을 제공하지만 구현이 복잡하고 무겁다.

- 작업간의 의존성을 설정에서 작업의 계층을 만들 수 있다. ~~이거 쓸바에 RxSwift쓰는게 나을 듯~~



**GCD Queue** : 

- 동시성 모델을 매우 간단하게 사용 할 수 있다.

- 앱의 메인 스레드 또는 백드라운드 스레드에서 작업의 실행을 직렬 또는 병렬적으로 할지 관리하는 객체이다.

- 작업항목을 동기 또는 비동기적으로 예약한다.

- 메인 큐에서 작업항목을 동기적으로 실행하면 데드락에 걸릴 수 있다.

  main.sync의 경우 해당 작업이 끝날 때 까지 코드에 머물러 있는다. 즉 큐를 블락하고 큐에 넣은 작업이 완료 될때까지 기다리지만 이미 큐는 블락된 상태이기 때문에 작업은 실행조차 할 수 없게 된다.



[Reference]

https://thoonk.tistory.com/30



### GCD API 동작 방식과 필요성에 대해 설명하시오.

한 스레드(특히 main thread)에서 너무 많은 일을 시키면 태스크마다 텀이 길어지고, 앱에서 볼때는 화면이 멈춘듯한 느낌을 줄 수 있다. 따라서 네트워크 통신이나 이미지 처리 같은 시간이 오래 걸리는 작업에 대해서 서브 쓰레드에서 동작 시킬 수 있도록 작업을 분산시켜 준다. 

작업이 완료되어 해당 결과를 통해 UI를 업데이트 해야 한다면 메인 쓰레드 큐에 뷰 업데이트 작업을 넣어준다.



### Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.

1. `.userInteractive` 유저와 직접 인터랙션 : UI관련 (즉시)
2. `.useInitiated` 반드시 필요한 비동기 처리 : 앱 내에서 첨부파일 열기, 내부 데이터 베이스 조회 등
3. `.default` 일반적인 작업
4. `.utility` 길게 실행되는 작업 : 데이터 다운로드 
5. `.background` 유저가 직접적으로 인지하지 않는 시간이 중요하지 않은 작업



### iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가?

**UIKit** : 사용자 인터페이스(UI)를 구현하고 이벤트를 관리하는 프레임 워크이다.

UI : 뷰, 컨트롤러, 뷰컨트롤러, 애니메이션, 햅틱, window & scene

이벤트 : 터치, 프레스, 제스쳐, 드래그 앤 드롭 등등



### Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.

Foundation Kit이란 코코아 터치 프레임 워크에 포함된 프레임워크이다.

기본 : 

- 원시데이터 타입 : Data, String, Number 등 
- Collection Type : Array, Dictionary, Set 등
- Date & Time : 날짜와 시간을 계산하거나 비교하는 작업
- Unit & Measurment : 물리적 차원을 숫자로 표현 및 관련 단위간 변환 가능
- Data Formatting : 숫자, 날짜, 측정값 등을 문자열로 변환 또는 반대 작업
- Filter & Sorting : 컬렉션의 요소를 정렬 하거나 검사

어플리케이션 지원 : 

- Resource : 애플리케이션의 에셋과 번들 데이터 접근
- Notification : 정보를 퍼뜨리거나 받아들이는 작업
- App Extension : 확장 애플리케이션과의 상호작용 
- Error & Extension : API 상호작용 에서 발생하는 예외 처리

파일 및 데이터 관리

- File System : 파일 또는 폴더 생성, 읽기 쓰기
- Archive & Serialization : 프로퍼티, Json 바이너리 데이터를 디코딩, 인코딩
- iCloud : 사용자의 iCloud 계정을 이용해 데이터 관리



**\+ .swift 파일을 추가하면 자동으로 foundation은 import 됨** 



[Reference]

https://lazyowl.tistory.com/entry/Foundation-Kit%EC%9D%B4%EB%9E%80



### Delegate란 무언인가 설명하고, retain(cycle) 되는지 안되는지 그 이유를 함께 설명하시오.

**Delegate** 는 디자인 패턴으로 클래스나 구조체의 책임 중 일부를 다른 타입의 인스턴스에게 전달(위임)을 가능하게 해준다.

클래스에서 프로토콜을 채택하기 위해서는 **class-only-protocol** 클래스 전용 프로토콜을 사용해야한다. 

```swift
protocol someDelegate: class
```

이렇게 되면 프로토콜이 class type을 바뀌게 되기 때문에 Retail Cycle이 발생할 수 도 있다는 것이다.

그렇기 때문에 보통 `delegate` 를 변수화 해서 사용 할 때에는 `weak` 로 선언해서 retain cycle에 의한 메모리 누수를 막아야 한다. 

```swift
protocol someClass{
  weak var delegate: someDelegate?
}
```



[Reference]

https://fomaios.tistory.com/entry/iOS-%EB%A9%B4%EC%A0%91%EC%A7%88%EB%AC%B8-Delegate%EB%8A%94-retain%EC%9D%B4-%EB%90%A0%EA%B9%8C?category=890971



### NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.

**동작방식**

NotificationCenter는 등록된 모든 Observer들에게 브로드캐스팅하여 정보를 전달하는 방식이다.

```swift
// NotificationCenter에 해당하는 뷰컨트롤러(self)를 옵저버로 추가함
// name에 해당하는 노티피케이션이 왔을 때
// selecter의 함수를 실행한다.
NotificationCenter.default.addObserver(self, selector: #selector(notificationHandler(_:)), name: "notiName", object: nil)

// NotificationCenter에 post 하면
// NotificationCenter에서 등록된 옵저버들에게 notification을 보냄
NotificationCenter.default.post(name: "notiName", object: "전달할 값")
```

**활용방안**

뷰컨트롤러 간에 즉각적으로 업데이트 되어야할 정보가 있을 시 NotifiacationCenter를 사용하여 해당 정보를 전달함



### UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?

**Main Thread**

UIKit 클래스는 앱의 Main Thread에서만 사용해야한다. 

UIKit이 Thread Safe를 보장하기 위해서는 block 메커니즘이 필요한데 이는 거대한 UIKit프레임 워크에서 치명적인 성능 저하를 유발 하게되므로 현실적으로 불가능하다.

그렇게 때문에 작업들을 serial 하게 처리하는 Main Thread 에서 처리해주어야만 한다.



### App Bundle의 구조와 역할에 대해 설명하시오.

**Bundle** : 실행가능한 코드와 관련 리소스를 한 공간에 묶는 파일 시스템에 존재하는 디렉토리 모음이다.

**App Bundle** : 개발자들에 의해 생성되는 가장 흔한 번들로 앱을 성공적으로 실행시키기 위한 모든 것들을 저장한다. 

**번들에 존재하는 파일들** :

- Info.plist : 앱을 위한 configuration 정보를 담은 런타임 configuration 파일
- Excutable : 모든 앱은 반드시 실행 가능한 파일이 필요하다.
- Resource Files: Excutable file 밖에 있는 데이터들 보통 이미지, 아이콘, 사운드, nib파일, 문자열 파일, config 파일, 데이터 파일 등을 포함한다. 모든 리소스 파일은 localized & nonlocalized가 될 수 있으며 localized 파일 이라면 Resources 서브 디렉토리에 내에 대응하는 언어나 locale정보에 `lproj` 확장자를 가진 파일로 저장됨
- Other Support Files

>  앱 번들의 리소스는 대부분 옵셔널하지만 항상 그렇지 않은 경우도 있다.



[Reference]

https://sihyungyou.github.io/iOS-app-bundle/



### 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?

**UIResponder**

UIResponder의 인스턴스는 UIKit의 앱 이벤트 처리에 대한 백본(backbone)을 구성한다.

UIApplication,UIViewController ,UIView 객체도 Responder이다. 이벤트가 발생하면 UIKit은 이를 처리 할 수 있도록 앱의 리스폰더 객체에 전달한다. **즉, 이벤트 발생시 해당 객체들이 이벤트를 처리 할 수 있다는 것이다.** 

**이벤트 처리 외에도 리스폰더는 처리되지 않은 이벤트를 앱의 다른 부분으로 전달하는 작업을 한다.** 즉 주어진 리스폰더가 해당 이벤트를 처리하지 않으면 UIKit은 미리 정의된 규칙을 사용해 리스폰더 체인을 동적으로 관리하여 다른 리스폰더에서 처리 할 수 있게 해준다.

Example) view -> super view, rootview -> view controller



[Reference]

https://www.zehye.kr/ios/2021/08/17/iOS_uiresponder/



### 자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.

**xib 파일을 사용하는 방법**

1. CustomView.swift & CustomVIew.xib 생성 

2. CustomView.xib에 UI 커스텀 후 File's Owner의 class를 CustomView로 설정

3. CustomView.swift에 init 설정

   ```swift
   // 코드로 초기화 하는 경우 실행
   override init(frame: CGRect) {
     super.init(frame: frame)
     initView()
   }
   // 스토리보드로 초기화 하는 경우 실행
   required init?(coder: NSCoder) {
     super.init(coder: coder)
     initView()
   }
   // 빈 Custom View에 직접 만든 xib를 불러와서 쌓는 원리
   private func initView(){
     let view = Bundle.main.loadNibNamed("CustomView" , owner: self, options: nil)?.first as ! UIView
     view.frame = bounds
     addSubview(view)
   }
   ```



**xib 사용과 Only Code 인 경우 비교**

|      |                           Xib 사용                           |                          Only Code                           |
| :--: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 장점 | 눈으로 쉽게 보면서 레이아웃 작업 가능, 뷰 컨트롤러에 추가적인 코드 작업 필요 없음, 레아아웃 에러찾기 쉬움, 재사용성 증가 | 개발자 마음대로 제어가 가능(동적인 레이아웃 구성하기가 쉬움), 충동시 해결하기 쉬움, 재사용성 증가 |
| 단점 |  충돌시 골치 아픔, 코드로 작성한 UI에 비해서 오버헤드가 큼   | 개발 기간이 Xib에 비해서 오래 걸림, 레이아웃 에러 찾기가 힘듬, 오래된 코드의 경우 리팩토링이 힘듬 |



[Reference]

https://nsios.tistory.com/83



### View 객체에 대해 설명하시오.

`UIView` 클래스의 인스턴스로, 윈도우(~~iOS13 이후엔 Scene아닐까?~~) 위에서 컨텐츠를 보여준다. 즉 화면에 나타나는 거의 모든 요소를 뷰라고 봐도 된다. 뷰는 컨텐츠를 나타내고 하위 뷰를 계층적으로도 담을 수 있다.

`View Controller` 의 경우 이러한 뷰를 컨트롤하고 정보를 주고 받고 뷰를 관리하는 역할을 수행한다.



[Reference]

https://etst.tistory.com/79



### UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.

모든 UIView 에는 렌더링, 레이아웃, 애니메이션 등을 관리하는 클래스인 **CALayer** 가 존재한다.

UIView는 실제로 다양한 이벤트 처리해야 하기 때문에 실제로 뷰위에 컨텐츠나 애니메이션을 그리는 행위는 직접 다루지 않고 해당 CALayer를 통해서 다른 작업하게 한다.

UIView가 바쁘기 때문에 대신 해주는 느낌, 실제로 아래 동작은 결과적으론 같다.

```swift
uiView.backgroundColor = .blue
uiView.layer.backgroundColor = .blue
```



[Reference]

https://gwangyonglee.tistory.com/54



### UIWindow 객체의 역할은 무엇인가?

보여지는 앱의 시각적 컨텐츠들을 담고 뷰들과 다른 객체들에게 터치 이벤트 같은 이벤트를 전달하는 역할 이었으나, iOS 13 버전 부터는 SceneDelegate가 나오면서 Scene으로 대체 되었지만 SceneDelegate 에서 UIWindow를 선언하여 사용은 가능하다.



### UINavigationController 의 역할이 무엇인지 설명하시오.

`UINavigationController`의 주요 역할은 컨텐츠인 뷰컨트롤러와 네비게션바(또는 툴바) 두가지를 보여주는 것이다. 네비게이션 바에서는 뒤로가기 버튼 또는 커스터마이징한 버튼을 추가할 수 있다.

`UINavigationController`의 네비게이션 스택은 Last-In First-Out 방식이며 처음 들어간 `RootViewController`의 경우 절대 제거되지 않는다. 

즉, `UINavigationController` 사용자의 액션에 응답하여, 새 컨텐츠 뷰 컨트롤러를 스택에 쌓고 뷰컨트롤러를 제거하는 역할을 한다.



### TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.

```swift
// 테이블 뷰의 섹션별로 아이템 개수
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int

// 특정위치(indexPath) 에 표시할 셀을 반환하는 메서드
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
```



### 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.

`extension` 을 사용하여 명시적으로 ViewController의 역할을 구분 한다.



### setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.

**Main Run Loop**

메인 런 루프는 터치이벤트, 위치의 변화, 디바이스 회전등 다양한 이벤츠를 처리하게 되고 이러한 처리과정은 각 이벤트들에 대해 적합한 핸들러를 찾아 그들에게 처리 권한을 위임하며 진행된다. 발생한 이벤트들을 모두 처리하고 다시 권한이 메인 런 루프로 돌아오는 시점을 **update cycle** 이라고 한다.

**setNeedsLayout() & setNeedsDisplay()**

뷰의 하위뷰를 조정하고 싶을 때 사용된다. 전자는 `layoutSubViews()` 를 후자는 `draw()` 를 실행하여 하위뷰를 조정한다.

하지만 `layoutSubViews()` & `draw()` 둘다 바로 실행되는 것이 아닌 어떤 뷰가 변경 되어야 하는지를 체크한 후 update cycle에서 해당 뷰들을 한번에 업데이트 해준다.



[Reference]

https://velog.io/@zeke/difference-between-setNeedsLayoutsetNeedsDisplay



### NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.

1. **NSCache**는 메모리 관리가 유용하다

   다른 앱에서 메모리를 더 사용하려고 하면 캐시되어 있던 데이터를 지우고 메모리를 해제 한다.

2. **NSCache** 는 Thread-Safe하다

   캐시 데이터를 읽고 쓰고 지울때마나다 따로 lock을 해줄 필요가 없다 

   반면에 딕셔너리로 해주었을 경우 Thead-safe하지 않기 때문에 따로 처리를 해주어야 한다.

3. **NSCache** 는 retain 카운트를 증가시키는 방식이다.

   복사를 지원하지 않는 객체까지 포용한다.

   반면에 딕셔너리는 key값을 카피만 가능하다. 



[Reference]

https://firekokoma.tistory.com/344



### URLSession에 대해서 설명하시오.

URLSession이란 iOS에서 제공하는 HTTP 를 이요한 네트워킹을 통해 데이터를 주고받을 수 있게 도와주는 API를 제공해주는 클래스이다. URLSession은 Thread-Safe하기 때문에 어떤 쓰레드에서든 자유롭게 세션과 테스크를 생성할 수 있다.



[Reference]

https://velog.io/@folw159/iOS-URLSession



### prepareForReuse에 대해서 설명하시오.

컬렉션 뷰나 테이블뷰의 경우 Cell을 `dequeReusableCell()` 을 사용하여 재사용한다. 이때 이전에 설정한 값 등 필요없는 값들을 갖게 되는데 이러한 문제를 해결하기 위해서 `prepareForReuse()` 메서드를 사용해서 재사용되기 전 해당 Cell을 초기화 해주는 것이다.



### 다크모드를 지원하는 방법에 대해 설명하시오.

**Code를 사용한 다크모드 지원**

`UIColor` 설정시 `traitCollection.userInterfaceStyle` 이 라이트 모드(.light) 인지 다크 모드인지 (.dark) 체크하여 원하는 UIColor를 적용한다.



**Assets을 사용한 다크모드 지원**

Color Set의 Appearance 값을 Any, Dark 로 설정 후 원하는 색 설정 