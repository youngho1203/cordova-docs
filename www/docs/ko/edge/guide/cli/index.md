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

# 명령줄 인터페이스

이 가이드에서는 `cordova` 명령줄 인터페이스 (CLI)를 사용하여, 다양한 네이티브 모바일 플랫폼에서, 어떻게 응용 프로그램을 만들고, 배포하는지에 대하여 알아봅니다. 이 도구는 당신이 새로운 프로젝트를 만들고, 서로 다른 다양한 플랫폼에서 그것들을 빌드하고, 실제 장치에서 동작시키거나 또는 에뮬레이터 안에서 실행할 수 있도록 만들어 줍니다. 이 CLI 는 코르도바 소개에서 설명된 것과 같이 크로스 플랫폼 워크플로우를 위한 주요한 도구입니다. 또다른 방법으로 당신은 이 CLI 를 프로젝트의 시작 코드를 생성하는데 사용할 수 있으며, 초기화 후 다양한 플랫폼의 SDK 와 셸 도구를 이용하여 지속적인 개발을 진행할 수 있습니다.

## 필수 구성 요소

명령줄 도구를 실행하기 전에, 당신은 원하는 대상 플랫폼에 대한 SDK 를 먼저 설치해야 합니다. (자세한 내용은 플랫폼 가이드들을 참조하십시오.)

어떤 플랫폼에서든 프로젝트를 다시 작성하거나 추가하기 위하여는, 해당 플랫폼의 SDK가 동작하는 동일한 컴퓨터에서 명령줄 인터페이스를 실행해야 합니다. CLI 는 아래와 같은 조합을 지원합니다.

*   iOS (맥)
*   아마존 Fire OS (맥, 리눅스, 윈도우)
*   안드로이드 (맥, 리눅스, 윈도우)
*   블랙베리 10 (맥, 리눅스, 윈도우)
*   윈도우폰 8 (윈도우)
*   윈도우 (윈도우)
*   파이어폭스 OS (맥, 리눅스, 윈도우)

맥에서는 명령줄이 *터미널* 을 통해 처리가 됩니다. 반면에 PC 에서는, *액세서리* 아래에 있는 *명령 프롬프트* 를 통하여 처리가 됩니다.

**참고**: 윈도우 전용 플랫폼에서도 가상 컴퓨터 환경 또는 듀얼 부팅 모드를 이용하여 여전히 맥 하드웨어용 개발을 진행할 수 있습니다. 보다 상세한 사용 가능한 옵션들에 대하여는 윈도우폰 8 플랫폼 가이드 또는 윈도우 플랫폼 가이드를 참조하십시오.

당신이 서로 다른 장비에서 CLI 를 사용하면 당신은 로컬 작업 디렉터리에 작업 소스를 내려받기 위한 원격 소스 코드 저장소를 운영하는 것이 좀 더 편리할 수 가 있습니다.

## 코르도바 CLI를 설치하기

코르도바 명령줄 도구는 바로 사용할 준비가 되어 있는 형식의 npm 패키지로 배포가 됩니다. 소스로부터 컴파일을 할 필요는 없습니다.

`cordova` 명령줄 도구를 설치하기 위하여는 아래의 단계를 수행 하십시오:

1.  [Node.js][1]를 내려받고 설치를 합니다. 설치에 이어서, 명령줄에서 `node` 및 `npm`을 호출할 수 있어야 합니다. 경우에 따라서 `nvm` 또는 `nave`과 같은 Node.js 설치를 관리할 수 있는 도구들을 사용할 수 있습니다.

2.  [git 클라이언트][2]를 내려받고 설치를 합니다. 설치에 이어서, 명령줄에서 `git` 를 호출할 수 있어야 합니다. 비록 당신이 직접 `git` 를 사용하지 않더라도, CLI는 새 프로젝트를 만들 때 몇 가지 자산을 내려받기 위하여 내부에서 이 명령어를 사용합니다.

3.  Node.js의 유틸리티인 `npm`을 사용하여 `cordova` 모듈을 설치합니다. `cordova`모듈은 `npm` 유틸리티에 의해 자동으로 다운로드 됩니다.

 [1]: http://nodejs.org/
 [2]: http://git-scm.com/

