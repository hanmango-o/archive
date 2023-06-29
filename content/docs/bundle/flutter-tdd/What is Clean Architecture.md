---
title: What is Clean Architecture? 클린 아키텍처의 개념 및 정의
description: Learn about Robert C. Martin's clean architecture and explore concepts and definitions. | Robert C. Martin의 클린 아키텍처에 대해 알아보고 개념과 정의 살펴봅니다.
image: ../../../assets/docs_flutter_tdd_intro.png
showToc: true
---

# What is Clean Architecture?

좋은 아키텍쳐를 적용한 코드는 가독성을 높이고 코드의 재사용성을 높이는 등 프로젝트에 긍정적인 영향을 줍니다.

이번 챕터에서는 Robert C. Martin이 [Clean Code](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)에서 제시한 Clean Architecture에 대해 알아봅니다.

----

## Separation of concerns : 관심의 분리

시스템의 목표와 요구사항을 더 잘 이해하고, 이를 충족하는 솔루션을 더 효과적으로 개발하기 위해 많은 System Architecture가 제시되어왔습니다.

> [!Hint] System Architecture 란?
>  _A system architecture is the conceptual model that defines the structure , behavior , and more views of a system._
>  
> System Architecture는 시스템의 구조(Structure), 행동(Behavior), 뷰(Views) 등을 정의하는 개념적 모델입니다.
> 
> (출처 : [Wikipedia, Systems architecture](https://en.wikipedia.org/wiki/Systems_architecture))


이러한 System Architecture들은 세부사항은 다르지만 공통된 목적을 가집니다.

Robert C. Martin은 이러한 목적을 Separation of concerns, **관심의 분리**라고 말합니다.

> They all have the same objective, which is the __separation of concerns__.


### 계층 구조와 특징

관심의 분리라는 목표를 위해 Architecture는 소프트웨어를 각 목적에 맞게 계층으로 나누어 관리합니다.

계층 구조의 소프트웨어를 통해 각 계층별 관심사를 분리할 수 있고, 이러한 구조의 시스템은 아래의 특징을 가지게 됩니다.

- **Independent of Frameworks : 프레임워크 독립성**  
  프레임워크(라이브러리)에 의존하지 않고 독립적인 성질을 가집니다.

- **Testable : 테스트 용이성**  
  계층별 의존성이 낮기 때문에 외부 요소 없이 테스트할 수 있어 테스트에 용이합니다.

- **Independent of UI : UI 독립성**  
  시스템의 Business rules과 같은 로직을 변경하지 않고 UI를 쉽게 변경할 수 있습니다.

- **Independent of Database : DB 독립성**  
  특정 DB에 의존적으로 코드가 작성되지 않으므로, DB에 독립적입니다.

- **Independent of any external agency : 외부 기능 독립성**    
  Business rules은 시스템의 Business rules에만 집중하며, 외부 요소(UI, DB, Server 등)를 알지 못하므로 외부 기능에 독립적입니다.

-----

## Clean Architecture

관심을 분리하는 공통된 목적을 가지는 System Architecture들을 하나의 단일 아이디어로 통합한 것이 Clean Architecture입니다.

이를 다이어그램으로 표현하면 아래와 같습니다.

![[docs_flutter-tdd_clean-architecture_layer.jpeg]]

단, Clean Architecture는 어디까지나 컨셉일 뿐 정답이 아닙니다. **"관심의 분리라는 목적을 달성하기 위해 계층 구조로 시스템을 구성한다"** 라는 컨셉만 지킨다면 계층의 개수나, 분리 수준은 크게 상관하지 않습니다.

> [!Tip]
>  가장 좋은 Architecture는 각 시스템의 요구사항에 맞는 Architecture입니다.


### The Dependency Rule : 종속성 규칙
위 다이어그램에서 각 원은 소프트웨어의 영역(Layer)을 의미합니다. 일반적으로 원의 중심으로 갈 수록 소프트웨어의 수준이 높아집니다.

여기서 수준이 높다라는 것은 변경되기 어렵다는 것이고, 수준이 낮다라는 것은 변경되기 쉽다라는 의미입니다.

예를 들어 시스템의 핵심 비즈니스 모델과 같은 것은 수준이 높다라고 할 수 있습니다. 반대로 프레임워크와 같이 변경되기 쉬운 모듈의 경우 수준이 낮다라고 할 수 있습니다.

Robert C. Martin은 외부 원은 메커니즘, 내부 원은 정책이라고 표현합니다. 이러한 계층 구조가 동작하도록 만드는 규칙이 바로 **The Dependency Rule : 종속성 규칙**입니다.

해당 규칙은 **"소스 코드의 종속성은 안쪽 원을 가르키는 모양이여야 한다."** 라는 의미입니다.

이러한 규칙은 아래의 특징을 가집니다.

- 내부 계층은 자신보다 외부 계층의 어떤 것도 알 수 없다.
- 외부 계층에서 선언된 이름(변수, 함수, 클래스 등)은 내부 계층의 코드에서 언급되면 안된다.
- 외부 계층에서 사용하는 데이터 타입을 내부 계층에서 사용하면 안된다.(특히 프레임워크 사용에 주의해야 한다.)

위 특징을 요약하면 "외부 계층의 어떤 것도 내부 계층에 영향을 주면 안된다." 입니다.

> [!Tip]
> 추상 클래스나 인터페이스를 이용한 캡슐화를 통해 종속성 규칙을 지킬 수 있습니다.

이렇듯 계층 간의 분리, 더 나아가 계층의 각 관심사에 따른 행동이 다른 계층에 영향을 주면 안된다는 것이 Clean Architecture로 구성된 소프트웨어가 지켜야하는 규칙입니다.


### Entity
가장 내부 계층으로 소프트웨어에서 전사적 비즈니스 규칙(Business rules)이 포함되어 있는 영역입니다.

해당 영역에서는 애플리케이션에 적용되며, 외부 계층에 영향을 받지 않는 비즈니스 규칙이 정의됩니다.

Entity는 메서드가 있는 객체이거나 데이터 구조 및 함수 집합일 수 있습니다. 중요한 건 애플리케이션 전체에 적용되는 규칙이여야 하며, 외부 계층에 영향을 받지 않아야 한다는 것입니다.


### Usecase
해당 계층은 특정 애플리케이션의 비즈니스 규칙이 포함되어 있는 영역입니다.

Entity 간 데이터 흐름을 제어하고 해당 Entity가 보유하고 있는 비즈니스 규칙을 이용하여 원하는 목표를 달성할 수 있도록 지시하는 역할을 수행합니다.

쉽게 말해 Entity의 비즈니스 규칙 호출의 트리거 역할을 수행한다고 할 수 있습니다.

이러한 Usecase 계층은 캡슐화를 통해 구현되어 외부 계층에서 해당 계층을 호출할 수 있도록 하여야 합니다.

또한, Usecase 계층의 변경 사항이 발생하더라도 Entity 계층에서 정의한 비즈니스 규칙에 영향을 주면 안됩니다. 이는 외부 계층도 마찬가지로 DB, UI, 프레임 워크 등에 대한 영향을 주거나 받으면 안됩니다.


### Interface Adapters
인터페이스 어댑터는 앞서 살펴본 Entity와 Usecase 계층에서 사용한 데이터 형식에서 외부 계층(DB, 프레임 워크 등)이 사용하기 편리한 형식으로 변경하는 역할을 수행합니다.

즉, (Entity, Usecase 계층)과 그 외부 계층을 이어주는 역할을 수행합니다.


### Frameworks and Drivers
가장 바깥쪽 계층으로 DB, 프레임 워크 등 외부 요소와의 통신이 해당 영역에서 이루어집니다.

해당 영역은 프레임 워크, DB 등을 호출하여 통신하는 코드가 주를 이루게 되므로 이러한 외부 요소들에 의해 변화될 가능성이 높습니다.

따라서, 내부 계층과의 확실한 분리가 필요하며, 쉽게 변화되고 쉽게 교체될 수 있도록 작성되어야 합니다.


### 계층 간 경계에서 흐름 제어
앞서 살펴본 바에 의하면 Clean Architecture의 흐름은 외부 계층에서 내부 계층으로 이어집니다.

하지만 이러한 규칙은 계층의 경계로 갈 수록 지키기 어려워집니다.

예를들어 다이어그램에서 나타낸 것과 같이 Controller > Usecase > Presenter로 이어지는 흐름은 Adaptor와 Usecase의 흐름을 보여줍니다. Usecase에 의해 Adaptor가 호출되어 소통할 수 있지만 이런 경우 규칙에 위배되게 됩니다.

이러한 문제점은 DIP를 통해 해결할 수 있습니다.

내부 계층에서 외부 계층을 참조할 경우 직접 참조하는 것이 아닌 인터페이스나 추상 클래스를 통해 캡슐화된 값을 참조하게 하여 외부 계층의 변동 사항에 영향을 받지 않도록 합니다.

-----

**Summary :**
- Clean Architecture는 관심사에 따른 계층 구조로 구성된 소프트웨어 아키텍처이다.
- 각 계층은 고유의 역할과 관심사가 있으며, 타 계층의 영향을 받지 않아야 한다.
- 계층간의 소통 흐음은 내부 계층에서 외부 계층으로 이어져야 하며, 내부 계층에서 외부 계층을 참조할 경우 DIP를 통해 해결한다.

**Links :**
- https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
- https://en.wikipedia.org/wiki/Systems_architecture