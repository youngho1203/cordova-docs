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

# 화이트 리스트 가이드

도메인 화이트 리스팅은 당신의 앱이 관리할 수 없는 외부 도메인의 접속을 관리하는 보안 모델입니다. 코르도바는 접속할 수 있는 외부 사이트들을 설정할 수 있는 보안 정책을 제공합니다. 기본적으로 새로 생성된 앱은 어떤 사이트에도 접속이 허용하도록 설정됩니다. 따라서 당신은 응용 프로그램을 정식으로 발표하기 전에 화이트 리스트를 공식화하고 특정 네트워크 도메인 및 하위 도메인에 대한 접속만을 허용해야 합니다.

안드로이드와 iOS에 대하여 (현재 그들의 4.0 버전), 코르도바의 보안 정책은 플러그인 인터페이스를 통하여 확장됩니다. 당신의 앱은 이전 버전 보다 더 나은 보안 및 구성방식을 제공하는 [화이트 리스트 코르도바 플러그인][1]를 사용해야 합니다. 당신은 자신의 화이트 리스트 플러그인을 구현할 수 있지만, 당신의 앱이 매우 구체적인 보안 정책을 필요로 하지 않는 한 권장하지 않습니다. 자세한 사용 및 구성에 대한 내용은[화이트 리스트 코르도바 플러그인][1]을 참조하십시오.

 [1]: https://github.com/apache/cordova-plugin-whitelist

다른 플랫폼에 대하여는 코르도바는 [W3C 위젯 접속][2]사양을 준수합니다. 이 사양은 특정 도메인에 대한 네트워크 접속을 허용하도록 설정하려면 `config.xml` 파일에서 `< access >` 요소에 설정하여야 합니다. 프로젝트에서는 명령줄 인터페이스에서 설명된 CLI 워크플로우에서는, 이 파일은 프로젝트의 최상위 디렉터리에 있습니다. 그렇지 않고 특정 플랫폼 개발인 경우에는, 각 위치는 아래 단원에 나열됩니다. (각 플랫폼에 대한 자세한 내용은 플랫폼 가이드를 참조하십시오.)

 [2]: http://www.w3.org/TR/widgets-access/

다음 예에서는 `<access>` 화이트 리스트 구문을 보여줍니다.

*   [Google.com][3]에 접속하기:
    
        <access origin="http://google.com" />
        

*   안전하게 [google.com][4]로 접속하기 ( `https://` ):
    
        <access origin="https://google.com" />
        

*   하위 도메인 [maps.google.com][5]으로 접속하기:
    
        <access origin="http://maps.google.com" />
        

*   [google.com][3]의 모든 하위 도메인에 접속하기, 예를 들면 [mail.google.com][6] 및 [docs.google.com][7]접속:
    
        <access origin="http://*.google.com" />
        

*   [google.com][3] 및 [developer.mozilla.org][8]등 *모든* 도메인에 대한 접속:
    
        <access origin="*" />
        
    
   이 설정은 새로 생성되는 CLI 프로젝트의 기본값입니다.

 [3]: http://google.com
 [4]: https://google.com
 [5]: http://maps.google.com
 [6]: http://mail.google.com
 [7]: http://docs.google.com
 [8]: http://developer.mozilla.org

일부 웹 사이트들은 그들의 홈 페이지를 자동으로 https 프로토콜을 사용하거나 또는 특정 국가 도메인으로 리디렉션 할 수 있다는 점을 유의하십시오. 예를 들어 http://www.google.com 은 SSL/TLS를 사용하도록 https://www.google.com 로 리디렉션한 다음에 https://www.google.co.uk와 같이 지역에 따라 추가 리디렉션을 할 수 있습니다. 이러한 시나리오는 초기 요구 사항을 넘어 추가로 수정하거나 추가 목록 항목을 필요로 할 수 있습니다. 당신의 화이트 리스트를 작성할 때 이 점을 고려하여야만 합니다.