*   OS X와 리눅스:

            $ sudo npm install -g cordova

       OS X와 리눅스에서, `npm` 명령앞에 있는 `sudo`는 `/usr/local/share` 와 같은 제한된 디렉터리에 개발 유틸리티들이 설치되기 때문에 필요할 수 있습니다. 만약 당신이 nvm/nave 도구나 다른 설치 디렉터리에 쓰기 권한이 있는 경우에는 `sudo`를 생략할 수 있습니다. `sudo` 없이 `npm`을 사용할 수 있는 [더 많은 팁][3] 이 있는데 참조하여 사용하시기 바랍니다.

*   윈도우:
    
            C:\>npm install -g cordova

위에서 `cordova` 설치할 때 `npm`에 보낸 `-g`플래그는 코르도바를 전역 명령어로 설치합니다. 그렇지 않으면 `node_modules` 는 현재 작업 디렉터리의 하위 디렉터리로 설치가 됩니다.

이제 전역으로 설치된 `npm` 모듈들을 호출 하려면, 당신의 `PATH`에 `npm` 디렉터리를 추가해야 합니다. 윈도우에서는 일반적으로 `C:\Users\username\AppData\Roaming\npm` 에서 `npm`을 찾을 수 있습니다. 반면 OS X와 리눅스에서는 보통 `/usr/local/share/npm` 에서 찾을 수 있습니다.

설치로그는 설치되지 않은 플랫폼의 SDK들에 대한 오류를 생성할 수 있습니다.

설치한 다음에, 아무런 인수가 없는 `cordova` 명령줄 명령어를 실행하면 도움말 텍스트가 화면에 보여야 합니다.

 [3]: http://justjs.com/posts/npm-link-developing-your-own-npm-modules-without-tears

## 앱 만들기

당신의 소스 코드를 관리할 수 있는 디렉터리로 가서 아래의 명령어를 실행합니다.:

        $ cordova create hello com.example.hello HelloWorld
    

시간이 좀 걸릴 수 있습니다. 잠시 기다리기 바랍니다. 이 명령을 `-d` 옵션과 함께 실행하면 진행 상황에 대한 정보가 표시됩니다.

첫 번째 인수인 *hello*는 당신의 프로젝트를 위하여 생성될 디렉터리를 지정합니다. 이 디렉터리는 미리 존재하지 말아야 하며, 코르도바가 당신을 위해 만들 것입니다. 그 디렉터리 안의 `www` 디렉터리에는 `css` , `js` , 및 `img` 아래에 일반적인 웹 개발 파일 명명 규칙을 따르는 다양한 리소스와 응용 프로그램의 홈 페이지가 들어 있습니다. 이러한 것들은 장치의 로컬 파일 시스템에 저장되며, 원격으로는 제공되지 않습니다. `config.xml`파일은 응용 프로그램을 생성하고 배포하는 데 필요한 중요한 메타 데이터를 포함합니다.

두 번째 인수인 `com.example.hello`는 역방향 도메인 스타일의 식별자를 당신의 프로젝트에 부여합니다. 이 인수는 선택 사항이지만 다음 인수의 위치가 설정되어 있기 때문에 세 번째 인수를 생략하는 경우에만 생략이 가능합니다. 이 값은 나중에 `config.xml` 파일에서 편집할 수 있지만, `config.xml` 의 밖에서 코드를 생성할 때, 자바 패키지 이름등의 값으로 사용될 수 있음을 알고 있어야 합니다. 기본값은 `io.cordova.hellocordova`이지만, 당신이 적절한 값을 설정하여야 합니다.

세 번째 인수인 `HelloWorld`는 응용 프로그램의 디스플레이 타이틀을 제공합니다. 이 인수는 선택 사항입니다. 이 값은 나중에 `config.xml` 파일에서 편집할 수 있지만, `config.xml` 의 밖에서 코드를 생성할 때, 자바 클래스 이름등의 값으로 사용될 수 있음을 알고 있어야 합니다. 기본값은 `HelloCordova`이지만, 당신이 적절한 값을 설정하여야 합니다.

## 플랫폼 추가하기

이어지는 모든 후속 명령어들은 프로젝트의 디렉터리 또는 해당 범위 내에서 모든 하위 디렉터리 안에서 실행을 해야 합니다.

        $ cd hello
    

