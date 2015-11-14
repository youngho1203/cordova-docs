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

# 안드로이드 플랫폼 가이드

이 가이드에서는 안드로이드 장치에 코르도바 앱들을 배포하기 위한 SDK 환경 설정 방법과 당신의 개발 워크플로우에서 안드로이드-중심의 명령줄 도구를 사용하기 위한 방법을 보여줍니다. 당신이 플랫폼-중심 셸 도구를 사용하든 아니면 크로스-플랫폼 코르도바 CLI를 사용하여 개발하든 안드로이드 SDK를 설치해야 합니다. 두 가지 개발 경로에 대한 비교는 코르도바 소개를 참조하십시오. CLI에 대한 자세한 내용은, 명령줄 인터페이스를 참조하십시오.

## 요구 사항 및 지원 사항

안드로이드를 위한 코르도바는 OS X, 리눅스 또는 윈도우 운영 체제에 설치할 수 있는 안드로이드 SDK를 필요로 합니다. 안드로이드 SDK의 [시스템 요구 사항][1]를 참조바랍니다.

 [1]: http://developer.android.com/sdk/index.html#Requirements

코르도바는 안드로이드 4.0.x(안드로이드 API 레벨 14로 시작) 또는 그 이상을 지원합니다. 일반적으로, 코르도바에가 지원하지 않는 안드로이드 버전들은 Google의 [배포 대시보드][2]에 의하면 5% 아래를 보이고 있습니다. API 레벨 10보다 이전의 안드로이드 버전, 그리고 3.x 버전 (허니콤, API 수준 11-13)는 임계값 5% 보다 월씬 아래로 내려가 있습니다.

 [2]: http://developer.android.com/about/dashboards/index.html

## 코르도바 셸 도구 설치하기

만약 당신이 SDK와 코르도바의 안드로이드-중심 셸 도구를 사용하려면 [cordova.apache.org][3]에서 코르도바를 다운로드 합니다. 그렇지 않고 명령줄 인터페이스에서 설명된 크로스 플랫폼 CLI 도구를 사용하려는 경우에는 이 단원을 무시하기 바랍니다.

 [3]: http://cordova.apache.org

내려받은 코르도바는 각 플랫폼에 대하여 별도의 저장소를 포함합니다. 이 경우 `android`는 적절한 저장소를 확보해야 하기 때문에 빈 디렉터리 내에서 실행해야 합니다. 그러면 실행 유틸리티들이 최상위 `bin` 디렉터리에 설치가 됩니다. (보다 자세한 설명이 필요한 경우 **README** 파일을 참조 하십시요.)

이 셸 도구들을 사용하여 안드로이드 앱을 작성, 구축 및 실행할 수 있습니다. 명령줄 인터페이스에서 모든 플랫폼에 걸쳐 플러그인 기능을 활성화 하는 기능에 대한 정보는 Plugman을 사용한 플러그인 관리를 참조하십시오. 플러그인을 개발하는 방법에 대한 내용은 응용 프로그램 플러그인을 참조하십시오.

## 자바 개발 키트 (JDK) 설치

[자바 개발 키트 (JDK) 7][4] 또는 그 이후 버전 설치.

 [4]: http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html

윈도우에 설치할 때 JDK 설치 경로 (예: C:\Program Files\Java\jdk1.7.0_75)를 `JAVA_HOME` 환경 변수로 설정해야 합니다.

## 안드로이드 SDK 설치

[안드로이드 스튜디오][5]또는 [안드로이드 독립 실행형 SDK 도구][6]를 설치합니다. 만약 당신이 안드로이드 플러그인을 위한 새로운 코르도바를 개발하거나, 안드로이드 플랫폼에서 디버깅 및 실행을 하기 위한 네이티브 도구를 사용하려 계획하는 경우 `안드로이드 스튜디오`를 설치하십시요. 그렇지 않으면, `안드로이드 독립 실행형 SDK 도구`만 설치하여도 안드로이드 응용 프로그램 빌드 및  배포에 충분합니다.

 [5]: http://developer.android.com/sdk/installing/index.html?pkg=studio
 [6]: http://developer.android.com/sdk/installing/index.html?pkg=tools

자세한 설치 지침을 위의 설치 링크에 있는 지침을 확인하십시요.

