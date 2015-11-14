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

# Plugman을 사용한 플러그인 관리

버전 3.0부터, 코르도바는 모든 장치 API들을 플러그인으로 구현하고 기본 설정값으로 비활성화 시켜 놓았습니다. 그리고 코르도바 소개에서 설명한 것과 같이 어떤 워크플로우를 선택하는냐에 따라서 플러그인을 추가하고 제거하는 두 가지 방법을 제공합니다.

*   만약 당신이 크로스-플랫폼 워크플로우를 사용하는 경우는 명령줄 인터페이스에 설명한 것과 같이 `cordova` CLI 유틸리티를 사용하여 플러그인을 추가합니다. CLI는 모든 지정된 플랫폼에 대한 플러그인을 한 번에 수정합니다.

*   만약 당신이 플랫폼-중심 워크플로우를 사용하는 경우에는, 각 대상 플랫폼에서 따로 따로 하위 수준의 [Plugman][1] 명령줄 인터페이스를 사용합니다.

 [1]: https://github.com/apache/cordova-plugman/

이 단원에는 Plugman 유틸리티를 자세히 설명합니다. 노드 모듈에서 Plugman을 샤용하거나 소스 코드를 수정해야 한다면, [파일 저장소에 있는 README 파일][2]을 참조하십시오.

 [2]: https://github.com/apache/cordova-plugman/blob/master/README.md

## Plugman 설치하기

Plugman를 설치하려면 [node][3]가 컴퓨터에 설치되어 있어야 합니다. 그 다음에 plugman을 전역으로 설치하기 위하여, 어느 위치에서든 아래의 명령어를 실행합니다. 그러면 어느 디렉터리에서든 노드를 사용할 수 있습니다.:

 [3]: http://nodejs.org/

    $ npm install -g plugman
    

또한 원격 git URL들에서 직접 플러그인을 설치할 수 있기 때문에 `git`가 당신의 `PATH` 에 설정되어 있어야만 합니다. 

**팁**: `npm`으로 plugman를 설치한 후에 `plugman` 명령어를 동작시킬 수 없으면, 당신의 `PATH` 에  `/npm/` 디렉터리가 들어가 있는지 확인햐여 주시기 바랍니다.

**참고**: Plugman를 전역으로 설치하여 전역 `npm` 명령어를 사용할 필요가 없으면 단계를 건너뛸 수 있습니다. 만약이 그렇치 않은 경우에는, 셸 도구를 사용하여 코르도바 프로젝트를 만들 때, Plugman를 포함하고 있는 `node_modules` 이  프로젝트의 내부 디렉터리에 존재할 것 입니다. 왜냐하면 전역으로 설치하지 않았기 때문에, 예를 들어 'node ./node_modules/plugman/main.js -version` 처럼 각 Plugman 명령를 실해하기 위하여 `node` 를 호출해야 했기 때문입니다.
이 가이드의 나머지 부분은 Plugman이 전역으로 설치되었음을 가정합니다, 즉 `plugman` 만 입력하면 그것을 그냥 호출할 수 있어야 합니다.

## 코르도바 프로젝트 만들기

Plugman를 사용하기 전에 먼저 코르도바 프로젝트를 만들어야 합니다. 명령줄 인터페이스를 사용하거나 또는 낮은 수준의 셸 스크립트를 사용하여 만들 수 있습니다. 셸 스크립트를 사용하여 프로젝트를 만드는 데 필요한 지침은 플랫폼 가이드들에 나열된 여러 "명령줄 도구" 가이드중에 있습니다.

## 플러그인 추가하기

Plugman 설치하고 코르도바 프로젝트가 만들어 있는 경우에는 플랫폼에 플러그인을 추가할 수 있습니다.

    $ plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin <name|url|path> [--plugins_dir <directory>] [--www <directory>] [--variable <name>=<value> [--variable <name>=<value> ...]]
    

이 명령은 최소의 매개 변수를 사용하여 코르도바 프로젝트에 플러그인을 설치합니다. 당신은 플랫폼을 지정해야 하고, 해당 플랫폼에 대한 코르도바 프로젝트 위치를 지정해야 합니다. 또한 `--plugin` 매개 변수를 사용하여 플러그인을 지정해야 합니다.:

*   `name`: 플러그인의 내용이 존재하는 디렉터리의 이름입니다. 이 이름은 `--plugins_dir` 경로(아래 추가 정보 참조)에 있는, 존재하고 있는 디렉터리이름 이거나 또는 코르도바 레지스트리에 있는 플러그인이어야 합니다.
*   `url`: https:// 또는 git로 시작하는 URL 로서 `plugin.xml` 파일을 포함하고 있으며, 복제 가능하고 유효한 git 저장소를 가리킵니다. 이 저장소의 내용들은 `--plugins_dir` 아래에 복사됩니다.
*   `path`: `plugin.xml` 파일을 포함하며, 유효한 플러그인을 가지고 있는 디렉터리의 경로입니다. 이 경로의 내용은 `--plugins_dir`로 복사됩니다.

다른 매개 변수들:

