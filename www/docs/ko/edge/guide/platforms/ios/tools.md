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

# iOS 셸 도구 가이드

이 가이드에는 코르도바의 플랫폼을 중심 셸 도구 세트를 사용하여 iOS 앱을 개발하는 방법을 보여줍니다. 이 개발 경로는 명령줄 인터페이스에 설명된 크로스 플랫폼 CLI 도구 경로보다, 코르도바 소개에서 설명한, iOS를 위한 보다 더 넓은 범위의 개발 옵션을 제공할 수 있습니다. 예를 들어, 당신이 네이티브 구성 요소와 함께 사용자 지정 코르도바 WebView를 배포하는 경우 셸 도구를 사용해야 합니다. 따라서 개발 경로 중 하나를 사용하기 전에, iOS 플랫폼 가이드에서 설명된 것과 같이 먼저 SDK 환경을 구성해야 합니다. 이러한 도구는 `xcode-select` 와 `xcodebuild` 같은 Xcode의 명령줄 도구에 의존합니다.

iOS 위한 셸 도구를 사용하려면 [cordova.apache.org][1]에서 코르도바를 다운로드하십시요. 다운로드는 각 플랫폼에 대한 별도의 아카이브를 포함하고 있습니다. 대상으로 하고 싶은 것의 압축을 해제합니다. 이 경우에는 `ios` 입니다. 관련 도구는 일반적으로 최상위 `bin` 디렉터리에서 사용할 수 있습니다. 그렇지 않으면 자세한 지시 사항에 대하여 **README** 파일을 참조하십시오.

 [1]: http://cordova.apache.org

이러한 도구는 iOS 앱을 작성하고, 구축하고 그리고 실행할 수 있도록 하여 줍니다. 모든 플랫폼에 걸쳐 플러그인 기능을 활성화하는 추가 명령줄 인터페이스에 대한 정보에 관하여, Plugman을 사용한 플러그인 관리를 참조하십시오. 플러그인을 개발하는 방법에 대한 자세한 내용은 응용 프로그램 플러그인을 참조하십시오.

## 프로젝트를 만들기

`create` 명령어를 프로젝트가 위치하는 존재하는 경로, 리버스 도메인 스타일의 패키지 식별자, 그리고 앱의 표시 이름과 함께 실행합니다.

        $ ./path/to/cordova-ios/bin/create /path/to/my_new_project com.example.project_name ProjectName
    

## 프로젝트를 빌드하기

        $ /path/to/my_new_project/cordova/build
    

## 에뮬레이터에서 앱을 실행하기

        $ /path/to/my_new_project/cordova/run --emulator
    

## 장치에서 앱을 실행하기

        $ /path/to/my_new_project/cordova/run --device
    

## 앱에 서명하기

당신은 [iOS 개발자 라이브러리][2]에서 iOS 앱에 서명을 하고, 배포를 하고, 인증서 생성하고, 프로파일을 프로비전닝하기 위한 자세한 내용을 배울 수 있습니다.

 [2]: https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html

코르도바에서 엡에 서명을 하기 위하여 당신은 아래의 내용을 따라야 합니다.

*   Code signing identity ( `--codeSignIdentity` ): [XCode를 사용하여][3] 새로운 iOS signing identity를 만들 수 있으며 키체인에 추가할 수 있습니다. code signing identity 의 유형은 - 일반적으로 배포 또는 개발이며, 여기에서 지정해야 합니다.

*   Provisioning profile ( `--provisioningProfile` ): [애플 회원 센터를 사용하여][4] 당신은 프로비저닝 프로파일을 만들 수 있습니다. 생성한 프로비저닝 프로파일을 컴퓨터에 다운로드하고 그것을 등록하기 위하여 XCode에서 그것을 기동시키십시요. 그러면 당신의 맥에 복사가 됩니다: ~/Library/MobileDevice/Provisioning\ Profiles/. 이것을 텍스트 편집기에서 열면, 여기에서 지정되어 있는 UUID를 찾을 수 있습니다.

*   Code signing identity을 위한 리소스 규칙 ( `--codeSignResourceRules` ) (선택 사항): 사용자 지정 서명 리소스 규칙을 지정할 수 있습니다.

 [3]: https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html#//apple_ref/doc/uid/TP40012582-CH31-SW6
 [4]: https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW61

위의 변수들은 `build` 또는 `run` 스크립트에 명령줄 인수를 사용하여 이러한 매개 변수를 지정할 수 있습니다.

        $ /path/to/my_new_project/cordova/build --codeSignIdentitiy="iPhone Distribtion" --provisioningProfile="926c2bd6-8de9-4c2f-8407-1016d2d12954" 
    

다른 방법으로는, (`-buildConfig`) 인수를 사용하여 빌드 구성 파일 (build.json)에서 그들을 지정할 수 있습니다. 빌드 구성 파일의 예제는 다음과 같습니다.

    {
         "ios": {
             "debug": {
                 "codeSignIdentitiy": "iPhone Development",
                 "provisioningProfile": "926c2bd6-8de9-4c2f-8407-1016d2d12954",
             },
             "release": {
                 "codeSignIdentitiy": "iPhone Distribution"
                 "provisioningProfile": "70f699ad-faf1-4adE-8fea-9d84738fb306",
             }
         }
     }
    

또한 build.json 파일에 정의된 변수값들과 명령줄 인수들을 혼합하여 설정(mix and match)하는 것도 지원이 됩니다. 이때 명령줄 인수에서 주어진 값이 우선 순위를 가집니다.

## 로깅

        $ /path/to/my_new_project/cordova/log