코르도바 명령줄 도구 또는 이 도구들에 기초한 CLI 로 작업을 진행할 때, 여러분의 `PATH`에 SDK의 `tools` 및 `platform-tools` 디렉터리가 포함돠어 있어야 합니다. 맥 이나 리눅스에는 `~/.bash_profile` 파일을 텍스트 편집기를 사용하여, SDK의 설치에 따라, 다음 줄을 추가합니다.:

        export PATH=${PATH}:/Development/android-sdk/platform-tools:/Development/android-sdk/tools
    

`~/.bash_profile` 에 있는 이 줄 내용은 새로 연 터미널 창에서 적용이 됩니다. 만약 당신의 터미널 창이 이미 OSX 에서 열려져 있거나 또는 리눅스에 로그 아웃/로그인을 피하고 싶다면, 열려 있으면 현재 터미널 창에서 아래 명령어를 실행하여 적용시킬 수 있습니다.

        $ source ~/.bash_profile
    

윈도우에서 `PATH` 환경 변수를 수정하기 위하여는:

1.  바탕 화면 왼쪽 아래에 있는 **시작** 메뉴를 클릭 하십시오 **컴퓨터**에서 마우스 오른쪽 단추로 클릭하고, **속성** 을 선택하십시요.

2.  왼쪽 열에서 **고급 시스템 설정** 을 선택합니다.

3.  결과 대화 상자에서 눌러 **환경 변수** 를 선택합니다.

4.  **PATH** 변수를 선택하고 **편집** 을 누릅니다.

5.  다음은 설치된 SDK 의 위치를 `PATH` 값에 추가합니다. 예를 들면:
    
        ;C:\Development\android-sdk\platform-tools;C:\Development\android-sdk\tools
        

6.  값을 저장하고 두 대화 상자를 닫습니다.

## SDK 패키지 설치하기

안드로이드 SDK 관리자를 열고(예를 들어 터미널에서: `android` 입력) 설치를 시작합니다.:

1.  안드로이드 5.1.1 (API 22) 플랫폼 SDK
2.  안드로이드 SDK 빌드 도구 버전 19.1.0 또는 그 이상
3.  안드로이드 지원 저장소 (엑스트라)

자세한 내용은 [SDK 패키지 설치][7] 를 참조하십시오.

 [7]: http://developer.android.com/sdk/installing/adding-packages.html

## 에뮬레이터를 구성하기

안드로이드 sdk는 기본적으로 어떠한 에뮬레이터 인스턴스도 제공하지 않습니다. 하지만 명령줄에서 `android` 를 실행하여 새로운 것을 만들 수 있습니다. **Tools → Manage AVDs** (안드로이드 가상 장치)를 클릭하고, 다음에 **Device Definitions** 결과 대화 상자에서 원하는 항목을 선택합니다.

![][8]

 [8]: img/guide/platforms/android/asdk_device.png

**Create AVD**을 누룹니다. 선택적으로 이름을 수정할 수 있으며, 변경 내용을 적용 하려면 **OK**를 누릅니다.

![][9]

 [9]: img/guide/platforms/android/asdk_newAVD.png

그러면 **Android Virtual Devices** 목록에 AVD 가 나타납니다.

![][10]

 [10]: img/guide/platforms/android/asdk_avds.png

별도 응용 프로그램으로 에뮬레이터를 열려면 AVD를 선택하고 **Start**을 누릅니다. 이제 하드웨어 버튼까지 컨트롤할 수 있는 장치가 기동됩니다.:

![][11]

 [11]: img/guide/platforms/android/asdk_emulator.png

더 빠른 실행 속도를 위해 `가상 머신 가속기`을 사용할 수 있습니다. 현대의 많은 CPU는 가상 머신을 보다 효율적으로 실행하기 위한 확장기능을 제공합니다. 이러한 유형의 가속기를 적용하기 전에, 지금 개발하고 있는 시스템의 CPU가 다음과 같은 가상화 기술을 지원하는지 확인해야 합니다.

