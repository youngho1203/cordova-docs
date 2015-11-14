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

# 안드로이드 구성

`config.xml`파일은 각 응용 프로그램 및 CordovaWebView 인스턴스에 적용되는 앱의 기본 설정을 제어합니다. 이 단원에서는 안드로이드 빌드에만 적용되는 설정을 자세히 설명합니다. 전역 설정 옵션에 대한 내용은 [config.xml 파일][1]을 참조하십시오.

 [1]: config_ref_index.md.html#The%20config.xml%20File

*   `KeepRunning`(boolean, 기본값은 `true` ): `pause` 이벤트가 발생한 다음에 응용 프로그램을 백그라운드에서 계속 실행할지 여부를 설정합니다. 이 값을 `false`로 설정하면 `pause` 이벤트가 발생한 다음에 앱은 끝나지 않고 백그라운드에 있지만, 코르도바 webview 내에서 단순히 코드의 실행이 중지됩니다.
    
        <preference name="KeepRunning" value="false"/>
        

*   `LoadUrlTimeoutValue`(밀리초 단위 숫자, 기본값은 `20000`, 20 초): 페이지를 로드할 때, 시간 초과 오류를 던지기 전에 대기할 시간. 이 예제에서는 20초가 아닌 10초를 규정하고 있습니다.
    
        <preference name="LoadUrlTimeoutValue" value="10000"/>
        

*   `SplashScreen`(문자열, 기본값: `splash` ): `res/drawable` 디렉터리에 있는 파일의 이름에서 확장자를 뺀 이름. 모든 자산들은 하위 디렉터리에서 이 이름을 공유해야 합니다.
    
        <preference name="SplashScreen" value="mySplash"/>
        

*   `SplashScreenDelay`(기본값: 밀리초 단위 숫자 `3000` ): 시작화면 이미지가 표시되는 시간을 설정합니다.
    
        <preference name="SplashScreenDelay" value="10000"/>
        

*   `InAppBrowserStorageEnabled`(boolean, 기본값은 `true` ): InAppBrowser 에서 연 화면에서 기본 브라우저를 이용하여 연 화면처럼 로컬스토리지 및 WebSQL 저장 장치를 접속할 수 있도록 할 지에 대한 설정을 합니다.
    
        <preference name="InAppBrowserStorageEnabled" value="true"/>
        

*   `LoadingDialog`(문자열, 기본값은 `null` ): 설정이 되면, 응용 프로그램의 첫 번째 페이지를 로드할 때 지정된 제목 및 메시지, 그리고 회전자와 함께 대화 상자가 표시됩니다. 제목 및 메시지는 쉼표로 구분된 문자열이며, 쉼표는 대화 상자 표시 되기 전에 제거됩니다.
    
        <preference name="LoadingDialog" value="My Title,My Message"/>
        

*   `LoadingPageDialog`(문자열, 기본값: `null` ): `LoadingDialog`와 동일하지만, 응용 프로그램에서 첫 번째 페이지 다음의 모든 페이지를 로드를 위한 것입니다.
    
        <preference name="LoadingPageDialog" value="My Title,My Message"/>
        

*   `ErrorUrl`(URL, 기본값은 `null` ): 설정이 되면, 오류발생시에 "응용 프로그램 오류" 대화 상자 대신 오류에 참조된 페이지를 표시합니다.
    
        <preference name="ErrorUrl" value="myErrorPage.html"/>
        

*   `ShowTitle`(boolean, 기본값은 `false` ): 화면 상단에 제목을 표시합니다.
    
        <preference name="ShowTitle" value="true"/>
        

*   `LogLevel`(문자열, 기본값: `ERROR` ): 응용 프로그램에서 로그 메시지를 필터링하는 최소한의 로그 수준을 설정합니다. 유효한 값은 `ERROR` , `WARN` , `INFO` , `DEBUG` , 그리고`VERBOSE` 입니다.
    
        <preference name="LogLevel" value="VERBOSE"/>
        

*   `SetFullscreen`(boolean, 기본값은 `false` ): xml 파일의 전역 구성 매개 변수인 `Fullscreen` 과 동일합니다. 이 안드로이드에 한정된 요소는 `Fullscreen` 요소를 우선 사용함에 따라서 이후 버전에서 제거될 예정입니다.

*   `AndroidLaunchMode`(문자열, 기본값: `singleTop` ): Activity `android:launchMode` 속성을 설정합니다. 이것은 앱이 아이콘 이나 intent에서 시작할 때 이미 실행 중인 것으로 변경됩니다. 유효한 값은 `standard` , `singleTop` , `singleTask` ,`singleInstance`.
    
        <preference name="AndroidLaunchMode" value="singleTop"/>

*   `DefaultVolumeStream`(문자열, 기본값은 `default`, 코르도바-안드로이드 3.7.0 에서 추가): 볼륨을 하드웨어 볼륨 버튼에 링크로 연결합니다. 기본값은 휴대폰에서는 "call" 그리고 테블릿에서는 "media" 입니다. 따라서 만약 "media" 로 설정하면 당신앱의 볼륨 버튼은 항상 미디어의 볼륨만을 조정하게 됩니다. 만약 코르도바 미디어 플러그인을 사용하고 있다면, 볼륨 버튼은 미디어 개체가 활성화되면 미디어 볼륨을 제어하도록 동적으로 변경됩니다.

*   `OverrideUserAgent` (문자열, 기본값은 설정되어 있지 않음): 설정이 되면, 설정값이 webview의 이전 UserAgent 값을 대체하게 됩니다. 이 설정은 원격 페이지를 요청할 때 앱 또는 브라우저에서의 요청을 식별하는 데 도움이 됩니다. 이것은 웹 서버와 호환성 문제를 발생할 수 있기 때문에 조심해서 사용하여야 합니다. 대부분의 경우에, AppendUserAgent를 대신 사용합니다.
    
        <preference name="OverrideUserAgent" value="Mozilla/5.0 My Browser" />

*   `AppendUserAgent` (문자열, 기본값은 설정되어 있지 않음): 설정이 되면, 설정값이 webview의 이전 UserAgent의 끝에 추가 됩니다. OverrideUserAgent와 함께 사용하는 경우에는 이 설정값은 무시됩니다.
    
        <preference name="OverrideUserAgent" value="My Browser" />