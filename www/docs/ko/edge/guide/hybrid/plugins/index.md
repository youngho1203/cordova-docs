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

# 플러그인 개발 가이드

*플러그인*은 webview안에서 코르도바가 앱이 실행되는 동안에 네이티브 플랫폼과 통신할 수 있도록 만들어 주기 위하여 삽입된 코드 패키지입니다. 플러그인은 일반적으로 웹 기반 앱에서 처리할 수 없는 장치 또는 플랫폼 기능에 대한 액세스를 제공합니다. 모든 주요 코르도바 API 기능들은 모두 플러그인으로 구현되어 있으며, NFC 통신, 바코드 스캐너와 같은 기능 또는 맞춤 달력 인터페이스등 많은 다른 기능들을 사용할 수 있습니다. 사용 가능한 플러그인의 저장소는 [레지스트리][1] 입니다.

 [1]: http://plugins.cordova.io

플러그인은 지원되는 각 플랫폼에 대한 해당 네이티브 코드 라이브러리들과 단일 자바스크립트 인터페이스로 구성되어 있습니다. 이러한 형식은 공통의 자바스크립트 인터페이스 뒤로 다양한 플랫폼의 네이티브 코드로 된 구현체들을 숨깁니다.

이 단원에서는 자바스크립트에서 네이티브 플랫폼으로 문자열을 전달하고 다시 받는 간단한 *에코* 플러그인을 단계별로 만들어 봅니다. 한번 이러한 모델을 만들어 보면 훨씬 더 복잡한 기능을 구축하는 모델로 사용할 수 있습니다. 이 단원에서는 기본 플러그인 구조와 외부와 접한 자바스크립트 인터페이스를 설명합니다. 각 네이티브 인터페이스에 대하여는 이 단원의 끝에 있는 목록을 참조하십시요.

여기의 지침과 함께, 플러그인을 만들 때는 안내서로 [기존의 플러그인][2]들을 살펴보는 것이 좋습니다.

 [2]: http://cordova.apache.org/#contribute

## 플러그인을 빌드하기

응용 프로그램 개발자는 CLI를 사용하여 `plugin add` (명령줄 인터페이스에서 설명된) 명령을 프로젝트에 적용하기만 하면 됩니다. 해당 명령에 대한 인수는 플러그인 코드가 포함된 *git* 저장소에 대한 URL입니다. 아래는 예제로 코르도바의 장치 API를 구현하는 방법입니다.

        $ cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-device.git
    

플러그인 저장소는 `plugin.xml` 매니페스트 파일에서 최상위 기능(feature) 이어야만 합니다. 이 파일을 설정하는 방법은 여러가지가 있는데 자세한 사항은 플러그인 사양을 참조하여 주시기 바랍니다. `Device` 플러그인을 사용하는 간단한 예제의 모델로 약식 버젼이 아래에 있습니다.:

        <?xml version="1.0" encoding="UTF-8"?>
        <plugin xmlns="http://apache.org/cordova/ns/plugins/1.0"
                id="cordova-plugin-device" version="0.2.3">
            <name>Device</name>
            <description>Cordova Device Plugin</description>
            <license>Apache 2.0</license>
            <keywords>cordova,device</keywords>
            <js-module src="www/device.js" name="device">
                <clobbers target="device" />
            </js-module>
            <platform name="ios">
                <config-file target="config.xml" parent="/*">
                    <feature name="Device">
                        <param name="ios-package" value="CDVDevice"/>
                    </feature>
                </config-file>
                <header-file src="src/ios/CDVDevice.h" />
                <source-file src="src/ios/CDVDevice.m" />
            </platform>
        </plugin>
    

최상위 `plugin` 태그의 `id` 속성은 플러그인 패키지를 식별하기 위한 것으로, 앱을 식별하기 위하여 도입하였던 것과 같은 리버스 도메인 형식을 사용합니다. `js-module`태그는 공통 자바스크립트 인터페이스에 경로를 지정합니다. `platform`태그는 해당하는 네이티브 코드의 집합을 지정하는데, 이 예제에서는 `ios` 플랫폼에 대한 내용을 설정하고 있습니다. `config-file` 태그는 플랫폼로 달리 추가되는 코드들을 구분하기 위한 플랫폼별 `config.xml` 파일에 주입되는 `feature` 태그를 캡슐화한 것입니다. `header-file`와 `source-file` 태그는 라이브러리의 구성 요소 파일들의 경로를 지정합니다.

## 플러그인을 검증하기

당신은 `plugman` 유틸리티를 사용하여 플러그인이 각 플랫폼에 대하여 설치가 올바르게 되었는지 여부를 확인할 수 있습니다. 아래의 [노드][3] 명령을 사용하여 `plugman` 을 설치합니다.:

 [3]: http://nodejs.org/

        $ npm install -g plugman
    

이때 프로젝트의 디렉토리는 명령줄 인터페이스에 설명된 대로, CLI로 생성한 프로젝트가 기본으로 가지는, 최상위 `www` 디렉터리 같은 유효한 앱 소스가 있는 디렉터리이어야만 합니다. 또한 앱의 `index.html` 홈 페이지가 플러그인의 자바스크립트 인터페이스의 이름을 참조하고 있는지 확인해야 합니다.:

        <script src="myplugin.js"></script>
    

다음에 iOS 종속성들이 제대로 로드되는지 여부를 테스트하려면 다음 명령을 실행합니다.:

         $ plugman install --platform ios --project /path/to/my/project/www --plugin /path/to/my/plugin
    