화이트 리스트는 코르도바 webview에만 적용되며 InAppBrowser webview 또는 시스템 웹 브라우저에서의 열기 링크에는 적용되지 않는 점을 참고바랍니다.

## 아마존 Fire OS 화이트 리스팅

플랫폼 특정 화이트 리스팅 규칙은 `res/xml/config.xml` 에서 찾을 수 있습니다.

## 안드로이드 화이트 리스팅

위의 [화이트 리스트 코르도바 플러그인][1]에 대한 자세한 내용을 참조하십시오. 코르도바-안드로이드 4.0.0 이전 버전은,이 설명서의 이전 버전을 참조하십시오.

## iOS 화이트 리스팅

위의 [화이트 리스트 코르도바 플러그인][1]에 대한 자세한 내용을 참조하십시오. 코르도바-ios 4.0.0 이전 버전은, 이 설명서의 이전 버전을 참조하십시오.

## 블랙베리 10 화이트 리스팅

화이트 리스팅 허용 규칙은 `www/config.xml` 에서 찾을 수 있습니다.

블랙베리 10 에서 와일드 카드의 사용법은 다른 플랫폼과 두 가지 방법으로 다릅니다.

*   `XMLHttpRequest` 를 사용하여 접속할 모든 콘텐츠는 명시적으로 선언해야 합니다. 이 경우 `origin="*"` 설정은 작동하지 않습니다. 블랙베리 구성에서 설명된 `WebSecurity` 의 설정으로 모든 웹 보안은 비활성화 될 수 있습니다.
    
        <preference name="websecurity" value="disable" />
        

*   `*.domain`의 대체 설정값으로, 추가적인 `subdomains` 속성을 `true`로 설정합니다. 이것의 기본값은 `false` 입니다. 예를 들어 다음 설정은 `google.com`, `maps.google.com`및 `docs.google.com`에 접속할 수 있습니다:
    
        <access origin="http://google.com" subdomains="true" />
        
    
    다음은 `google.com` 에만 접속을 허용합니다.:
    
        <access origin="http://google.com" subdomains="false" />
        
    
    로컬 `file://` 프로토콜을 포함하여 모든 도메인에 대한 접속 허용은 다음과 같습니다.
    
        <access origin="*" subdomains="true" />
        

(보다 자세한 내용은 블랙베리의 [접속 요소][9] 설명서를 참조하십시오.)

 [9]: https://developer.blackberry.com/html5/documentation/ww_developing/Access_element_834677_11.html

## Firefox 운영 체제

파이어폭스 OS에서는 특정 도메인 대한 화이트 리스팅 개념이 존재하지 않습니다. 대신 [SystemXHR][10]라는 특수 사용 권한이 있습니다. 이 권한을 `Config.xml`에 추가해야 합니다.:

 [10]: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest#Permissions

    <platform name="firefoxos">
        <permission name="systemXHR" privileged="true" description="load data from server" />
    </platform>
    

`XMLHttpRequest` 개체는 두 개의 매개 변수 `mozAnon` 와 `mozSystem`와 함께 인스턴스화할 수 있습니다.

    var request = new XMLHttpRequest({
        mozAnon: true,
        mozSystem: true});
    

이 솔루션은 투명하기 때문에 다른 플랫폼과의 차이가 없습니다.

## 윈도우폰 화이트 리스팅

윈도우폰 8에 대한 허용 규칙은  앱의 `config.xml` 파일에서 찾을 수 있습니다.

## 타이젠 화이트 리스팅

허용 규칙은 앱의 `config.xml` 파일에 있습니다. 이 플랫폼은 블랙베리 플랫폼과 동일한 `subdomains` 특성을 사용합니다. (보댜 자세한 내용은 타이젠의 [접속 요소][11] 설명서를 참조하십시요.)

 [11]: https://developer.tizen.org/help/index.jsp?topic=%2Forg.tizen.web.appprogramming%2Fhtml%2Fide_sdk_tools%2Fconfig_editor_w3celements.htm