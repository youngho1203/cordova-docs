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

# 스토리지

> 코르도바를 위한 저장소 옵션에 대한 개요입니다.

코르도바 응용 프로그램을 위하여 여러가지 저장소 API를 사용할 수 있습니다. 더 완전하고 다양한 예제는 [Html5rocks][1]를 참조하십시오.

 [1]: http://www.html5rocks.com/en/features/storage

## LocalStorage

*웹 스토리지*, *간단한 스토리지*, 또는 *세션 저장소* 인터페이스 등으로 알려진, 이 API는 동기된 키/값 쌍 스토리지를 제공합니다. 기본 WebView 구현에서 사용할 수 있습니다. 자세한 내용은 [W3C 사양][2]을 참조하십시오.

 [2]: http://www.w3.org/TR/webstorage/

## WebSQL

이 API는 기본 WebView에서 사용할 수 있습니다. [웹 SQL 데이터베이스 사양][3]은 SQL 쿼리를 통해 액세스되는 보다 완전한 기능의 데이터베이스 테이블을 제공합니다.

 [3]: http://dev.w3.org/html5/webdatabase/

다음 플랫폼에서 WebSQL을 지원합니다.

*   안드로이드
*   블랙베리 10
*   iOS
*   타이젠

## IndexedDB

이 API는 WebView에서 사용할 수 있습니다. [Indexed DB][4]는 LocalStorage 보다 더 많은 기능이 있지만 WebSQL 보다 적게 제공합니다.

 [4]: http://www.w3.org/TR/IndexedDB/

다음 플랫폼에서 IndexedDB를 지원합니다.

*   블랙베리 10
*   Firefox 운영 체제
*   윈도우폰 8
*   윈도우 8

## 플러그인 기반 옵션

위에 나열된 API 저장소 뿐만 아니라 [파일 API][5]는 로컬 파일 시스템에서 캐시 데이터를 사용할 수 있도록 합니다. 다른 [코르도바 플러그인][6]은 유사한 스토리지 옵션을 제공합니다.

 [5]: https://github.com/apache/cordova-plugin-file/blob/master/doc/index.md
 [6]: http://plugins.cordova.io/