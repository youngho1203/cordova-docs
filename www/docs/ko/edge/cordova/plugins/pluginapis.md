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

# 플러그인 API

코르도바는 최소한의 API 세트와 함께 제공되고 있기 떄문에 각 프로젝트들은 플러그인을 통하여 필요한 API를 추가하여야 합니다.

여러분은 [npm][1]으로 (제3자 플러그인을 포함하여)모든 기존 플러그인을 검색할 수 있습니다.

 [1]: https://www.npmjs.com/search?q=ecosystem%3Acordova

전통적인 코어 코르도바 플러그인들은 다음과 같습니다.

*   [배터리 상태][2]
    
    > 단말기의 배터리의 상태를 모니터링 합니다.

*   [카메라][3]
    
    > 단말기의 카메라를 사용하여 사진을 찍습니다.

*   [콘솔][4]
    
    > Console.log()에 추가적인 기능을 더합니다.

*   [연락처][5]
    
    > 단말기의 연락처 데이터베이스와 함께 동작합니다.

*   [장치][6]
    
    > 단말기의 정보를 수집합니다.

*   [장치 동작 (가속도계)][7]
    
    > 장치의 동작 센서를 인지합니다.

*   [장치 방향 (나침반)][8]
    
    > 장치가 가리키는 방향을 인식합니다.

*   [대화 상자][9]
    
    > 시각적 장치 알림입니다.

*   [파일 시스템][10]
    
    > 자바스크립트를 통해 네이티브 파일 시스템에 연결합니다.

*   [파일 전송][11]
    
    > 자바스크립트를 통해 네이티브 파일 시스템에 연결합니다.

*   [위치 정보][12]
    
    > 응용 프로그램이 위치를 인식하게 합니다.

*   [세계화][13]
    
    > 각 개체에 특정 로케일의 표현을 가능하게 합니다.

*   [InAppBrowser][14]
    
    > 또다른 브라우저 인스턴스에 URL을 기동합니다.

*   [미디어][15]
    
    > 오디오 파일을 녹음하고, 재생합니다.

*   [미디어 캡처][16]
    
    > 장치의 미디어 캡처 응용 프로그램을 사용하여 미디어 파일을 캡쳐합니다.

*   [네트워크 정보 (연결)][17]
    
    > 신속하게 네트워크 상태 및 셀룰러 네트워크 정보를 확인합니다.

*   [시작화면][18]
    
    > 응용 프로그램의 시작화면을 보이거나 숨깁니다.

*   [진동][19]
    
    > 장치를 진동하기 위한 API.

*   [상태 표시줄][20]
    
    > 상태 표시줄을 설정, 표시 또는 숨기기를 하기 위한 API.

*   [허용된 사이트 목록][21]
    
    > 네트워크 요청시 화이트 리스트를 설정합니다. 응용 프로그램에서 어떠한 네트워크 요청을 허용해야 할 지 설치를 해야 합니다.

*   [기존 화이트 리스트][22]
    
    > 화이트 리스트 플러그인으로 분리되기 전의 옛날 화이트 리스트 스타일을 사용하는 플러그인.

 [2]: https://www.npmjs.com/package/cordova-plugin-battery-status
 [3]: https://www.npmjs.com/package/cordova-plugin-camera
 [4]: https://www.npmjs.com/package/cordova-plugin-console
 [5]: https://www.npmjs.com/package/cordova-plugin-contacts
 [6]: https://www.npmjs.com/package/cordova-plugin-device
 [7]: https://www.npmjs.com/package/cordova-plugin-device-motion
 [8]: https://www.npmjs.com/package/cordova-plugin-device-orientation
 [9]: https://www.npmjs.com/package/cordova-plugin-dialogs
 [10]: https://www.npmjs.com/package/cordova-plugin-file
 [11]: https://www.npmjs.com/package/cordova-plugin-file-transfer
 [12]: https://www.npmjs.com/package/cordova-plugin-geolocation
 [13]: https://www.npmjs.com/package/cordova-plugin-globalization
 [14]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
 [15]: https://www.npmjs.com/package/cordova-plugin-media
 [16]: https://www.npmjs.com/package/cordova-plugin-media-capture
 [17]: https://www.npmjs.com/package/cordova-plugin-network-information
 [18]: https://www.npmjs.com/package/cordova-plugin-splashscreen
 [19]: https://www.npmjs.com/package/cordova-plugin-vibration
 [20]: https://www.npmjs.com/package/cordova-plugin-statusbar
 [21]: https://www.npmjs.com/package/cordova-plugin-whitelist
 [22]: https://www.npmjs.com/package/cordova-plugin-legacy-whitelist

이러한 플러그인 문서들의 영어 이외의 언어 번역본들은 github repos 의 plugin 에 있는 docs 폴더에서 찾을 수 있습니다.