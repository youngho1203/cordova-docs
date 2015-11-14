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

# 타이젠 플랫폼 가이드

이 가이드에서는 타이젠 운영 체제를 실행하는 장치에 대한 코르도바 앱을 배포하기 위해 SDK 개발 환경을 설정하는 방법을 설명합니다.

## 요구 사항 및 지원

타이젠 SDK 리눅스 우분투 10.04/10.10/11.04/11.10 (32 비트), 또는 윈도우 XP s p 3/7 (32 비트) 필요합니다.

개발자가 사용해야 합니다 `cordova` 타이젠 SDK와 함께에서 유틸리티. 설치, 프로젝트 추가 다음 빌드하고 프로젝트를 배포하는 방법 정보에 대한 명령줄 인터페이스를 참조.

## SDK 설치

[Tizen.org][1] 에서 타이젠 SDK를 다운로드.

 [1]: https://developer.tizen.org/sdk

<!--

- (optional) Install 타이젠 Cordova template projects: copy the
  `/templates` directory content into the 타이젠 Eclipse IDE web
  templates directory (e.g.:
  `/home/my_username/tizen-sdk/IDE/Templates/web`).

- __Method #2: Use 타이젠 Eclipse IDE Cordova 타이젠 project templates__
    - Launch 타이젠 Eclipse IDE
    - Select  __File &rarr; New &rarr; 타이젠 Web Project__
    - Select __User Template__ and __User defined__ items
    - Select one of the 타이젠 Cordova template (e.g.: __CordovaBasicTemplate__)
    - Fill the __Project name__ and its target __Location__

    ![](img/guide/platforms/tizen/project_template.png)

    - Click __Finish__

    ![](img/guide/platforms/tizen/project_explorer.png)

    - Your project should now appear in the __Project Explorer__ view

-->

## SDK에서는 프로젝트를 열려면

1.  타이젠 이클립스 IDE를 시작 합니다.

2.  **파일 → 가져오기 → 타이젠 웹 프로젝트를**선택합니다.
    
    ![][2]

3.  **다음** 키를 누릅니다.

4.  **루트 디렉터리 선택** 확인란이 선택되어 있는지 확인합니다.

5.  **프로젝트 작업 영역으로 복사** 확인란이 선택되어 있는지 확인합니다.

6.  **찾아보기** 누른 후 선택 코르도바 타이젠 `samples` 프로젝트 디렉터리 (와 같은 `/cordova-basic` ):
    
    ![][3]

7.  **완료**를 누릅니다. 프로젝트를 가져올 수 지금과 **프로젝트 탐색기** 보기에서 표시 해야 합니다.
    
    ![][4]

 [2]: img/guide/platforms/tizen/import_project.png
 [3]: img/guide/platforms/tizen/import_widget.png
 [4]: img/guide/platforms/tizen/project_explorer.png

프로젝트를 다시 작성 하려면 **프로젝트 탐색기** 보기에서 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 빌드**를 선택합니다.

![][5]

 [5]: img/guide/platforms/tizen/build_project.png

프로젝트의 루트 디렉터리에 있는 *hello.wgt* 와 같은 위젯 패키지 파일 생성 해야 합니다.

## 에뮬레이터에 배포

**프로젝트 탐색기** 보기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **→ 타이젠 웹 시뮬레이터 응용 프로그램을 실행**을 선택합니다.

![][6]

 [6]: img/guide/platforms/tizen/runas_web_sim_app.png

## 장치에 배포

*   대상 장치 제대로 시작, 연결 및 구성 된는 다는 것을 확인 하십시오. 그것의 **날짜 및 시간** 설정은 올바르게 설정해야 합니다.

*   **연결 탐색기** 보기를 사용하여 응용 프로그램 배포 대상 선택: **창 → 쇼 보기 → 연결 탐색기**.
    
    ![][7]

*   **프로젝트 탐색기** 보기에서 프로젝트 마우스 오른쪽 단추로 클릭 하 고 **실행 → 타이젠 웹 응용 프로그램**선택:
    
    ![][8]

 [7]: img/guide/platforms/tizen/connection_explorer.png
 [8]: img/guide/platforms/tizen/runas_web_app.png