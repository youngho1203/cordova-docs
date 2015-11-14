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

# iOS 구성

`config.xml`파일은 각 응용 프로그램 및 CordovaWebView 인스턴스에 적용되는 앱의 기본 설정을 제어합니다. 이 단원에서는 iOS 빌드에만 적용되는 설정을 자세히 설명합니다. 전역 설정 옵션에 대한 내용은 [config.xml 파일][1]을 참조하십시오.

 [1]: config_ref_index.md.html#The%20config.xml%20File

*   `EnableViewportScale`(boolean, 기본값은 `false` ): `true` 로 설정하면 뷰포트 메타 태그를 사용하지 않도록 설정하거나 사용자 비율의 범위를 제한하는 것을 허용하게 됩니다.
    
        <preference name="EnableViewportScale" value="true"/>
        
    
    스케일링을 해제하여 맞는 HTML에 뷰포트를 위치시켜서, 렌더링 WebView 내에서 유연하게 콘텐츠를 배치합니다.:
    
        <meta name='viewport' content='width=device-width, initial-scale=1, user-scalable=no' />
        

*   `MediaPlaybackAllowsAirPlay`(boolean, 기본값은 `true` ): `false` 로 설정하면 이 보기에 사용 되 고에 어 플레이 방지하기 위해. 기본 UIWebView에 WKWebView 사용할 수 있습니다.
    
        <preference name="MediaPlaybackAllowsAirPlay" value="false"/>
        

*   `MediaPlaybackRequiresUserAction`(boolean, 기본값은 `false` ):`true` 로 설정하면  와 함께 자동으로 재생에서 HTML5 비디오 또는 오디오를 방지 하는 `autoplay` 특성 또는 자바스크립트를 통해.
    
        <preference name="MediaPlaybackRequiresUserAction" value="true"/>
        

*   `AllowInlineMediaPlayback`(boolean, 기본값은 `false` ):`true` 로 설정하면  HTML5 미디어 재생 네이티브 컨트롤 대신 브라우저 제공 컨트롤을 사용하여 화면 레이아웃 내에서 *인라인* 을 표시할 수 있도록. 이 대한 추가 `webkit-playsinline` 속성을 `<video>` 요소.
    
        <preference name="AllowInlineMediaPlayback" value="true"/>
        

*   `BackupWebStorage`(문자열, `none`, `local`, 또는 기본값 `cloud` 중 하나):로 설정 `cloud` 웹 스토리지 데이터를 iCloud 통해 백업 하. 설정 `local` 만 로컬 백업을 아이튠즈 동기화를 통해 수 있도록. 설정 `none` 웹 스토리지 백업 방지.
    
        <preference name="BackupWebStorage" value="local"/>
        

*   `TopActivityIndicator`(문자열, 기본값: `gray` ): 중요한 프로세서 작업을 나타내는 상태 표시줄에 작은 회전 아이콘의 모양을 조정. 유효한 값은 `whiteLarge` , `white` , 그리고`gray`.
    
        <preference name="TopActivityIndicator" value="white"/>
        

*   `KeyboardDisplayRequiresUserAction`(boolean, 기본값은 `true` ):`false` 로 설정하면 키보드를 호출할 때 표시를 수 있도록 `focus()` 폼 입력에.
    
        <preference name="KeyboardDisplayRequiresUserAction" value="false"/>
        

*   `SuppressesIncrementalRendering`(boolean, 기본값은 `false` ):`true` 로 설정하면  화면에 렌더링 하기 전에 모든 콘텐츠 수신 되었습니다 때까지 기다려야.
    
        <preference name="SuppressesIncrementalRendering" value="true"/>
        

*   `GapBetweenPages`(부동, 기본값: `` ): 포인트, 페이지 사이 간격의 크기.
    
        <preference name="GapBetweenPages" value="0"/>
        

*   `PageLength`(부동, 기본값: `` ): 포인트, 페이지 흐름 방향에서 각 페이지의 크기. 때 PaginationMode는 오른쪽에서 왼쪽 또는 왼쪽에서 오른쪽,이 속성은 각 페이지의 너비를 나타냅니다. PaginationMode topToBottom 또는 bottomToTop 인 경우이 속성은 각 페이지의 높이 나타냅니다. 기본값은 0, 레이아웃 뷰포트 크기를 사용하여 페이지의 크기를 결정 하는 것을 의미.
    
        <preference name="PageLength" value="0"/>
        

*   `PaginationBreakingMode`(문자열, 기본값: `page` ): 유효한 값은 `page` 및 `column` . 열 또는 페이지 최신 발생하는 방식. 이 속성에는 특정 CSS 속성에 대한 열 및 페이지 분리 영광 또는 무시 여부를 결정합니다. 이 속성 설정 하면 `column` , 열-속보 페이지 바꿈의 위치에 관련 된 CSS 속성을 존중 하는 콘텐츠.
    
        <preference name="PaginationBreakingMode" value="page"/>
        

