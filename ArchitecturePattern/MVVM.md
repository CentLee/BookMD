# MVVM 

* Model View ViewModel 로 구성되어 있다.
* POP를 기반으로 관심사 분리를 통해 Input Output를 구분하여 사용하는 것이 효과적이다.


# MVVM + Clean Architecture
![circle](https://user-images.githubusercontent.com/35019052/170171918-c3a7eb29-e4e8-4201-8d1a-cf6dad2c0b40.png)


- 바깥쪽 원의 어떠한 것도 안쪽의 원에 영향을 줘선 안된다.

## Application Layer 
- 이 계층은 앱 전체의 entry-Level이며, global Layer ( etc... DI components, Constants, AppDelegaet ) 이다.

## Domain Layer
  - 가장 내부에 위치한 계층으로서 Entity와 UseCase 그리고 RepositoryInterface가 있습니다.
  - 이 레이어는 다른 레이어들에게 어떠한 영향도 받지 않습니다.
  - 다른 프로젝트에 의하여서 재사용 될 수 있습니다. 
  - Entity: 불변하는 구조를 가지며, 비즈니스 모델을 뜻한다.
  - UseCase: 고유 비즈니스 규칙을 포함하며 시스템의 모든 유스케이스를 캡슐화하고 구현한다. 

## Presentation Layer
  - 그 다음 계층으로서 UI와 ViewModel등을 포함합니다.
  - 뷰모델은 하나이상의 Use cases를 execute하기때문에 Presentation Layer는 Domain Layer를 의존합니다. 


## Data Layer
  - Repository와 Local DB, restAPI 등을 포함합니다.
  - 명시된 경로를 통해서 데이터를 반환해서 DTO를 통해 Domain Layer의 Entity로 데이터를 반환하는 구조를 가집니다. 
  - 따라서, 데이터 계층 또한 Domain Layer를 의존합니다.
