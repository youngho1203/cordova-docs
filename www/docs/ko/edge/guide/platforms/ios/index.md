---
license: >
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
---

# iOS 플랫폼 가이드

이 가이드는 앱 아이폰과 iPad와 같은 iOS 장치에서 코르도바 앱들을 배포하기 위하여 어떻게 SDK 개발 환경을 설정하는지 방법을 보여줍니다. 자세한 플랫폼 관련 내용은 다음을 참조하십시오.

*   iOS 구성
*   iOS 업그레이드
*   iOS WebViews
*   iOS 플러그인
*   iOS 셸 도구 가이드

위의 명령줄 도구는 코르도바 3.0 이전 버전을 참조하십시오. 현재 인터페이스에 대한 내용은 명령줄 인터페이스를 참조하십시오.

## 필요 사항 및 지원

iOS 응용 프로그램을 빌드하는데 필요한 Apple® 도구는 인텔 기반 맥에 OS X 운영 체제에서만 동작합니다. Xcode® 6.0 (최소 필수 버전)은 OS X 버전 10.9 (댈러스 매버릭스) 또는 그 이상에서만 동작하고, iOS 8 SDK (소프트웨어 개발 키트)가 설치되어 있어야 합니다. 애플 앱 Store℠ 에 앱을 제출시에는 가장 최신 버전의 Apple 도구들을 필요로 합니다.

당신은 코르도바 기능의 대부분을 설치된 SDK와 Xcode의 iOS 에뮬레이터를 사용하여 테스트할 수 있습니다. 하지만 App 스토어에 제출하기 전에 응용 프로그램의 모든 기능을 실제 장치에서 테스트해야 합니다. 기기는 최소한 코르도바 3.0 이 지원하는 최소 버전인 iOS 6.x 가 설치되어 있어야 합니다. 기기는 모든 iPad ® 모델, 아이폰 ® 3GS 이상, 아이팟 ® 터치 3 세대 이상을 지원합니다. 장치에 앱을 설치하려면 애플의 [iOS 개발자 프로그램][1],연간 회비 $99, 회원이어야 합니다. 이 가이드는 당신이 개발자 프로그램에 등록하지 않아도 iOS 에뮬레이터에 앱을 배포하는 방법을 보여줍니다.

 [1]: https://developer.apple.com/programs/ios/

[ios-sim][2] 과 [ios-deploy][3] 도구 - 명령줄에서 iOS 시뮬레이터와 iOS 기기로 iOS 앱을 기동시킬 수 있도록 합니다.

 [2]: https://www.npmjs.org/package/ios-sim
 [3]: https://www.npmjs.org/package/ios-deploy

## SDK를 설치하기

Xcode를 다운로드하는 방법은 두 가지가 있습니다.:

*   [App 스토어][4]에서 **App 스토어** 응용 프로그램에서 "Xcode"를 검색하여 사용할 수 있습니다.

*   [애플 개발자 다운로드][5]에서 내려받을 수 있지만, 애플 개발자 등록을 해야합니다.

 [4]: https://itunes.apple.com/us/app/xcode/id497799835?mt=12
 [5]: https://developer.apple.com/downloads/index.action

일단 Xcode가 설치되면 코르도바를 동작시키기 위하여 여러 명령줄 도구가 동작할 수 있도록 설정해야 합니다. **Xcode** 메뉴에서 **Preferences**를 선택하고, **Downloads** 탭을 선택합니다. **Components** 패널에서 **Command Line Tools** 목록 옆에 있는 **Install** 단추를 누릅니다.

## 배포 도구를 설치하기

Command 라인 터미널에서 다음을 실행합니다.:

        $ npm install -g ios-sim
        $ npm install -g ios-deploy
    

## 새 프로젝트 만들기

코르도바 명령줄 인터페이스를 설명한 바와 같이 새로운 프로젝트 설정하기 위하여 `cordova` 유틸리티를 사용하십시요. 예를 들어 소스 코드 디렉터리에서:

        $ cordova create hello com.example.hello "HelloWorld"
        $ cd hello
        $ cordova platform add ios
        $ cordova prepare              # or "cordova build"
    

## 앱을 배포하기

연결되어 있는 iOS 디바이스에 응용 프로그램을 배포하려면:

        $ cordova run ios --device
    

기본 iOS 에뮬레이터에 응용 프로그램을 배포하려면:

        $ cordova emulate ios
    

**cordova run ios --list** 을 사용하면 모든 사용 가능한 대상을 확인할 수 있고, **cordova run ios --target=target_name** 실행하면 특정 장치 또는 에뮬레이터에서 응용 프로그램을 실행할 수 있습니다(예를 들어 `cordova run ios --target="iPhone-6"`).

