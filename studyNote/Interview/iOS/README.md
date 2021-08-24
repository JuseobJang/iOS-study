# iOS Develop

## Interview List

- [Bounds 와 Frame 의 차이점을 설명하시오.](#bounds-와-frame-의-차이점을-설명하시오)

- [실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오.](#실제-디바이스가-없을-경우-개발-환경에서-할-수-있는-것과-없는-것을-설명하시오)
- 앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?
- 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?
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

- Frame : superview의 좌표계를 기준으로 해당 view가 위치하는 location 과 size를 나타내는 속성이다.(superview는 **한 단계** 상위뷰를 의미)
- Bounds : 자기 자신의 좌표계를 기준으로 location 과 size를 나타내는 속성이다.

**Location** :

Frame 의 경우 superview의 왼쪽 상단을 기준으로 해당 view의 왼쪽 상단과 x축, y축 으로 만큰 떨어진 값으로 계산된다.

Bounds의 경우에는 superview 상관없이 자기 자신만의 좌표계를 갖기 때문에 origin 은 항상 (0, 0) 이다.

**Size** :

사이즈의 두 속성 모두 동일하다고 생각할 수 있고 일반적으로는 그러하다.

하지만 만약 뷰가 회전된 상태라고 한다면, 

Frame은 상위 뷰와 x축, y축으로 평행하게 해당 뷰를 감쌀 수 있는 틀의 사이즈를 나타내고 Bounds의 경우에는 회전 되기 전의 자체 뷰 사이즈를 갖는다.

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

## 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?

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