더 자세한 `plugman` 옵션에 대한 내용은 Plugman을 사용한 플러그인 관리를 참조하십시오. 실제로 플러그인을 *디버깅* 하는 방법에 대한 정보는 이 페이지의 맨 아래에 나열된 각 플랫폼의 네이티브 인터페이스 참조하십시요.

## 자바스크립트 인터페이스

자바스크립트는 플러그인에서 아마도 가장 중요한 부분인 전면 인터페이스를 제공합니다. 당신이 선호하는 구조로 플러그인의 자바스크립트 구조를 만들 수 있습니다. 그러나 다음 구문을 사용하여 네이티브 플랫폼과 교신을 할 수 있도록 `cordova.exec` 를 호출할 수 있어야 합니다.:

        cordova.exec(function(winParam) {},
                     function(error) {},
                     "service",
                     "action",
                     ["firstArgument", "secondArgument", 42, false]);
    

여기에서 각 매개 변수의 역할은 다음과 같습니다.:

*   `function(winParam) {}`: 성공 콜백 함수입니다. 당신의 `exec` 호출이 성공적으로 완료되면, 이 함수는 전달된 매개 변수와 함께 실행됩니다.

*   `function(error) {}`: 오류 콜백 함수입니다. 작업이 성공적으로 완료되지 않은 경우에, 이 함수는 오류 매개 변수와 함께 실행됩니다.

*   `"service"`: 네이티브쪽을 호출하기 위한 서비스 이름입니다. 이것은 네이티브 클래스에 해당 합니다. 더 많은 정보는 아래에 나열된 네이티브 가이드를 참조하여 주시기 바랍니다.

*   `"action"`: 네이티브쪽을 호출하기 위한 작업 이름입니다. 이것은 일반적으로 네이티브 클래스의 메서드에 해당합니다. 아래에 나열된 네이티브 가이드를 참조하십시오.

*   `[/* arguments */]`: 네이티브 환경에 전달할 인수 배열입니다.

## 샘플 자바스크립트

이 예제에서는 플러그인의 자바스크립트 인터페이스를 구현하는 방법을 보여줍니다.

        window.echo = function(str, callback) {
            cordova.exec(callback, function(err) {
                callback('Nothing to echo.');
            }, "Echo", "echo", [str]);
        };
    

이 예제에서는 플러그인을 `window` 개체의 `echo` 함수로 만들었습니다. 플러그인 사용자는 다음과 같이 사용할 수 있습니다.:

        window.echo("echome", function(echoValue) {
            alert(echoValue == "echome"); // should alert true.
        });
    

`cordova.exec` 함수의 마지막 세 인수를 주목하여 주십시요. 그 첫 번째는 `Echo` *서비스*를 호출하는 클래스 이름입니다. 두 번째는 그 클래스 안에 있는 `echo` *작업* 메서드를 요청하고 있습니다. 세 번째는 인수들의 배열인데, `window.echo` 함수의 첫 번째 매개 변수인 에코문자열을 포함하고 있습니다.

`exec`로 전달되는 성공 콜백은 단순히 `window.echo`를 가르키는 레퍼런스입니다. 만약 네이티브 플랫폼에서 오류 콜백이 발생하는 경우 그것은 성공 콜백을 호출하고 단순히 기본 문자열을 전달합니다.

## 네이티브 인터페이스

일단 당신의 플러그인에 대한 자바스크립트를 정의하였으면, 적어도 하나의 네이티브에 대한 구현을 만들어야 합니다. 각 플랫폼에 대한 세부 정보는 아래목록을 참조하십시요. 여기에는 위의 간단한 에코 플러그인 예제를 구현하는 방법이 설명되어 있습니다.:

*   아마존 Fire OS 플러그인
*   안드로이드 플러그인
*   iOS 플러그인
*   블랙베리 10 플러그인
*   윈도우폰 8 플러그인
*   윈도우 플러그인

타이젠 플랫폼은 플러그인을 지원하지 않습니다.

## 플러그인을 게시하기

일단 당신의 플러그인이 개발되면, 그것을 게시하고 커뮤니티와 함께 공유할 수 있습니다. 당신은 어떠한 `npmjs` -기반 레지스트리에도 당신의 플러그인을 게시할 수 있습니다. 하지만 권장하는 곳은 [NPM 레지스트리][4]입니다. [npm 에 플러그인을 게시하기 위한 가이드][5]를 참조 하시기 바랍니다.

 [4]: https://www.npmjs.com
 [5]: http://plugins.cordova.io/npm/developers.html

**참고**: [코르도바 플러그인 레지스트리][6]는 읽기 전용 상태로 전환됩니다. `publish`/ `unpublish` 명령어는 `plugman`에서 제거되었으며, 따라서 당신은 해당하는 `npm` 명령어를 사용하여야 합니다.

 [6]: https://plugins.cordova.io

다른 개발자들도 `plugman` 또는 코르도바 CLI를 사용하여 자동으로 귀하의 플러그인을 설치할 수 있습니다. (각 개발 경로에서 보다 자세한 내용은, Plugman을 사용한 플러그인 관리와 명령줄 인터페이스를 참조하시기 바랍니다.)

NPM 레지스트리에 플러그인을 게시하려면 아래 단계를 수행해야 합니다.

*   귀하의 플러그인에 대한 `package.json` 파일 만들기:
    
        $ plugman createpackagejson /path/to/your/plugin
        

*   게시하기:
    
        $ npm adduser # 아직 사용자 계정이 없으면 이것을 실행하십시요.
        $ npm publish /path/to/your/plugin
        

이제 다 되었습니다.!

`plugman --help` 를 실행하면 사용할 수 있는 레지스트리 기반 명령 목록을 보여줍니다.