또한 **cordova run --help** 사용하여 추가 빌드 및 실행 옵션들에 대한 도움말을 확인할 수 있습니다.

## SDK에서 프로젝트를 열기

일단 ios 플랫폼 프로젝트에 당신의 프로젝트가 추가되면, Xcode 에서 그것을 열 수 있습니다. `hello/platforms/ios/hello.xcodeproj` 파일을 두 번 클릭 합니다. 스크린은 다음과 같습니다.:

![][6]

 [6]: img/guide/platforms/ios/helloworld_project.png

## 에뮬레이터로 배포하기

iOS 에뮬레이터에서 앱을 미리 보기 위하여:

1.  왼쪽 패널에서 *.xcodeproj* 파일이 선택되어 있는지 확인합니다.

2.  바로 오른쪽 패널에서 **hello** 앱을 선택합니다.

3.  툴바의 **Scheme** 메뉴에서 여기에 아이폰 6.0 시뮬레이터처럼 강조되어 있는 원하는 장치를 선택합니다.:
    
    ![][7]

4.  **Scheme**의 왼쪽에 동일한 도구 모음에 있는 **Run** 단추를 누릅니다. 이제 빌드, 배포하고, 에뮬레이터에서 응용 프로그램을 실행합니다. 별도의 에뮬레이터 응용 프로그램이 이 앱을 표시하기 위하여 열립니다.
    
    ![][8]
    
    하나의 에뮬레이터에 한 번에 하나씩 실행 될 수 있습니다. 따라서 다른 에뮬레이터에서 앱을 테스트하려면 에뮬레이터 응용 프로그램을 종료하고 Xcode 내에서 다른 대상을 실행해야 합니다.

 [7]: img/guide/platforms/ios/select_xcode_scheme.png
 [8]: img/guide/platforms/ios/HelloWorldStandard.png

Xcode는 아이폰과 iPad의 가장 최신 버전에 대한 에뮬레이터를 번들로 제공합니다. 이전 버전에서 사용할 수 있는 것은 **Xcode → Preferences → Downloads → Components** 패널에서 가능합니다.

## 기기로 배포하기

기기에 배포하기 위하여 여러가지 필요 사항에 대한 자세한 내용은 애플의 [응용 프로그램 배포 작업][9] 문서의 *Launch Your App On Devices* 단원을 참조하십시오. 간단하게 설명하면, 배포하기 전에 다음을 수행해야 합니다.

 [9]: https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html

1.  애플 iOS 개발자 프로그램에 가입하세요.

2.  [iOS Provisioning Profile][10]에서 *Provisioning Profile* 을 생성합니다. 당신은 Xcode 에서 인증을 하고, 프로필을 생성하고, 설치하기 위하여 *Development Provisioning Assistant* 을 사용할 수 있습니다.

3.  프로젝트 설정에서 *Code Signing* 단원의 *Code Signing Identity* 값이 당신의 프로비저닝 프로파일 이름으로 설정되어 있는지 확인합니다.

 [10]: https://developer.apple.com/ios/manage/overview/index.action

기기에 배포하기:

1.  USB 케이블을 사용하여 mac에 장치를 연결합니다.

2.  Xcode 창의 **Scheme** 드롭다운 목록에서 프로젝트의 이름을 선택합니다.

3.  **Device** 목록에서 장치를 선택합니다. USB를 통해 연결되어 있지만 여전히 표시되지 않습니다, 모든 오류를 해결하려면 **Organizer** 단추를 누릅니다.

4.  빌드하고, 배포한 다음 당신의 기기에서 응용 프로그램을 실행하려면 **Run** 단추를 누릅니다.

## 일반적인 문제

**사용 중단 경고**: 응용 프로그램 프로그래밍 인터페이스 (API)가 변경되었거나 다른 API로 대체 되었을 때, 그것들은 *deprecated* 로 표시됩니다. 이런 deprecated API는 일정기간 동작을 하지만 궁극적으로 제거됩니다. 이러한 사용되지 않는 인터페이스의 일부가 아파치 코르도바에 반영되어 있기 때문에 Xcode 에서 빌드하고 응용 프로그램을 배포하는 경우 그것들에 대한 경고가 나타날 수 있습니다.