*   `PaginationMode`(문자열, 기본값: `unpaginated` ): 유효한 값은 `unpaginated` , `leftToRight` , `topToBottom` , `bottomToTop` , 및 `rightToLeft` . 이 속성은 웹 보기에서 콘텐츠 페이지를 한 번에 보기 한 화면을 채우는으로 또는 하나의 긴 스크롤 보기로 표시 여부 결정. 만약 설정 페이지가 매겨진된 폼에이 속성을 일으키는 relayout에 PageLength와 GapBetweenPages의 값을 사용하여 웹 보기 콘텐츠 내용에 페이지가 매겨진된 레이아웃을 전환 합니다.
    
        <preference name="PaginationMode" value="unpaginated"/>
        

*   `UIWebViewDecelerationSpeed`(문자열, 기본값: `normal` ): 유효한 값은 `normal` , `fast` 입니다. 이 속성은 기세 스크롤의 감속 속도 제어합니다. `normal`대부분의 네이티브 앱에 대한 기본 속도 `fast` 는 모바일 사파리에 대한 기본값입니다.
    
        <preference name="UIWebViewDecelerationSpeed" value="fast" />
        

*   `ErrorUrl`(문자열, 기본값은 설정되어 있지 않음): 값을 설정하면, 응용 프로그램에서 오류에 참조된 로컬 페이지를 표시합니다.
    
        <preference name="ErrorUrl" value="myErrorPage.html"/>
        

*   `OverrideUserAgent`(문자열, 기본값은 설정되어 있지 않음): 값을 설정하면, 값 대체 webview의 오래된 UserAgent. 원격 페이지를 요청할 때 응용 프로그램 또는 브라우저에서 요청을 식별하는 데 도움이 됩니다. 주의이 5 월 사용 웹 서버와 compitiable 문제를 발생합니다. 대부분의 경우, AppendUserAgent를 대신 사용합니다.
    
        <preference name="OverrideUserAgent" value="Mozilla/5.0 My Browser" />
        

*   `AppendUserAgent`(문자열, 기본값은 설정되어 있지 않음): 설정는 경우 값 webview의 오래된 UserAgent의 끝에 추가 됩니다. OverrideUserAgent와 함께 사용하는 경우이 값은 무시됩니다.
    
        <preference name="OverrideUserAgent" value="My Browser" />
        
*   `target-device` (string, 기본값: `universal`): 유효한 값은 `handset`, `tablet`, `universal` 입니다.
  For targeting a specific device family.  This property maps directly to `TARGETED_DEVICE_FAMILY` 
  in the xcode project.
  Note that if you target `universal` (which is the default) you will need to supply screen shots for 
  both iPhone and iPad or your app may be rejected.

        <preference name="target-device" value="universal" />

* `deployment-target` (string, 기본값은 설정되어 있지 않음):
  This sets the `IPHONEOS_DEPLOYMENT_TARGET` in the build, which ultimately tranlsates to the `MinimumOSVersion` in the ipa.
  For more details please refer to Apple's documentation on 
  [`Deployment Target Settings`](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/cross_development/Configuring/configuring.html)

        <preference name="deployment-target" value="7.0" />

* `CordovaWebViewEngine` (string, 기본값: 'CDVUIWebViewEngine'):
  This sets the WebView engine plugin to be used to render the host app. The plugin must conform to the CDVWebViewEngineProtocol protocol. The 'value' here should match the 'feature' name of the WebView engine plugin that is installed. This preference usually would be set by the WebView engine plugin that is installed, automatically.
  
        <preference name="CordovaWebViewEngine" value="CDVUIWebViewEngine" />

* `target-device` (string, 기본값: `universal`): 유효한 값은 `handset`, `tablet`, `universal` 입니다. 
  For targeting a specific device family.  This property maps directly to `TARGETED_DEVICE_FAMILY` 
  in the xcode project.
  Note that if you target `universal` (which is the default) you will need to supply screen shots for 
  both iPhone and iPad or your app may be rejected.

        <preference name="target-device" value="universal" />

* `deployment-target` (string, 기본값은 설정되어 있지 않음): 이것은 빌드에서 최종적으로 ipa 에 있는 `MinimumOSVersion` 으로 변환이 되는 `IPHONEOS_DEPLOYMENT_TARGET` 값을 설정합니다. 보다 상세한 내역은 Apple 의 문서를 참조바랍니다.[`Deployment Target Settings`](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/cross_development/Configuring/configuring.html)

        <preference name="deployment-target" value="7.0" />

* `CordovaWebViewEngine` (string, 기본값: 'CDVUIWebViewEngine'): 이값은 host 앱에서 렌더를 위하여 사용되는 WebView 엔진 플러그인을 설정합니다. 이 플러그인은 CDVWebViewEngineProtocol 프로토콜을 준수하여야 합니다. 여기서 '설정값'은 설치되어 있는 WebView 엔진의 'feature' 이름과 일치하여야 합니다. 이 설정은 자동적으로 설치되어 있는  WebView 엔진 플러그인에 의하여 설정이 됩니다.
  
        <preference name="CordovaWebViewEngine" value="CDVUIWebViewEngine" />

