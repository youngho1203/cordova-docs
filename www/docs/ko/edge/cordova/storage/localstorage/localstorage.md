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

# 로컬스토리지

W3C의 [웹 스토리지 인터페이스][1] 에 액세스를 제공합니다.

 [1]: http://dev.w3.org/html5/webstorage/#the-localstorage-attribute

    var permanentStorage = window.로컬스토리지;
    var tempStorage = window.sessionStorage;
    

## 메서드

*   **키**: 지정된 된 위치에서 키의 이름을 반환 합니다.

*   **getItem**: 지정된 키로 식별 된 항목을 반환 합니다.

*   **setItem**: 키 항목의 값을 할당 합니다.

*   **removeItem**: 지정된 키로 식별 된 항목을 제거합니다.

*   **취소**: 키/값 쌍을 모두 제거합니다.

## 세부 정보

`window.로컬스토리지`인터페이스는 W3C의 [웹 스토리지 인터페이스][2]를 구현 합니다. 앱 키-값 쌍을 사용하여 영구 데이터를 저장하는 데 사용할 수 있습니다. `window.sessionStorage`인터페이스는 모든 데이터는 응용 프로그램 종료 때마다 지워집니다 제외 하 고 모든 면에서 동일한 방식으로 작동 합니다. 각 데이터베이스는 별도 네임 스페이스를 제공합니다.

 [2]: http://dev.w3.org/html5/webstorage/

## 지원되는 플랫폼

*   안드로이드
*   블랙베리 WebWorks (OS 6.0 및 높은)
*   iOS
*   타이젠
*   윈도우폰 7과 8

## 키 빠른 예제

    var keyName = window.로컬스토리지.key(0);
    

## 설정된 항목 빠른 예제

    window.로컬스토리지.setItem("key", "value");
    

## 항목 빠른 예제를 얻을

        var value = window.로컬스토리지.getItem("key");
        // value is now equal to "value"
    

## 빠른 예제 항목 제거

        window.로컬스토리지.removeItem("key");
    

## 빠른 예를 들어 취소

        window.로컬스토리지.clear();
    

## 전체 예제

    <!DOCTYPE html>
    <html>
      <head>
        <title>Storage Example</title>
    
        <script type="text/javascript" charset="utf-8" src="cordova.js"></script>
        <script type="text/javascript" charset="utf-8">
    
        // Wait for device API libraries to load
        //
        document.addEventListener("deviceready", onDeviceReady, false);
    
        // device APIs are available
        //
        function onDeviceReady() {
            window.로컬스토리지.setItem("key", "value");
            var keyname = window.로컬스토리지.key(i);
            // keyname is now equal to "key"
            var value = window.로컬스토리지.getItem("key");
            // value is now equal to "value"
            window.로컬스토리지.removeItem("key");
            window.로컬스토리지.setItem("key2", "value2");
            window.로컬스토리지.clear();
            // 로컬스토리지 is now empty
        }
    
        </script>
      </head>
      <body>
        <h1>Example</h1>
        <p>로컬스토리지</p>
      </body>
    </html>
    

## 윈도우폰 7 단점

점 표기법은 *없습니다* 윈도우폰 7에서 사용할 수 있습니다. 사용 하십시오 `setItem` 또는 `getItem` 와 같은 저장소 개체에서 직접 키를 액세스 하는 대신`window.로컬스토리지.someKey`.