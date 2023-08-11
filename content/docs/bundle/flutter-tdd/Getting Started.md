---
title: Getting Started
showToc: true
---

앞선 [[flutter-tdd|Flutter TDD Chap01 ~ 02]] 를 통해 Flutter의 Test code 작성법에 대해 알아보았습니다.

이번 챕터에서는 TDD를 통한 Google map을 구현해봄으로써 Flutter Test code를 실습해봅니다.

----

## Package setup

Google_maps_flutter 패키지를 활용하여 Google Map을 구현합니다.

### 01. Create Flutter project
먼저 아래의 명령어를 통해 새로운 Flutter 프로젝트를 생성합니다.

```cli
flutter create --org <id> <project_name>
```

### 02. Package 추가하기
생성된 프로젝트에 [google_maps_flutter](https://pub.dev/packages/google_maps_flutter) 패키지를 추가합니다.

아래의 커맨드를 통해 `pubspec.yaml` 파일에 종속성을 추가합니다.

```
flutter pub add google_maps_flutter
```

추가된 dependency는 아래와 같습니다.

```yaml
dependencies:
	google_maps_flutter: <version>
```

### API 키 생성
Google Map을 사용하기 위해서는 API Key가 등록되어 있어야 합니다.
이를 위해 [Google Cloud Console](https://mapsplatform.google.com/)에서 API Key를 발급받습니다.

GCP에서 새로운 프로젝트를 생성하고 API 라이브러리에서 `Maps SDK for Android` 와 `Maps SDK for iOS` 를 추가합니다.

![[스크린샷 2023-07-17 오후 3.05.42.png]]

## iOS & Android Setup

### iOS
API 키 생성 이후 Runner/AppDelegate를 아래와 같이 수정합니다.

```swift
import UIKit
import Flutter
import GoogleMaps

@UIApplicationMain

@objc class AppDelegate: FlutterAppDelegate {

  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions:[UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    GMSServices.provideAPIKey("API KEY")
    GeneratedPluginRegistrant.register(with: self)
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
}
```

이후, 타겟 iOS 버전을 google_maps_flutter가 호환되는 11+ 로 변경합니다. 타겟 변경은 podfile에서 아래와 같이 작성합니다.

```
platform :ios, '11.0'
```

> [!More] 
> 타겟 설정 이후 `flutter clean` 명령어를 이용하여 pod 내용을 업데이트해줍니다.