프로젝트를 구성하기 전에, 먼저 대상 플랫폼들을 지정해야 합니다. 이때 당신의 컴퓨터가 각 SDK를 지원하는지 여부와 SDK를 설치하였는지에 따라서 코르도바 명령어들의 동작여부가 결정됩니다. 맥에서는 다음중 하나를 실행합니다.

        $ cordova platform add ios
        $ cordova platform add amazon-fireos
        $ cordova platform add android
        $ cordova platform add blackberry10
        $ cordova platform add firefoxos
    

윈도우 시스템에서는 다음중 하나를 실행합니다. 이때 *wp*는 윈도우폰 운영 체제의 버전을 말합니다.

        $ cordova platform add wp8 
        $ cordova platform add windows
        $ cordova platform add amazon-fireos 
        $ cordova platform android 
        $ cordova platform add blackberry10 
        $ cordova platform add firefoxos
    

현재 설정되어 있는 플랫폼의 집합을 확인하려면 다음을 실행하십시요:

        $ cordova platforms ls
    

(참고는 `platform` 및 `platforms` 명령을 동의어로 사용됩니다.)

설정되어 있는 플랫폼을 제거하려면 다음 동의어 명령 중 하나를 실행합니다.

        $ cordova platform remove blackberry10
        $ cordova platform rm amazon-fireos
        $ cordova platform rm android
    

플랫폼을 지정하거나 제거하는 명령어는, 지정된 각 플랫폼은 프로젝트 *platforms* 디렉터리의 하위 디렉터리로 나타나기 때문에, 프로젝트의 *platforms* 디렉터리 내용에 영향을 줍니다. *www* 소스 디렉터리는 각 플랫폼의 하위 디렉터리 내에서, 예를 들면 `platforms/ios/www` 또는 `platforms/android/assets/www` 처럼, 반복되어 나타나게 됩니다. CLI는 소스 *www* 폴더에서 지속적으로 파일을 복사하기 때문에, 당신은 이곳의 파일만을 수정할 수 있지, *platforms* 하위 디렉터리 아래에 있는 것은 수정해서는 안됩니다. 만약 당신이 버전 제어 소프트웨어를 사용하는 경우에는, 버전 제어 시스템을 위하여, *merges* 폴더와 함께 이 소스 *www* 폴더를 추가해야 합니다. ( *merges* 폴더에 대한 자세한 정보는 아래의 각 플랫폼 사용자 지정 단원에서 찾을 수 있습니다.)

**경고**: CLI를 사용하여 응용 프로그램 구성하는 경우에, 당신이 지금 하고 있는 것이 무엇을 하고 있는지에 대하여 충분히 알고 있거나, 문서에 특별하게 규정되어 있는 경우를 제외하고는, `/platforms/` 디렉터리 안에 있는 어떠한 파일도 수정하여서는 안됩니다. 이 디렉터리에 있는 파일들은 빌드를 준비하거나, 플러그인을 재설치 하는 경우 주기적으로 덮어 쓰여집니다.

이 시점에서 원한다면, 생성되어진 프로젝트를 열기위하여 이클립스나 Xcode SDK를 사용할 수 있습니다. 이때 SDK로 개발을 진행하기 위하여는 `/platforms/` 디렉터리의 각 플랫폼에 맞게 파생되어 있는 자산들을 같이 열어야 합니다. 왜냐하면, 각 SDK를 위한 메타 데이터 파일이 `/platform/` 아래의 해당 디렉터리에 저장되어 있기 때문입니다. (각 IDE 를 사용하여 응용 프로그램을 개발하는 방법에 대한 내용은 플랫폼 가이드들을 참조하십시오.) 단순히 CLI를 사용하여 프로젝트를 초기화 한 다음 네이티브 작업을 위하여 SDK를 전환하는 경우 이 방법을 사용합니다.

다음은 전체 개발 주기에서 크로스-플랫폼 워크플로우(CLI)를 사용하고자 하는 경우에 읽어 보시기 바랍니다.

## 앱 빌드하기

기본으로 `cordova create` 스크립트는 프로젝트의 홈 페이지가 `www/index.html`파일인 웹 기반 응용 프로그램의 골격을 생성합니다. 필요한 경우 이 응용 프로그램을 수정하십시요. 하지만 모든 초기화 작업은 `www/js/index.js`에서 참조되어 있는 `deviceready` 이벤트 처리의 일부분으로 지정해야만 합니다.