*   **인텔 가상화 기술** (VT-x, vmx) → [인텔 VT x 지원 프로세서 목록][12]
*   **AMD 가상화** (AMD-V, SVM), 리눅스에 대해서만 지원 (2006년 5월부터 AMD 셈프론을 제외한 모든 CPU, AMD-V 포함).

 [12]: http://ark.intel.com/products/virtualizationtechnology

인텔 프로세서가 VT-x 기술을 지원하는지 확인하는 다른 방법은, `인텔 프로세서 식별 유틸리티`를 실행하여 알 수 있습니다. `윈도우`인 경우 인텔 [다운로드 센터][13]에서 다운로드할 수 있거나 `OS 독립` 적인 것은 [booteable 유틸리티][14]를 사용할 수 있습니다.

 [13]: https://downloadcenter.intel.com/Detail_Desc.aspx?ProductID=1881&DwnldID=7838
 [14]: https://downloadcenter.intel.com/Detail_Desc.aspx?ProductID=1881&DwnldID=7840&lang=eng

윈도우에서 `인텔 프로세서 식별 유틸리티`를 설치하고 실행하면, 아래와 같은 CPU 가상화 기술을 지원하는지 확인할 수 있는 창이 열리게 됩니다.:

![][15]

 [15]: img/guide/platforms/android/intel_pid_util_620px.png

에뮬레이터를 가속화하기 위하여,  `인텔 하드웨어 가속 실행 관리자 (HAXM)` 뿐만아니라, 하나 또는 그 이상의 `인텔 x 86 Atom` 시스템 이미지를 내려받고 설치를 해야 합니다.

안드로이드 SDK 관리자를 열고, 테스트 하려는 버젼의 `인텔 x 86 Atom` 시스템 이미지을 선택합니다. 다음 `엑스트라` 로 이동하여 `인텔 x86 에뮬레이터 가속기 (HAXM)`를 선택하고, 선택한 패키지를 설치합니다.:

![][16]

 [16]: img/guide/platforms/android/asdk_man_intel_image_haxm.png

다운로드 한 후, `extras/intel/Hardware_Accelerated_Execution_Manager`에서 안드로이드 SDK에서 사용할 수 있는 인텔 설치 관리자를 실행합니다. **참고**:`패키지 설치에 어떤 문제가 있는 경우 자세한 정보 및 다음의 단계별 지침에서 도움을 찾을 수 있습니다` [인텔 문서][17].

 [17]: http://software.intel.com/en-us/android/articles/speeding-up-the-android-emulator-on-intel-architecture

1.  `인텔 하드웨어 가속 실행 관리자` 뿐만 아니라, 하나 이상의 `인텔 x 86 Atom` 시스템 이미지를 설치합니다. **엑스트라** 에서 설치할 수 있습니다.

2.  `extras/intel/Hardware_Accelerated_Execution_Manager` 에서 안드로이드 SDK에서 사용할 수 있는 인텔 설치 프로그램을 실행합니다.

3.  인텔 이미지가 설정되어 있는 대상으로 새로운 AVD를 만듭니다.

4.  에뮬레이터를 시작할 때 HAX 모듈을 로드하는 데 실패를 나타내는 오류 메시지가 없는 것을 확인합니다.

## 새 프로젝트 만들기

이 시점에서, 새 프로젝트를 만들기 위하여 명령줄 인터페이스에서 설명한 크로스 플랫폼 CLI 도구와 안드로이드 셸 도구들중 어느 것을 사용할지 선택할 수 있습니다. CLI 방식인 경우 소스 코드 디렉터리에서 :

        $ cordova create hello com.example.hello HelloWorld
        $ cd hello
        $ cordova platform add android
        $ ccordova prepare              # or "cordova build"
    

다음은 유닉스와 윈도우에 대한 해당하는 낮은 수준의 셸 도구 방식입니다.

        $ /path/to/cordova-android/bin/create /path/to/new/hello com.example.hello HelloWorld
        C:\path\to\cordova-android\bin\create.bat C:\path\to\new\hello com.example.hello HelloWorld
    

## 프로젝트를 빌드하기

CLI를 사용하는 경우 프로젝트 디렉터리의 최상위 `www` 디렉터리에 소스 파일이 들어 있습니다. 이프로젝트 디렉터리 내에서  응용 프로그램을 다시 빌드하려면 아래와 같이 실행합니다.

        $ cordova build                   # build all platforms that were added
        $ cordova build android           # build debug for only Android
        $ cordova build android --debug   # build debug for only Android
        $ cordova build android --release # build release for only Android
    

