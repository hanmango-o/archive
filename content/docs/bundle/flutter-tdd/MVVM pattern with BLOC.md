---
title: MVVM pattern with BLOC
showToc: true
---

관심사의 분리라는 목표를 위해 여러 디자인 패턴(Model-View-Whatever)이 존재합니다.

이번 챕터에서는 MVVM 패턴에 대해 알아보고 이를 BLOC 라이브러리를 활용하여 Flutter에서 구현하는 방법에 대해 알아봅니다.

----

## MVVM 패턴이란?

MVVM 패턴은 사용자 인터페이스의 개발을 비즈니스 로직으로 부터 분리하여 View가 종속되지 않게 하는 소프트웨어 아키텍쳐 패턴입니다.

[Microsoft](https://learn.microsoft.com/ko-kr/xamarin/xamarin-forms/enterprise-application-patterns/mvvm#the-mvvm-pattern)에서는 MVVM 패턴을 사용하였을 때 아래의 이점이 있다고 설명합니다.

> [!Hint] MVVM Pattern
>  _The Model-View-ViewModel (MVVM) pattern helps to cleanly separate the business and presentation logic of an application from its user interface (UI). Maintaining a clean separation between application logic and the UI helps to address numerous development issues and can make an application easier to test, maintain, and evolve. It can also greatly improve code re-use opportunities and allows developers and UI designers to more easily collaborate when developing their respective parts of an app._
>  
> - 애플리케이션의 비즈니스 및 프레젠테이션 로직을 UI(사용자 인터페이스)와 깔끔한 분리가능
> - 분리를 통해 쉬운 테스트, 유지 관리 및 기능 개발 가능
> - 코드 재사용성 향상 및 협업 편의성 증대
> 
> (출처 : [Microsoft, MVVM Pattern](https://learn.microsoft.com/ko-kr/xamarin/xamarin-forms/enterprise-application-patterns/mvvm#the-mvvm-pattern))


