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

# 개인 정보 보호 가이드

모바일 개인 정보는 모든 앱개발자들이 반듯이 해결해야 할 매우 중요한 문제입니다. 당신의 앱 사용자는 당신의 앱에서 그들의 개인 정보가 적절하게 취급되고 수집될 것이라 기대할 것입니다. 또한, 요즈음은 모바일 개인정보 취급에 대한 법적 요구 사항이 보다 더 강화되고 있는 추세입니다.

모바일 앱 개인 정보 보호에 관한 이 가이드는 매우 중요한 문제로서 가장 먼저 고려되어야 할 *최우선* 사항으로 취급되어야 합니다. 여기에서는 광범위하게 허용된 몇 가지 모범 사례를 간략하게 설명하고 다른 더 상세한 가이드 및 참조사항을 제시합니다.

*   **개인 정보 보호 정책**: 당신의 앱에서는 사용자에 대한 정보, 사용자들의 정보 이용 방법, 누구와 함께 사용하였는지 등등의 개인정보를 수집하고 있는지, 그리고 앱에서 개인의 취향에 관한 설정을 선택할 수 있는지 등에 관한 개인 정보 보호 정책이 설명되어 있는 것을 포함하고 있어야 합니다. 이해를 돕기 위해 일반 언어를 사용하여야 하고 기술적인 용어를 피하여야만 합니다. 당신은 개인 정보 보호 정책을 사용자가 앱 시장의 앱 설명서등에서 다운로드할 수 있도록 하여, 앱을 설치하기 전에 사전 검토를 할 수 있도록 해야 합니다. 또한 당신의 개인 정보 보호 정책을 앱내부에서 확인할 수 있도록 해야 합니다. 그러나 이동기기의 화면 크기 때문에 사용자에게 개인 정보 보호 정책을 표시하는 것은 쉽지만은 않습니다. 때문에 가장 중요한 정보만을 포함하고 있는 *약식* 설명서를 고려하고, 그 주제의 더 많은 세부 사항에 대하여는 "상세 형식" 정책에 대한 링크를 제공하는 것도 고려할 수 있습니다. 여러 그룹들은 개인 정보를 취급하는 방식을, 사용자들이 표준화된 아이콘에 친숙해 지기를 희망하면서, 표준화된 아이콘 기반으로 표현하려는 노력을 기하고 있기도 합니다.

*   **민감한 정보 수집**: 앱에서 민감한 개인정보의 수집은 중요한 개인 정보 보호 문제를 발생시킵니다. 민감한 개인 정보의 예로는 금융 정보, 건강 정보 및 또는 가족들에 대한 정보등이 있습니다. 또한 모바일 장치 또는 태블릿에 일반적으로 설치되어 있는 특정 센서와 데이터베이스에서 얻어지는 정보들, 예를 들어, 위치 정보, 연락처/전화 번호부, 마이크로폰/카메라, 저장된 사진/동영상등이 있습니다. 더 자세한 내용은 다음 설명서 페이지를 참조하십시오: [카메라][1], [캡처][2], [연락처][3]및 [위치 정보][4]. 일반적으로, 민감한 정보를 수집하기 전에 사용자의 명시적 허가를 받아야 하고, 가능하다면, 사용자가 권한을 쉽게 변경할 수 있는 제어 메커니즘을 제공해야 합니다. 앱 운영 체제에 따라서는 수집되기 전에 사용자의 허가를 요청하기 위한 저스트-인-타임 대화 상자를 제시하도록 할 수 도 있습니다. 이러한 경우에 수집된 정보를 앱에서 어떻게 사용하고, 또 해당되는 경우 그 정보의 공유 여부에 대한 내용을 대화 상자 안내글에 명확하게 설명해야 합니다.

*   **사용자의 혼선을 피하기**: 만약 당신의 앱이 앱의 기본 목적에 비추어 수집하는 경우에도 (예를 들어, 음악 플레이어가 저장된 사진에 액세스하는 경우등) 사용자에게 혼선을 줄 수 있으며, 민감한 개인 정보의 수집시에도 비슷한 상황이 발생할 수 있습니다. 이러한 점은, 정보를 수집하는 단계에서 저스트-인-타임 대화 상자를 사용하여 사용자에게 지금 정보를 수집할 것을 알리고, 사용자가 그 정보의 사용과 또 가능하다면 해당되는 개인 정보의 제공 여부를 제어할 수 있도록 고려해야 합니다.

*   **제3자 데이터 수집 또는 공유**: 당신이 앱이 정보를 수집해서 다른 회사-소셜 네트워킹 플랫폼 이나 광고 네트워크(예를 들어 당신의 앱이 광고를 표시하는 경우) 에 제공하는 경우, 당신은 사용자에게 수집되는 정보와 그 공유를 알려야 합니다. 최소한, 당신의 개인 정보 보호 정책에서는 정보의 수집과 공유를 설명해야 하고, 사용자가 적절하게 그 기능을 제어할 수 있거나 또는 수집과 공유를 중지할 수 있는 기능을 제공하여야 합니다.

*   **수집의 제한과 보안**: 사용자는 그들의 정보를 당신의 앱에 위임하고, 당신이 그것을 보호하기 위해 적절한 보안 조치를 취할 것을 기대하고 있습니다. 개인 정보의 보안 문제를 피하기 위해 최선의 방법은, 당신의 앱이 수집에 대하여 구체적이고 합법적인 이유가 있지 않는 한, 무턱데고 개인정보를 수집하지 않는 것 입니다. 수집될 필요가 있는 정보에 대하여, 그 정보가 저장되어 있는 장소가 사용기기이든 아니면 백 엔드 서버에이든 상관없이, 그 정보를 보호하기 위해 적절한 보안장치를 운영하고 있는 것을 명확히 하여야 합니다. 또한 앱과 백 엔드 서버에서 구현되는 적절한 데이터 보존 정책을 개발해야 합니다.

 [1]: cordova_camera_camera.md.html
 [2]: cordova_media_capture_capture.md.html
 [3]: cordova_contacts_contacts.md.html
 [4]: cordova_geolocation_geolocation.md.html

다음은 개발자들을 위하여 추가적인 도움이 될 몇 가지 모바일 개인정보 보호 가이드입니다.

*   캘리포니아 법무 장관, [이동체에서 개인 정보: 모바일 생태계에 대한 권장 사항][5]

*   민주주의와 기술의 중심, 개인 정보의 미래 포럼, [모바일 앱 개발자를 위한 최상의 방법][6]

*   CTIA-무선 협회, [위치 기반 서비스에서 모범 사례와 지침][7]

*   연방 무역 위원회, [모바일 개인 정보 공개: 투명성을 통해 신뢰 구축][8]

*   개인 정보의 미래 포럼 [응용 프로그램 개인 정보 보호][9] 웹 사이트

 [5]: http://oag.ca.gov/sites/all/files/pdfs/privacy/privacy_on_the_go.pdf
 [6]: http://www.futureofprivacy.org/wp-content/uploads/Best-Practices-for-Mobile-App-Developers_Final.pdf
 [7]: http://www.ctia.org/business_resources/wic/index.cfm/AID/11300
 [8]: http://www.ftc.gov/os/2013/02/130201mobileprivacyreport.pdf
 [9]: http://www.applicationprivacy.org