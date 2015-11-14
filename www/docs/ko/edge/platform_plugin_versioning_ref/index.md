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

# 플랫폼 및 플러그인 버전 관리

버전 4.3.0 이상 부터, 코르도바는 플랫폼과 플러그인을 저장하고 복원하는 기능을 제공합니다.

이 기능은 개발자가 모든 플랫폼과 플러그인 소스 코드를 체크인하지 않고 그들의 앱을 주어진 상태로 저장하고 복원할 수 있습니다.

'save' 명령어는 config.xml에 앱의 플랫폼 및 플러그인 버전에 대한 세부 정보를 저장합니다. 'restore' 단계는 **'cordova prepare'** 가 요청되면 자동으로 발생되는데, 이떄 config.xml 파일에 저장되었던 이전 정보를 사용할 수 있도록 합니다.

저장/복원 기능이 편리함을 주는 하나의 시나리오는 앱을 개발하는데 대규모 팀이 협업하는 경우인데 각 팀 멤버는 각각의 플랫폼 또는 플러그인 개발에만 초점을 맞출 수 있도록 합니다. 이 기능은 쉽게 프로젝트를 공유하고 코드 저장소에 중복된 코드의 등록을 많이 줄일 수 있도록 합니다.

## 플랫폼 버전 관리

### 플랫폼을 저장하기

플랫폼을 저장하려면 다음 명령을 실행하십시요.:

    $ cordova platform add <platform[@<version>] | directory | git_url> --save
    

위의 명령을 실행하면 config.xml는 다음과 같이 저장됩니다.

    <?xml version='1.0' encoding='utf-8'?>
        ...
        <engine name="android" spec="~4.0.0" />
        ...
    </xml>
    

몇 가지 예제:

  * **'cordova platform add android --save'** => 안드로이드 플랫폼의 고정된 버전을 검색하여, 프로젝트에 추가하고 config.xml을 업데이트 합니다.
  * **'cordova platform add android@3.7.0 --save'** => npm 에서 안드로이드 플랫폼 3.7.0 버전을 가지고 와서, 프로젝트에 추가한 다음 config.xml을 업데이트 합니다.
  * **'cordova platform add android@https://github.com/apache/cordova-android.git​ --save'** 지정된 코르도바-안드로이드 git 저장소를 복제하여, 프로젝트의 안드로이드 플랫폼을 추가한 다음에 config.xml을 업데이트하고 지정된 git-url로 이것의 버전으로 등록합니다.
  * **'cordova platform add C:/path/to/android/platform --save'** => 지정된 디렉터리에서 안드로이드 플랫폼을 가지고 와서 프로젝트에 추가한 다음에 config.xml을 업데이트하고 디렉터리를 등록합니다.

### 기존 프로젝트에 대용량의 플랫폼을 저장하기

위에서 설명한 '-save' 플래그는 플랫폼을 추가할 때 사용해야만 유용합니다. 만약 기존에 프로젝트가 있고 현재 프로젝트에 추가되어 있는 모든 플랫폼을 저장하려는 경우 다음과 같이 사용할 수 있습니다.

    $ cordova platform save
    

### 플랫폼을 업데이트/제거하기

또한 'cordova platform update'과 'cordova platform remove' 명령을 수행하면서 config.xml 정보를 업데이트/삭제 할 수 있습니다:

    $ cordova platform update <platform[@<version>] | directory | git_url> --save
    $ cordova platform remove <platform> --save
    
몇 가지 예제:

  * **'cordova platform update android --save'** => 고정된 버전으로 안드로이드 플랫폼을 업데이트하고 config.xml 항목을 업데이트합니다.
  * **'cordova platform update android@3.8.0 --save'** => 안드로이드 플랫폼 버전 3.8.0로 업데이트하고 config.xml 항목을 업데이트합니다. 
  * **'cordova platform update /path/to/android/platform --save'** => 특정 폴더에 있는 버전으로 안드로이드 플랫폼을 업데이트하고 config.xml 항목을 업데이트합니다. 
  * **'cordova platform remove android --save'** => 프로젝트에서 안드로이드 플랫폼을 제거하고 config.xml에서 항목을 삭제 합니다.

### 플랫폼을 복원하기

플랫폼은 **'cordova prepare'** 명령을 실행하면 config.xml에서 자동으로 복원됩니다.

