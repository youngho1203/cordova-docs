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

# Config.xml 파일

앱 동작에 대한 여러 특성들은 전역 설정 파일 `config.xml` 을 통하여 설정할 수 있습니다. 플랫폼에 독립적인 이 XML 파일은 W3C의 [웹 응용 프로그램 (위젯) 포장][1] 사양에 기반하여 구성되어 있으며, 몇몇 핵심 코르도바 API 기능, 플러그인, 및 플랫폼 관련 설정에 대하여 확장된 구성을 사용합니다.

 [1]: http://www.w3.org/TR/widgets/

코르도바 CLI (명령줄 인터페이스에 설명된) 를 사용하여 생성된 프로젝트에서는 이 파일은 최상위 디렉터리에서 찾을 수 있습니다.

        app/config.xml
    

이전 버전인 3.3.1-0.2.0 에서는, 이 파일이 `app/www/config.xml` 에 존재하는데, 그곳에 있어도 여전히 동작됩니다.

CLI를 사용하여 프로젝트를 빌드할 때, 이 파일의 각 버전들은 각각의 `platforms/` 하위 디렉터리에 수동적으로 복사됩니다. 예를 들면:

        app/platforms/ios/AppName/config.xml
        app/platforms/blackberry10/www/config.xml
        app/platforms/android/res/xml/config.xml
    

이 단원에서는 전역 및 크로스 플랫폼 구성 옵션들에 대하여 자세히 설명합니다. 특정 플랫폼의 옵션에 대하여는 다음 섹션을 참조 하십시오.

*   iOS 구성
*   안드로이드 구성
*   블랙베리 10 구성

아래에서 상세하게 서술되는 다양한 구성 옵션과 덧붙여, 당신은 각 대상 플랫폼에 대하여 응용 프로그램의 핵심 이미지 묶음들을 구성할 수 있습니다. 자세한 내용은 아이콘 및 시작화면을 참조 하십시오.

## 핵심 구성 요소

이 예제에서는, 명령줄 인터페이스에서 설명되었던, CLI 의 `create` 명령어로 생성된 기본 `config.xml` 를 보여 줍니다.:

        <widget id="com.example.hello" version="0.0.1">
            <name>HelloWorld</name>
            <description>
                A sample Apache Cordova application that responds to the deviceready event.
            </description>
            <author email="dev@callback.apache.org" href="http://cordova.io">
                Apache Cordova Team
            </author>
            <content src="index.html" />
            <access origin="*" />
        </widget>
    

다음의 설정 요소들은 `config.xml` 파일의 최상위 요소로 표시되고, 모든 코르도바 플랫폼에서 지원됩니다:

*   `<widget>`요소의 `id` 특성은 응용 프로그램의 리버스-도메인 식별자를 제공합니다 그리고 `version` 은 그것의 전체 버전 번호로서 메이저/마이너/패치 표기법으로 표현됩니다.
    
    위젯 태그는 버전값을 대신해서 안드로이드에서는 versionCode, iOS에서는 CFBundleVersion 라는 속성을 대신 갖을 수 도 있습니다. 자세한 내용은 아래 추가 버전 관리 섹션을 참조 하십시오.

*   `<name>`요소는 디바이스의 홈 화면과 앱스토어 인터페이스 안에서 나타나는 응용 프로그램의 공식 이름을 지정합니다.

*   `<description>`및 `<author>` 요소들은 메타 데이터 와 앱스토어 목록안에서 사용되는 연락처 정보를 지정합니다.

*   옵션설정인 `<content>` 요소는 최상위 웹 자산(Web Assets) 디렉터리에서 응용 프로그램의 시작 페이지를 정의합니다. 기본값은 `index.html` 이며, 관례적으로 프로젝트의 최상위에 있는 `www` 디렉터리 안에 있습니다.

*   `<access>`요소는 앱과 통신이 허용되는 외부 도메인 집합을 정의합니다. 위에 표시된 기본 값은 모든 서버에 액세스할 수 있습니다. 자세한 내용은 도메인 화이트 리스트 가이드를 참조 하십시오.

*   `<preference>`태그는 `name` / `value` 속성들의 쌍으로 다양한 옵션을 설정합니다. 각 설정의 `name` 값은 대/소문자를 구분하지 않습니다. 각 플랫폼에 대하여 고유한 많은 속성들이 이 페이지의 상단에 나열되어 있습니다. 이어지는 섹션에서는 하나 또는 그 이상의 플랫폼에 적용될 수 있는 상세한 환경 설정을 논의합니다.

### 추가적인 버전 관리

앱스토어에 표시되는 버전값을 지원하기 위하여, 안드로이드와 iOS 둘 다, 안드로이드에 대하여 [versionCode][2], iOS에 대하여 [CFBundleVersion][3] 인 대체 버전 문자열(또는 번호)를 지원합니다. 아래는 versionCode와 CFBundleVersion를 명시적으로 설정하는 예제입니다.

 [2]: http://developer.android.com/tools/publishing/versioning.html
 [3]: http://stackoverflow.com/questions/4933093/cfbundleversion-in-the-info-plist-upload-error

        <widget id="io.cordova.hellocordova"
          version="0.0.1"
          android-versionCode="7"
          ios-CFBundleVersion="3.3.3">
    

만약 대체 버전값이 지정되지 않으면 다음과 같은 기본값이 사용됩니다.

        // assuming version = MAJOR.MINOR.PATCH-whatever
        versionCode = PATCH + MINOR * 100 + MAJOR * 10000
        CFBundleVersion = "MAJOR.MINOR.PATCH"
    

## 전체 환경 설정

아래의 설정은 모든 플랫폼에 적용이 됩니다.