반복적으로 프로젝트를 빌드하려면 다음 명령을 실행하십시요:

        $ cordova build
    

이 명령어는 프로젝트의 `platforms` 하위 디렉터리에 각 플랫폼별 코드를 생성합니다. 필요에 따라서 특정 플랫폼에 매번 빌드 범위를 제한할 수 도 있습니다.

        $ cordova build ios
    

`cordova build`명령어는 아래와 같은 단일 플랫폼을 대상으로한 명령어의 축약 명령어입니다.:

        $ cordova prepare ios
        $ cordova compile ios
    

여기에서, `prepare`를 실행한 다음에, 코르도바가 `platforms/ios` 아래에 생성한 플랫폼별 코드를 수정하고 컴파일하는데 코르도바 대신 애플의 Xcode SDK를 사용할 수 있습니다. 다른 플랫폼의 SDK로도 동일한 접근 방식을 사용할 수 있습니다.

## 에뮬레이터 또는 장치에서 앱 테스트

모바일 플랫폼을 위한 SDK는 주로 장치 이미지를 실행하는 에뮬레이터와 함께 번들로 공급됩니다. 에뮬레이터를 사용하여 홈 화면에서 앱을 기동시킬수 있으며, 많은 플랫폼 기능과 어떻게 상호 작용하는지 알 수 도 있습니다. 아래의 명령어는 앱을 다시 구성하고 특정 플랫폼의 에뮬레이터 안에서 앱이 구동되는 것을 보여줍니다.

        $ cordova emulate android
    

일부 모바일 플랫폼에서는, iOS 프로젝트의 아이폰처럼, 기본으로 특정 장치를 에뮬레이션하도록 설정되어 있습니다. 그러나 다른 플랫폼의 경우에는 에뮬레이터에서 처음에 기동할 장치를 설정할 필요가 있습니다.

**참고**: 아직 아마존 Fire OS에는 에뮬레이터를 사용할 수 없습니다.

(자세한 내용은 플랫폼 가이드를 참조하십시오.) 예를 들어, 당신은 안드로이드 SDK 기동시키기 위하여 `android` 명령을 실행한 다음에, 기본 설정에 따라 기동되는 특정 장치 이미지를 실행할 수 있습니다.:

![][4]

 [4]: img/guide/cli/android_emulate_init.png

위의 그림에서 `cordova emulate` 명령어는 에뮬레이터의 이미지가 홈 화면에서 기동시킬 수 있는 가장 최신 응용 프로그램들이 표시되는 것으로 고쳐지는 것을 볼 수 있습니다.

![][5]

 [5]: img/guide/cli/android_emulate_install.png

또는 당신의 컴퓨터에 휴대폰을 연결하고 직접 응용 프로그램을 테스트할 수도 있습니다.:

        $ cordova run android
    

이 명령을 실행하기 전에 테스트를 위한 장치를 설정하여야 합니다. 장치를 설정하는 절차를 각 플랫폼마다 다릅니다. 안드로이드와 아마존 Fire OS 장치에서는, 아마도 개발 환경에 따라 USB 드라이버를 추가해야 할지도 모르지만, 장치에서 **USB 디버깅** 옵션을 사용가능으로 설정하여야 합니다. 자세한 각 플랫폼의 요구 사항에 대한 내용은 플랫폼 가이드를 참조하십시오.

## 플러그인 기능 추가하기

새로운 프로젝트를 구성하고, 앱을 구동시켜 보면 기본 기능은 매우 적습니다. 당신은 표준 웹 기술의 장점을 활용하여 여러 가지 방법으로 앱을 수정할 수 있습니다. 하지만 앱이 다양한 장치 수준의 기능과 밀접하게 통신을 하기 위해서는 핵심 코르도바 API에 대한 액세스를 제공하는 플러그인을 추가해야 합니다.