안드로이드 셸 도구를 사용하는 경우는 다르게 접근합니다. 일단 프로젝트를 생성하면 앱의 소스는 기본으로 `assets/www` 하위 디렉터리에 설치됩니다. 이어지는 명령들은 그것의 `cordova` 하위 디렉터리에서 사용할 수 있습니다.

`build` 명령은 프로젝트 파일들을 청소하고 응용 프로그램을 다시 빌드합니다. 다음은 맥과 윈도우 모두에 대한 구문입니다. 예제의 첫 번째 쌍은 디버깅 정보를 생성하고, 두 번째는 릴리스를 위한 앱을 빌드합니다.:

        $ /path/to/project/cordova/build --debug
        C:\path\to\project\cordova\build.bat --debug
    
        $ /path/to/project/cordova/build --release
        C:\path\to\project\cordova\build.bat --release
    

## 앱을 배포하기

`cordova` CLI 유틸리티를 사용하여 명령줄에서 에뮬레이터 또는 장치에 응용 프로그램을 배포할 수 있습니다.

        $ cordova emulate android       #to deploy the app on a default android emulator
        $ cordova run android --device  #to deploy the app on a connected device
    

그렇지 않으면 셸 인터페이스를 사용하여:

        $ /path/to/project/cordova/run --emulator
        $ /path/to/project/cordova/run --device
    

당신은 **cordova run android --list** 를 이용하여 사용할 수 있는 모든 대상을 확인할 수 있으며, **cordova run android --target=target_name** 을 사용하여 특정 장치 또는 에뮬레이터에서 응용 프로그램을 실행할 수 있습니다.(예를 들어 `cordova run android --target="Nexus4_emulator"`).

또한 **cordova run --help** 을 사용하여 빌드와 실행 옵션들을 확인할 수 있습니다.

이제 홈 화면에 앱을 보내고 앱을 기동시킵니다.:

![][18]

 [18]: img/guide/platforms/android/emulator2x.png

당신이 앱을 `run` 시킬때, 당신은 또한 앱을 `build` 합니다. 당신은 추가적으로 `--debug`, `--release`, 그리고 `--nobuild` 플래그를 붙혀서 앱을 빌드할지 아니면 필요할 때만 빌드할지 제어할 수 있습니다.:

        $ /path/to/project/cordova/run --emulator --nobuild
    

## 다른 명령들

다음 명령어는 실행할 때 앱의 자세한 로그를 발생시킵니다.:

        $ /path/to/project/cordova/log
        C:\path\to\project\cordova\log.bat
    

다음은 프로젝트 파일들을 정리합니다.:

        $ /path/to/project/cordova/clean
        C:\path\to\project\cordova\clean.bat
    

## SDK에서 새 프로젝트를 엽니다

일단 안드로이드 플랫폼에 당신의 프로젝트가 추가되면 [안드로이드 스튜디오][5]에서 그것을 열 수 있습니다.

1.  **안드로이드 Studio** 응용 프로그램을 시작합니다.

2.  **프로젝트 가져오기(이클립스 ADT, Gradle, 등)**를 선택합니다.
    
    ![][19]

3.  안드로이드 플랫폼 저장된(`your/project/platforms/android`)위치를 선택합니다.
    
    ![][20]

4.  `Gradle 동기화` 질문에 단순히 **네**를 답할 수 있습니다.

 [19]: img/guide/platforms/android/asdk_import_project.png
 [20]: img/guide/platforms/android/asdk_import_select_location.png

이제 당신은 모두를 선택하고 빌드를 할 수 있으며, `안드로이드 스튜디오` 에서 직접 앱을 실행할 수 있습니다.

![][21]

 [21]: img/guide/platforms/android/asdk_import_done.png

[안드로이드 스튜디오 개요][22] 를 참조하고, 더 자세한 내용은 [안드로이드 스튜디오에서 빌드 및 실행하기][23]에서 참조 할 수 있습니다.

 [22]: http://developer.android.com/tools/studio/index.html
 [23]: http://developer.android.com/tools/building/building-studio.html