*   `Fullscreen`은 화면 상단의 상태 표시줄을 숨길 수 있습니다. 기본값은 `false` 입니다. 예를 들어:
    
        <preference name="Fullscreen" value="true" />
        

## 멀티 플랫폼 환경 설정

아래의 설정들은 하나 또는 두개 이상의 이상의 플랫폼에서 적용되지만, 모든 플랫폼에 적용되지는 않습니다.

*   `DisallowOverscroll`(boolean, 기본값은 `false` ): `true` 로 설정하면 사용자가 콘텐츠를 스크롤하여 시작 또는 끝에 도착하였을 때 어떠한 피드백도 표시하지 않습니다.
    
        <preference name="DisallowOverscroll" value="true"/>

       안드로이드와 iOS에 적용됩니다. iOS에서 overscroll 제스처는 콘텐츠를 원래 위치쪽으로 다시 반동시키는 작용을 합니다. 안드로이드에서는 콘텐츠의 위쪽 또는 아래쪽 가장자리를 따라 미묘하게 빛나는 효과를 보여줍니다.

*   `BackgroundColor`: 앱의 배경색을 설정합니다. 4 바이트의 16진수값을 지원하며, 첫 번째 바이트는 알파 채널을 의미하고, 뒤의 3 바이트는 표준 RGB 값을 표현합니다. 아래 예제는 파란색을 지정합니다.
    
        <preference name="BackgroundColor" value="0xff0000ff"/>

       안드로이드와 블랙베리에 적용됩니다. 하지만 CSS를 재정의하여 모든 플랫폼으로 확장할 수 있습니다. 예 :`body{background-color:blue}`.

*   `HideKeyboardFormAccessoryBar`(boolean, 기본값은 `false` ): `true` 로 설정하면 키보드 위에 표시되는 추가 도구 모음을 감주게 되고, 사용자가 여러 입력 양식 사이에서 쉽게 이동할 수 있습니다.
    
        <preference name="HideKeyboardFormAccessoryBar" value="true"/>

       블랙베리에 적용됩니다.

*   `Orientation` (문자열, 기본값은 `default`): 기기의 방향이 바뀜에 따라 반응하는 화면의 회전을 잠금처리 할 수 있습니다. 가능한 값은 `default`, `landscape` 또는 `portrait` 입니다. 예를 들어:
    
        <preference name="Orientation" value="landscape" />

       또한, `<platform>` 요소 내에서 `<preference>` 요소를 설정하면 플랫폼에 특정된 방향 값을 지정할 수 있습니다. :

        <platform name="android">
            <preference name="Orientation" value="sensorLandscape" />
        </platform>

       안드로이드, iOS, WP8, 아마존 Fire OS 와 Firefox 운영 체제에 적용됩니다.

      **참고**: `default` 값은 플랫폼의 기본 동작 특성을 보장하기 위하여 코르도바가 매니페스트/설정 파일에 설정된 방향 설정값을 삭제하게 됩니다.

     iOS인 경우에는, 플랫폼에 특정된 `all` 로 값을 설정하면 초상화 모드, 풍경화 모드 모두를 설정할 수 있습니다.

        <platform name="ios">
            <preference name="Orientation" value="all" />
        </platform>

## *기능* 요소

CLI를 사용하여 응용 프로그램을 구축할 경우, 장치 API들을 설정하기 위하여 `plugin` 명령을 사용합니다. 하지만 이것은 최상위 `config.xml` 파일을 수정하지는 않습니다. 따라서 `<feature>` 요소들은 아직 워크플로우에 적용되지 않습니다. 만약 당신이 SDK를 사용해서 플랫폼-중심 `config.xml`을 파일을 소스로 사용하여 작업을 하는 경우에, 장치 수준 API와 외부 플러그인을 설정하기 위하여 `<feature>` 태그를 사용합니다. 그들은 종종 특정 플랫폼 `config.xml` 파일에서 사용자 지정값으로 표현되기도 합니다. 예를 들어 여기에 안드로이드 프로젝트에 대한 장치 API를 지정하는 방법입니다.

        <feature name="Device">
            <param name="android-package" value="org.apache.cordova.device.Device" />
        </feature>
    

다음은 iOS 프로젝트에서 요소가 표시되는 방법입니다.

        <feature name="Device">
            <param name="ios-package" value="CDVDevice" />
        </feature>
    

각 기능을 지정하는 방법에 대한 자세한 내용은 API 문서를 참조하십시오. 플러그인에 대한 자세한 내용은 플러그인 개발 가이드를 참조하십시오.

## *플랫폼* 요소

CLI를 사용하여 응용 프로그램을 구축하는 경우일지라도, 때로는 특정 플랫폼에 대한 설정 또는 요소 설정이 필요한 경우도 있습니다. 이러한 경우에는 단일 특정 플랫폼 `config.xml` 파일에만 지정하여 설정할 수 있는 기능을 가진 `<platform>` 요소를 사용하십시요. 예를 들어 안드로이드에서만 전체 화면을 사용하도록 지정하는 방법입니다.

        <platform name="android">
            <preference name="Fullscreen" value="true" />
        </platform>
    

## *hook* 요소

특정 동작이 발생할 때(예를 들어, 플러그인을 추가한 다음이나 또는 플랫폼에 준비되어 있는 로직이 호출되었을 때) 당신은 코르도바에서 이 동작을 확인할 수 있는 사용자 지정 스크립트를 만들 수 있습니다. 이것은 코르도바의 기본 기능을 확장해야 할 때 매우 유용합니다. 자세한 내용은 후크 가이드를 참조하십시오.

    <hook type="after_plugin_install" src="scripts/afterPluginInstall.js" />