*플러그인*은 네이티브 구성 요소와 인터페이스를 제공하는 작은 부가 기능의 코드입니다. 예를 들어 당신이 네이티브 요소를 가진 코르도바 WebView가 혼합된 하이브리드 앱을 디자인할 때 자신의 플러그인 인터페이스를 디자인할 수 있습니다. (자세한 내용은 임베딩 WebViews 및 [플러그인 개발 가이드][6] 를 참조 하십시요.) 더 일반적으로, API 참조에서 자세히 설명한, 코르도바의 기본 장치 수준 기능 중 하나를 사용하는 플러그인을 추가할 수 도 있습니다.

 [6]: guide_hybrid_plugins_index.md.html#Plugin%20Development%20Guide

버전 3.0에서, 코르도바 프로젝트 만들 때 어떤 플러그인도 설치가 되지 않습니다. 이것은 새로운 기본 동작입니다. 심지어 코어 플러그인조차도, 당신이 원하는 어떤 플러그인도 명시적으로 추가되어야 합니다.

이러한 플러그인의 목록들은, 커뮤니티에 의해 제공된 추가적인 타사 플러그인을 포함하여, [plugins.cordova.io][7] 레지스트리에서 찾을 수 있습니다. CLI를 사용하여 이 레지스트리에서 플러그인에 대한 검색을 할 수 있습니다. 예를 들어 `bar` 와 `code`를 검색하면 대소문자 구분없이 두 단어가 포함된 단일 결과를 생성합니다.:

 [7]: http://plugins.cordova.io/

        $ cordova plugin search bar code
    
        com.phonegap.plugins.barcodescanner - Scans Barcodes
    

만약 `bar` 문자만 검색한다면 추가적인 결과를 보여줍니다.:

        cordova-plugin-statusbar - Cordova StatusBar Plugin
    

`cordova plugin add` 명령어는 플러그 코드를 위한 저장소를 지정해서 사용하여야 합니다. 여기에서 앱에 기능들을 추가하기 위하여 CLI를 사용하는 방법을 알아 봅니다.

*   기본 장치 정보 (장치 API):
    
        $ cordova plugin add cordova-plugin-device
        

*   네트워크 연결 및 배터리 이벤트:
    
        $ cordova plugin add cordova-plugin-network-information
        $ cordova plugin add cordova-plugin-battery-status
        

*   가속도계, 나침반, 및 위치 정보:
    
        $ cordova plugin add cordova-plugin-device-motion
        $ cordova plugin add cordova-plugin-device-orientation
        $ cordova plugin add cordova-plugin-geolocation
        

*   카메라, 미디어 재생 및 캡처:
    
        $ cordova plugin add cordova-plugin-camera
        $ cordova plugin add cordova-plugin-media-capture
        $ cordova plugin add cordova-plugin-media
        

*   장치 또는 네트워크 (파일 API) 파일 접근:
    
        $ cordova plugin add cordova-plugin-file
        $ cordova plugin add cordova-plugin-file-transfer
        

*   대화 상자 또는 진동 알림:
    
        $ cordova plugin add cordova-plugin-dialogs
        $ cordova plugin add cordova-plugin-vibration
        

*   연락처:
    
        $ cordova plugin add cordova-plugin-contacts
        

*   세계화:
    
        $ cordova plugin add cordova-plugin-globalization
        

*   시작화면:
    
        $ cordova plugin add cordova-plugin-splashscreen
        

*   새로운 브라우저 윈도우 열기 (InAppBrowser):
    
        $ cordova plugin add cordova-plugin-inappbrowser
        

*   콘솔 디버깅:
    
        $ cordova plugin add cordova-plugin-console
        

**참고**: CLI는 각 플랫폼에 대하여 해당하는 플러그인 코드를 추가합니다. 만약 당신이 코드도바 소개에서 설명한 것 처럼 낮은 수준의 셸 도구 또는 플랫폼 SDK를 사용하여 개발을 하고자 할 때에는  각 플랫폼에 대해 별도로 플러그인을 추가하는 Plugman 유틸리티를 사용해야 합니다. (자세한 내용은 Plugman을 사용한 플러그인 관리를 참조 바랍니다.)

현재 설치되어 있는 플러그인들을 보려면 `plugin ls` (또는 `plugin list` , 또는 `plugin` 자체)를 사용합니다. 보여지는 것들은 서로의 식별자에 의해 구분됩니다.

        $ cordova plugin ls    # or 'plugin list'
        [ 'cordova-plugin-console' ]
    