*   `--plugins_dir` 의 기본값은 `<project>/cordova/plugins` 입니다. 하지만 내려 받은 각각의 플러그인을 하위 디렉터리로 포함한 어떠한 디렉터리도 가능합니다.
*   `--www`는 기본값으로 프로젝트의 `www` 폴더 위치를 가르킵니다. 하지만 어떠한 디렉터리도 코르도바 프로젝트 응용 프로그램의 웹 자산(Web Assets)으로 사용될 수 있습니다.
*   `--variable`은 설치시에 API 키가 필요하거나 또는 사용자 정의 매개 변수를 필요로 하는 플러그인등을 위하여 어떠한 변수들도 정의할 수 있습니다. 자세한 내용은 [플러그인 명세][4] 를 참조하십시오.

 [4]: plugin_ref_spec.md.html#Plugin%20Specification

## 플러그인 제거하기

플러그인을 제거하려면 간단히 `--uninstall` 플래그와 플러그인 ID 매개 변수로 설정합니다.

    $ plugman --uninstall --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin <id> [--www <directory>] [--plugins_dir <directory>]
    

## 도움말 명령

Plugman은 문제가 발생하는 경우 도움이 될 수 있는 전역 도움말 기능을 같고 있습니다. 아래의 명령어는 사용 가능한 모든 Plugman 명령 및 구문 목록을 표시합니다.

    plugman -help
    plugman  # same as above
    

**참고**: `plugman -help`는 몇 가지 레지스트리 관련 명령어들이 추가로 표시될 수 있습니다. 이 명령어들은 플러그인 개발자를 위한 것 이며 플러그인 레지스트리에 있는 제3자 플러그인에는 구현되어 있지 않을 수 있습니다.

또한 당신은 어떠한 Plugman 명령어에도 `--debug|-d` 플래그를 추가하여 상세 모드로 실행을 할 수 있습니다. 상세 모드로 실행이 되면, 파일이 존재하지 않는 경우와 같은 문제를 추적하는데 도음이 되는 모든 내부 디버깅 메시지가 표시되게 됩니다.

    # Adding Android battery-status plugin to "myProject":
    plugman -d --platform android --project myProject --plugin cordova-plugin-battery-status
    

마지막으로, `--version|-v` 플래그를 사용할 수 있는데, 이것은 지금 사용하고 있는 Plugman의 버전을 표시합니다.

    plugman -v
    

## 레지스트리와의 연동 작업

[플러그인 레지스트리][5]와 상호 작용을 위해 사용될 수 있는 여러개의 plugman 명령어가 있습니다. 이러한 레지스트리 명령어들은  *plugins.cordova.io* 플러그인 레지스트리에 특정되어 있으며, 제3자 플러그인 레지스트리에서는 구현되어 있지 않을 수 있습니다.

 [5]: http://plugins.cordova.io

### 플러그인 검색

Plugman를 사용하여 공백문자로 구분된 키워드 목록과 일치하는 id의 플러그인을 [플러그인 레지스트리][5]에서 검색할 수 있습니다.

    plugman search <plugin keywords>
    

### 플러그인 레지스트리 변경

당신은 plugman이 사용하고 있는 현재 플러그인 레지스트리의 URL 을 설정하거나 확인할 수 있습니다. 보통 제3자 플러그인 레지스트리를 사용하려는 경우가 아니면 http://registry.cordova.io 으로 설정합니다.

    plugman config set registry <url-to-registry>
    plugman config get registry
    

### 플러그인 정보 얻기

당신은 아래의 명령어로 플러그인 저장소에 저장되어 있는 특정 플러그인에 대한 정보를 얻을 수 있습니다.

    plugman info <id>
    

이 명령어는 플러그인의 버전 번호와 같은 정보를 얻기 위하여 플러그인 레지스트리를 접속하여 정보를 가지고 옵니다.

## 코어 플러그인들을 설치하기

아래 예제에서는 코르도바 API 프로젝트에서 버전 3.0으로 업그레이드 한 후 필요에 따라 플러그인을 추가하는 방법을 보여줍니다. 각 명령마다 대상 플랫폼을 선택하고 플랫폼의 프로젝트 디렉터리를 지정해야 합니다.

*   cordova-plugin-battery-status
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-battery-status`

*   cordova-plugin-camera
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-camera`

*   cordova-plugin-console
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-console`

*   cordova-plugin-contacts
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-contacts`

*   cordova-plugin-device
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-device`

*   cordova-plugin-device-motion (accelerometer)
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-device-motion`

*   cordova-plugin-device-orientation (compass)
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-device-orientation`

*   cordova-plugin-dialogs
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-dialogs`

*   cordova-plugin-file
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-file`

*   cordova-plugin-file-transfer
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-file-transfer`

*   cordova-plugin-geolocation
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-geolocation`

*   cordova-plugin-globalization
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-globalization`

*   cordova-plugin-inappbrowser
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-inappbrowser`

*   cordova-plugin-media
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-media`

*   cordova-plugin-media-capture
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-media-capture`

*   cordova-plugin-network-information
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-network-information`

*   cordova-plugin-splashscreen
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-splashscreen`

*   cordova-plugin-vibration
    
    `plugman --platform <ios|amazon-fireos|android|blackberry10|wp8> --project <directory> --plugin cordova-plugin-vibration`