version/folder/git_url을 지정하지 않고 플랫폼을 추가하면, 설치되는 버전은 config.xml에서 값을 가지고 옵니다. **발견되는 경우에**.

예:

config.xml 파일에 다음 항목이 포함되어 있다고 가정할 때

    <?xml version='1.0' encoding='utf-8'?>
        ...
        <engine name="android" spec="3.7.0" />
        ...
    </xml>
    

**'cordova platform add android'** (no version/folder/git_url 지정) 명령을 실행하면, 플랫폼 'android@3.7.0' (config.xml에서 가지고 옴)로 설치됩니다.

* * *

## 플러그인 버전 관리

*(플러그인 명령어는 플러그인 명령의 거울)*

### 플러그인을 저장

플러그인을 저장하려면 다음 명령을 실행:

    $ cordova plugin add <plugin[@<version>] | directory | git_url> --save
    

위의 명령을 실행 후 결과 config.xml이 같습니다.

    <?xml version='1.0' encoding='utf-8'?>
        ...
        <plugin name="cordova-plugin-console" spec="~1.0.0" />
        ...
    </xml>
    

몇 가지 예제:

  * **'cordova plugin add cordova-plugin-console --save'** => 콘솔 플러그인의 고정된 버전을 검색, 프로젝트에 추가하고 config.xml을 업데이트 합니다.
  * **'cordova plugin add cordova-plugin-console@0.2.13 --save'** => 안드로이드 플러그인 버전 0.2.13 고궁 박물원, 프로젝트 및 다음 업데이트 config.xml 그것를 추가합니다.
  * **'cordova plugin add https://github.com/apache/cordova-plugin-console.git --save'** => 지정된 콘솔 플러그인 git 저장소를 복제, 콘솔 플러그인 프로젝트에 추가 다음 config.xml을 업데이트하고 지정된 된 git url 그것의 버전을 가리킵니다.
  * **'cordova plugin add C:/path/to/console/plugin --save'** => 지정된 된 디렉터리에서 콘솔 플러그인 프로젝트, 다음 업데이트 config.xml 및 디렉터리를 추가합니다.

### 기존 프로젝트에 플러그인을 저장하는 질량

'-save ' 위에서 설명한 플래그는 플러그인 추가하는 동안 그것을 사용해야 하는 경우에 유용. 기존 프로젝트를 있고 저장하려는 경우 모든 현재 프로젝트에 플러그인을 추가, 사용할 수 있습니다.

    $ cordova plugin save
    

### 업데이트/제거 플러그인

그것은 또한 명령 '코르도바 플러그인 업데이트'과 'cordova 플러그인 제거' 동안 config.xml에서 업데이트/삭제 수 있습니다:

    $ cordova plugin update <plugin[@<version>] | directory | git_url> --save
    $ cordova plugin remove <plugin> --save
    

몇 가지 예제:

  * **'cordova plugin update cordova-plugin-console --save'** => 고정된 버전, 업데이트 config.xml 항목을 콘솔 플러그인을 업데이트 뿐만 아니라
  * **'cordova plugin update cordova-plugin-console@0.2.13 --save'** => 안드로이드 플러그인 버전 업데이트 하 3.8.0, 업데이트 config.xml 항목 이외에 
  * **'cordova plugin update /path/to/console/plugin --save'** => 폴더, 업데이트 config.xml 항목에에서 버전 콘솔 플러그인을 업데이트 뿐만 아니라 
  * **'cordova plugin remove cordova-plugin-console --save'** => 를 프로젝트에서 콘솔 플러그인을 제거하고 config.xml에서 항목을 삭제 합니다.

### 플러그인을 복원하기

플러그인은 **'cordova prepare'** 명령을 실행하면 config.xml에서 자동으로 복원됩니다.

만약 당신이 version/folder/git_url 를 지정하지 않고 플러그인을 추가하면, 설치되는 버전은 config.xml에서 가져온 것 입니다 **발견되는 경우**.

예:

가정 config.xml 파일에 다음 항목이 포함되어 있습니다.

    <?xml version='1.0' encoding='utf-8'?>
        ...
        <plugin name="cordova-plugin-console" spec="0.2.11" />
        ...
    </ xml>
    

만약 당신이 **'cordova plugin add cordova-plugin-console'** (version/folder/git_url 지정하지 않고)를 실행하면, 플러그인은 'cordova-plugin-console@0.2.11' (config.xml에서 가지고 온 것)로 설치됩니다.