설치되어 있는 플러그인을 제거하려면 목록에서 나타나는 같은 동일한 식별자를 사용하여야 합니다. 예를 들어, 아래에서 릴리스 버전에서 어떻게 디버그 콘솔을 제거하는지에 대한 방법을 알 수 있습니다.

        $ cordova plugin rm cordova-plugin-console
        $ cordova plugin remove cordova-plugin-console    # same
    

각 명령에 하나 이상의 인수를 지정하여 플러그인을 일괄 제거하거나 추가할 수 있습니다.:

        $ cordova plugin add cordova-plugin-console cordova-plugin-device
    

## 고급 플러그인 옵션들

플러그인을 추가할 때 어디에서 플러그인을 가져오게 하는지 설정하기 위한 몇가지 옵션을 지정할 수 있습니다. 위의 예제는 잘 알려진 `registry.cordova.io` 레지스트리에서 `id` 로 정의된 플러그인에 의해 지정된 것을 가지고 옵니다.:

        $ cordova plugin add cordova-plugin-console
    

`id`는 문자 `@` 뒤에 따라오는 플러그인의 버전 번호를 포함할 수도 있습니다. `latest`은 최신 버전에 대한 별칭입니다. 예를 들어:

        $ cordova plugin add cordova-plugin-console@latest
        $ cordova plugin add cordova-plugin-console@0.2.1
    

플러그인이 `registry.cordova.io` 에 등록 되지 있지는 않지만 다른 git 저장소에 위치하고 있다면, 다른 URL을 지정할 수 도 있습니다.:

        $ cordova plugin add https://github.com/apache/cordova-plugin-console.git
    

위의 git 예제는 마스터 브랜치의 마지막에서 플러그인을 가지고 오지만, `#` 문자뒤에 태그 또는 브랜치와 같은 대체 git-ref 를 지정할 수 도 있습니다.:

태그에서 설치:

        $ cordova plugin add https://github.com/apache/cordova-plugin-console.git#r0.2.0
    

또는 브랜치에서 설치:

        $ cordova plugin add https://github.com/apache/cordova-plugin-console.git#CB-8438cordova-plugin-console
    

또는 git-ref 특정 커밋일 수 도 있습니다:

        $ cordova plugin add https://github.com/apache/cordova-plugin-console.git#f055daec45575bf08538f885e09c85a0eba363ff
    

만약 플러그인이 (그리고 `plugin.xml` 파일이) git repo 내에서 하위 디렉터리에 있다면 `:` 문자를 사용하여 지정할 수 있습니다. 참고로 `#` 문자는 여전히 필요합니다.:

        $ cordova plugin add https://github.com/someone/aplugin.git#:/my/sub/dir
    

또한 git-ref와 하위 디렉터리를 결합할 수 도 있습니다.

        $ cordova plugin add https://github.com/someone/aplugin.git#r0.0.1:/my/sub/dir
    

또한 `plugin.xml` 파일를 가지고 있는 로컬 경로의 플러그인 디렉터리를 지정할 수 도 있습니다.:

        $ cordova plugin add ../my_plugin_dir
    

## 각 플랫폼에서 사용자 지정 *병합*을 사용하기

코르도바를 사용하면 쉽게 많은 다른 플랫폼을 위한 앱을 배포할 수 있지만, 때로는 사용자 지정 사항을 추가해야 합니다. 이 경우, 최상위 디렉터리의 `platforms` 디렉터리에 있는 각 플랫폼의 `www` 디렉터리에 있는 소스 파일들을 수정해서는 않됩니다. 왜냐하면 그것들은 최상위로 `www` 디렉터리의 크로스-플랫폼 소스로 정기적으로 대체가 되기 때문입니다.

대신에, 최상위 `merges` 디렉터리가 특정 플랫폼을 위하여 배포하는 자산을 지정하는 장소를 제공합니다. `merges` 안의 각 플랫폼별 하위 디렉터리는 `www` 소스트리의 디렉터리구조와 똑같이 반영하여야 하고, 당신은 필요에 따라 파일을 추가하거나 덮어 쓸 수 있습니다. 예를 들어 여기에 안드로이드와 아마존 Fire OS 장치에 대한 기본 글꼴 크기를 처음부터 변경하는 `merges`의 사용법에 대하여 알아봅니다.:

* `www/index.html`파일에 CSS 파일, 이 경우 `overrides.css`, 의 링크를 추가하는 수정을 하여 봅시다.:
    
        <link rel="stylesheet" type="text/css" href="css/overrides.css" />
        

*   선택사항으로 비어있는 `www/css/overrides.css` 파일을 생성하면, 안드로이드 빌드가 아닌 경우 누락 파일 오류를 방지할 수 있습니다.

*   `merges/android` 안에서 `css` 하위 디렉터리를 생성하고, 해당하는 `overrides.css` 파일을 추가합니다. `www/css/index.css` 에서 지정되어 있는 12 포인트 기본 글꼴 크기의 CSS를 재정의합니다. 예를 들면:
    
        body { font-size:14px; }
        

프로젝트를 다시 빌드하면, 안드로이드은 지정된 글꼴 크기를 갖추고 있지만, 다른 플랫폼의 것들은 변하지 않고 그대로 유지되고 있습니다.

당신은 또한 원 `www` 디렉터리에는 존재하지 않는 파일들을 추가하는데 `merges`를 사용할 수 있습니다. 예를 들어, 앱의 _뒤로 가기 버튼_ 그림이 iOS 인터페이스의 경우 `merges/ios/img/back_button.png` 에 저장되어 있지만, 안드로이드 버전에서는 `backbutton` 이벤트를 잡아서 해당하는 하드웨어 버튼을 사용할 수 있습니다.

## 도움말 명령

코르도바는 몇가지의 전역 명령어를 가지고 있는데, 이것들은 당신이 문제가 발생하였을 경우 도음이 될 것입니다. `help` 명령은 모든 사용 가능한 코르도바 명령 및 구문을 표시합니다.:

    $ cordova help
    $ cordova        # same
    

또한, 특정 명령에 대하여 더 자세한 도움말을 얻을 수 도 있습니다. 예를 들면:

    $ cordova run --help
    

`info` 명령은 현재 설치된 플랫폼, 플러그인, 각 플랫폼의 SDK 버전 및 `node.js` 와 CLI 의 버전등 잠재적으로 유용한 정보의 목록을 생성합니다.:

    $ cordova info
    

이것을 모두 화면에 보이고 로컬에서 `info.txt` 파일로 출력합니다.

**참고**: 현재, iOS 및 안드로이드 플랫폼에만 사용할 수 있습니다.

## 코르도바 및 프로젝트 업데이트

`cordova` 유틸리티를 설치한 후에 당신은 언제든지 다음 명령을 실행하여 가장 최근 버전으로 업데이트할 수 있습니다.:

        $ sudo npm update -g cordova
    

이 구문을 사용하여 특정 버전을 설치할 수 도 있습니다.

        $ sudo npm install -g cordova@3.1.0-0.2.0
    

`cordova -v` 을 실행하면 현재 실행 중인 버전을 볼 수 있습니다. `npm info`는 현재 버전과 함께 사용 가능한 모든 버전 번호를 포함한 긴 목록을 보여주는 명령어입니다.:

        $ npm info cordova
    

코르도바 3.0은 이 단원에서 설명하는 명령줄 인터페이스를 지원하는 최초의 버전입니다. 이전 버전에서 3.0으로 업데이트한다면, 위에서 설명한 대로 새 프로젝트를 만든 다음, 이전 응용 프로그램의 내용들을 최상위 `www` 디렉터리에 복사를 해야 합니다. 3.0로의 업그레이드에 대한 자세한 내용은 플랫폼 가이드들에서 사용할 수 있습니다. 일단 `cordova` 명령줄 인터페이로 업그레이드 하면, `npm update`를 사용하여 최신 버전을 유지하십시요. 이제 많은 시간이 걸리는 절차는 더 이상 없습니다.

코르도바 3.0+는 여전히 프로젝트 수준 디렉터리 구조와 다른 종속성등 다양한 변경을 요구합니다. 코르도바 자체를 업데이트 하기 위하여 위의 `npm` 명령을 실행한 후에, 프로젝트의 리소스들이 최신 버전의 요구 사항에 부합되고 있는지 당신은 확인을 해야 합니다. 구축하려는 각 플랫폼에 대하여 다음과 같은 명령을 실행합니다.

        $ cordova platform update android
        $ cordova platform update ios
        ...etc.