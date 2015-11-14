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

# deviceready

이 이벤트는 코르도바가 완전히 로드될 때 발생합니다.

    document.addEventListener("deviceready", yourCallbackFunction, false);
    

## 세부 정보

이 이벤트는 모든 응용 프로그램에 필수적입니다. 이것은 코르도바의 장치 API가 로드되었고 액세스할 준비가 되었다는 신호입니다.

코르도바는 두개의 코드 베이스로 구성되어 있습니다.: 네이티브와 자바스크립트. 네이티브 코드를 로드하는 동안 사용자 지정 로딩 이미지를 표시합니다. 그러나, 자바스크립트는 DOM을 로드할 때 한 번만 로드합니다. 이것은, 대응되는 네이티브 코드를 사용할 수 있게 되기 전에 웹 앱 코르도바 자바스크립트 함수 호출이 잠재적으로 발생할 수 있다는 것을 의미합니다.

`deviceready` 이벤트는 코르도바가 완전히 로드되면 발생합니다. 이 이벤트가 발생한 다음에 당신은 안전하게 Cordova API를 사용할 수 있습니다. 응용 프로그램은 일반적으로 HTML 문서의 로드되어 있는 DOM 에 `document.addEventListener`를 사용하여 이벤트 리스너를 첨부합니다.

`deviceready` 이벤트는 다른 것들과는 약간 다르게 동작하는 이벤트 입니다. `deviceready` 이벤트가 발생한 다음 등록된 이벤트 처리기는 발생 즉시 그 것의 콜백 함수를 호출합니다.

## 지원되는 플랫폼

*   아마존 Fire OS
*   안드로이드
*   블랙베리 10
*   iOS
*   타이젠
*   윈도우폰 8
*   윈도우 8

## 빠른 예제

    document.addEventListener("deviceready", onDeviceReady, false);
    
    function onDeviceReady() {
        // Now safe to use device APIs
    }
    

## 완전한 예제

    <!DOCTYPE html>
    <html>
      <head>
        <title>Device Ready Example</title>
    
        <script type="text/javascript" charset="utf-8" src="cordova.js"></script>
        <script type="text/javascript" charset="utf-8">
    
        // Wait for device API libraries to load
        //
        function onLoad() {
            document.addEventListener("deviceready", onDeviceReady, false);
        }
    
        // device APIs are available
        //
        function onDeviceReady() {
            // Now safe to use device APIs
        }
    
        </script>
      </head>
      <body onload="onLoad()">
      </body>
    </html>