`invokeString` 방법에 대한 Xcode의 경고는 사용자 지정 URL에서부터 앱이 기동되는 기능에 대한 우려를 보이는 것입니다. 사용자 지정 URL에서 로드하는 메커니즘은 변경이 되었지만 이 코드는 코르도바의 이전 버전을 사용하여 만든 앱에 대한 기능을 제공하기 위하여 여전히 존재합니다. 다음 샘플 앱은 이 기능을 사용하지 않으므로 이러한 경고를 무시할 수 있습니다. 이러한 경고가 나타나지 않도록 하기 위해 사용되지 않는 invokeString API를 참조하는 코드를 제거합니다.

*   *Classes/MainViewController.m* 파일을 수정하십시요, /*` 및 `*/` 코멘트를 둘러싸고 있는 코드 불록에 아래와 같이 입력합니다. **Command-s** 로 파일을 저장합니다.:
    
        (void) webViewDidFinishLoad:(UIWebView*) theWebView {
        // ___PROJECTNAME__-Info.plist 에서 처리하는 프로토콜을 지정하는 경우에만 유효합니다. 
        /* 
            if (self.invokeString) {
            // 이것은 deviceready 이벤트가 발생하기 전에 전달됩니다. 따라서 당신은 deviceready 를 받았을 때 js에서 액세스할 수 있습니다.
            NSLog(@"DEPRECATED:N(: window.invokeString - 항산 사용자 설정 url 을 통하여 앱이 기동될 때 불리우는 window.handleOpenURL(url) 함수를 대신 사용합니다.");
            NSString * jsString = [NSString stringWithFormat:@"var invokeString = \" % @\ ";", self.invokeString];
            [theWebView stringByEvaluatingJavaScriptFromString:jsString];
        } 
        */ 
        // 배경이 네이티브 앱과 일치하도록 검은 색 
        theWebView.backgroundColor = [UIColor blackColor];
        
        return [super webViewDidFinishLoad: theWebView];
        }
        

*   *Classes/AppViewDelegate.m* 파일을 수정하십시요, 아래와 같이 이중 슬래시를 삽입하고 코멘트 처리한 다름에, **Command-s** 를 사용하여 파일을 저장합니다.:
    
        //self.viewController.invokeString = invokeString;

*   프로젝트를 다시 빌드하여 경고를 제거하려면 **Command-b** 를 누릅니다.

<!-- Does this fix only last until the next "cordova prepare"? -->

**누락된 헤더**: 컴파일시에 누락된 헤더에 관한 오류들은 빌드 위치의 문제로 발생하며 Xcode 환경 설정을 통해 해결할 수 있습니다:

1.  **Xcode → Preferences → Locations** 를 선택합니다.

2.  **Derived Data** 단원에서 **Advanced** 단추를 누르고 다음과 같이 **Build Location** 으로 **Unique** 를 선택합니다.:
    
    ![][11]

 [11]: img/guide/platforms/ios/xcode_build_location.png

이것이 새로운 Xcode 설치의 기본 설정이지만 Xcode의 이전 버전에서 업그레이드에 따라서 다르게 설정되었을 수 도 있습니다.

자세한 내용은 Apple의 설명서를 참조하십시오.

*   [오늘 iOS 앱 개발을 시작하기][12] iOS 앱을 개발하기 위한 단계에 대한 빠른 개요를 제공합니다.

*   [회원 센터 홈 페이지][13] 기술 리소스, 프로비저닝 포털, 배포 가이드 및 커뮤니티 포럼 등 기술 자원을 여러 iOS에 대한 링크를 제공합니다.

*   [iOS 용 도구 워크플로우 가이드][14]

*   [Xcode 사용 설명서][15]

*   애플 월드 와이드 개발자 컨퍼런스 2012 (WWDC2012)에서 [세션 동영상][16]

*   [xcode-select 명령][17]는 하나 이상의 Xcode 가 설치되어 있는 경우에 올바른 버전을 지정하는 데 필요한 도움말입니다.

 [12]: http://developer.apple.com/library/ios/#referencelibrary/GettingStarted/RoadMAPiOS/index.html#//apple_ref/doc/uid/TP40011343
 [13]: https://developer.apple.com/membercenter/index.action
 [14]: http://developer.apple.com/library/ios/#documentation/Xcode/Conceptual/ios_development_workflow/00-About_the_iOS_Application_Development_Workflow/introduction.html#//apple_ref/doc/uid/TP40007959
 [15]: http://developer.apple.com/library/ios/#documentation/ToolsLanguages/Conceptual/Xcode4UserGuide/000-About_Xcode/about.html#//apple_ref/doc/uid/TP40010215
 [16]: https://developer.apple.com/videos/wwdc/2012/
 [17]: http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/xcode-select.1.html

(Mac® OS X® Apple®, Xcode®, App Store℠, iPad®, iPhone®, iPod® 및 Finder® 는 애플 inc의 등록 상표입니다.)