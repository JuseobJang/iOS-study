# VIPER Pattern

![img](https://miro.medium.com/max/1400/1*0pN3BNTXfwKbf08lhwutag.png)

View - Interactor - Presenter - Entity - Router 의 구성을 가지는 디자인 패턴, 줄여서 VIPER 패턴이라고 한다.

View : Presenter가 전달한 정보를 표시하고 사용자 입력을 받아 Presenter에게 전달한다.

Interactor : Use case에 따라 Entity 모델 Object를 조작한다. (Entity의 새로운 instance 생성 혹은 networking 관련 Logic)

Presenter : Interactor에게서 데이터를 가져와 View에 띄울 정보를 준비한다. 그리고 사용자 입력에 반응하기 위한 View 로직을 포함하고 있다.

Entity : 기본 모델 Object (일반 데이터 객체들을 말함)

Router : 어떤 화면이 어떤 순서로 표시되는지 설명하기 위한 로직을 포함한다. Navigation 혹은 segue (화면 전환) 를 담당한다.

## 특징 및 장단점

- VIPER는 기본적으로 [단일 책임 원칙(Single Responsibility Principle, SRP)](https://ko.wikipedia.org/wiki/%EB%8B%A8%EC%9D%BC_%EC%B1%85%EC%9E%84_%EC%9B%90%EC%B9%99) 기반이다.

- 따라서 각 도메인의 역할이 명확하게 구분되고 재사용성(Reusability)과 테스트용이함(Testability)을 위해 코드를 분리한다.

- 새로운 기능을 추가하기 쉽다.

- 모듈을 작게 만들고 역할을 명확하게 하기 때문에 생성되는 파일의 수가 많고, 이는 대규모의 프로젝트에 유리하다.

### Reference

- [Architecting iOS Apps with VIPER](https://www.objc.io/issues/13-architecture/viper/)

- [iOS 아키텍처 패턴(MVC, MVVM, VIPER)](https://www.theteams.kr/teams/1092/post/67632)

- [iOS Architecture Patterns](https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52)

- [Building iOS App With VIPER Architecture](https://afteracademy.com/blog/building-ios-app-with-viper-architecture-8109acc72227)
