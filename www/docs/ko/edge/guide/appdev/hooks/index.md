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

# 후크 가이드

코르도바 후크는 응용 프로그램, 플러그인 개발자, 심지어 여러분의 빌드 시스템이 커스터마이즈된 코르도바 명령어를 추가 할 수 있는 특별한 스크립트를 말합니다. 후크 스크립트는 미리 정의된 폴더 ( `/hooks` ) 에 추가하거나 또는 구성 파일을 통해 ( `config.xml` 및 `plugin.xml` ) 정의할 수 있으며, 아래의 순서에 따라 순차적으로 실행됩니다.:

  * `/hooks` 에 정의된 응용프로그램 후크;
  * `config.xml` 에 정의된 응용프로그램 후크;
  * `plugins/.../plugin.xml` 에 정의된 플러그인 후크;

**참고**: `/hooks` 디렉터리는 config.xml 와 plugin.xml 에 있는 후크 요소를 우선 사용하고, 더이상 사용되지 않는 것으로 간주됩니다.

## 지원되는 후크 유형

아래의 후크 유형들이 지원되고 있습니다.

    after_build
    after_compile
    after_clean
    after_docs
    after_emulate
    after_platform_add
    after_platform_rm
    after_platform_ls
    after_plugin_add
    after_plugin_ls
    after_plugin_rm
    after_plugin_search
    after_plugin_install // Plugin hooks in plugin.xml are executed for a plugin being installed only
    after_prepare
    after_run
    after_serve
    before_build
    before_clean
    before_compile
    before_docs
    before_emulate
    before_platform_add
    before_platform_rm/
    before_platform_ls
    before_plugin_add
    before_plugin_ls
    before_plugin_rm
    before_plugin_search/
    before_plugin_install // Plugin hooks in plugin.xml are executed for a plugin being installed only
    before_plugin_uninstall // Plugin hooks in plugin.xml are executed for a plugin being uninstalled only
    before_prepare
    before_run
    before_serve
    pre_package // 윈도우 and 윈도우폰 only
    

## 후크를 정의하는 방법

### `/Hooks` 디렉토리를 사용하여 정의하기

**참고**:이 방법은 config.xml 와 plugin.xml 후크 요소를 사용함에 따라서, 더 이상 사용되지 않는 것으로 간주합니다.

해당 후크 형식이 발생 때 사용자 지정 작업을 실행하기 위하여, '후크' 디렉토리 안의 하위 폴더에 후크 타입을 이름으로한 당신의 스크립트 파일을 배치하시기 바랍니다. 예를 들어 스크립트:

    # script file will be automatically executed after each build
    hooks/after_build/after_build_custom_action.js
    

이러한 후크를 사용할 때, 그것들은 로드 가능한 자바스크립트 모듈 아니라 항상 실행 파일로 실행 됩니다. **기억하세요**: 이경우에 항상 당신의 스크립트가 실행 가능해야 한다는 것을 확인하세요.

### Config.xml

후크는 프로젝트의 `config.xml`  에 있는 `<hook>` 요소를 사용하여 정의할 수 있습니다. 예를 들어:

    <hook type="before_build" src="scripts/appBeforeBuild.bat" />
    <hook type="before_build" src="scripts/appBeforeBuild.js" />
    <hook type="before_plugin_install" src="scripts/appBeforePluginInstall.js" />
    
    <platform name="wp8">
        <hook type="before_build" src="scripts/wp8/appWP8BeforeBuild.bat" />
        <hook type="before_build" src="scripts/wp8/appWP8BeforeBuild.js" />
        <hook type="before_plugin_install" src="scripts/wp8/appWP8BeforePluginInstall.js" />
        ...
    </platform>
    
    <platform name="windows8">
        <hook type="before_build" src="scripts/windows8/appWin8BeforeBuild.bat" />
        <hook type="before_build" src="scripts/windows8/appWin8BeforeBuild.js" />
        <hook type="before_plugin_install" src="scripts/windows8/appWin8BeforePluginInstall.js" />
        ...
    </platform>
    

### 플러그인 후크들 (plugin.xml)

만약 당신이 플러그인 개발자라면, 후크는 `plugin.xml` 에 있는  `<hook>` 요소를 사용하여 아래처럼 후크 스크립트를 정의할 수 있습니다.:

    <hook type="before_plugin_install" src="scripts/beforeInstall.js" />
    <hook type="after_build" src="scripts/afterBuild.js" />
    
    <platform name="wp8">
        <hook type="before_plugin_install" src="scripts/wp8BeforeInstall.js" />
        <hook type="before_build" src="scripts/wp8BeforeBuild.js" />
        ...
    </platform>
    

`before_plugin_install`, `after_plugin_install`, `before_plugin_uninstall` 플러그인 후크는 설치되거나/제거되는 상태에 있는 플러그인에서만 신호가 발생될 것 입니다.

## 스크립트 인터페이스

### Javascript

만약 당신이 Node.js 를 사용하여 후크를 작성하는 경우에는 다음과 같이 모듈을 정의하여 사용해야 합니다.

```javascript
module.exports = function(context) {
    ...
}
```

Q 를 사용하여 scipts 를 비동기적으로 만들 수 있습니다.

```javascript
module.exports = function(context) {
    var Q = context.requireCordovaModule('q');
    var deferral = new Q.defer();

    setTimeout(function(){
      console.log('hook.js>> end');
    deferral.resolve();
    }, 1000);

    return deferral.promise;
}
```

`context` 개체에는 후크 형식, 실행되는 스크립트의 전체 경로, 후크 옵션들, 코르도바에 전달되는 명령줄 인수들, 그리고 최상위 "cordova" 개체가 포함되어 있습니다.:

```json
{
  "hook": "before_plugin_install",
  "scriptLocation": "c:\\script\\full\\path\\appBeforePluginInstall.js",
  "cmdLine": "The\\exact\\command\\cordova\\run\\with arguments",
  "opts": {
    "projectRoot":"C:\\path\\to\\the\\project",
    "cordova": {
      "platforms": ["wp8"],
      "plugins": ["com.plugin.withhooks"],
      "version": "0.21.7-dev"
    },
    "plugin": {
      "id": "com.plugin.withhooks",
      "pluginInfo": {
        ...
      },
      "platform": "wp8",
      "dir": "C:\\path\\to\\the\\project\\plugins\\com.plugin.withhooks"
    }
  },
  "cordova": {...}
}

```

`context.opts.plugin` 개체는 플러그인 후크 스크립트에게만 전달됩니다.

또한 아래와 같은 방식으로 `context.requireCordovaModule` 을 사용하여 당신의 스크립트에 코르도바 모듈들을 추가할 수 있습니다.

```javascript
var Q = context.requireCordovaModule('q');
```

**참고**: 새로운 모듈 로더 스크립트 인터페이스는 `config.xml` 또는 `plugin.xml` 에서 정의된 `.js` 파일에 대해서만 사용이 됩니다. 호환성 때문에 `/hooks` 폴더를 통해 지정된 후크 파일들은 노드 child_process spawn 을 통하여 실행이 됩니다. '비-자바스크립트' 섹션을 참조바랍니다.

### 비-자바스크립트

**참고**: 크로스-플랫폼을 유지하기 위하여, 가능한 Node.js 를 사용하여 후크를 작성하는 것이 좋습니다. 위의 '자바스크립트' 섹션을 참조 하십시오.

비-자바스크립트 스크립트들은 프로젝트의 루트 디렉터리에서 노드 child_process spawn 을 통해 실행이 되고 첫 번째 인수로 루트 디렉토리의 경로를 가집니다. 스크립트에 전달되는 다른 모든 옵션은 환경 변수를 사용하여 전달됩니다.

  * CORDOVA_VERSION-코르도바-CLI의 버전
  * CORDOVA_PLATFORMS-쉼표로 구분된 적용되는 플랫폼 (예: android, ios) 목록.
  * CORDOVA_PLUGINS-쉼표로 구분되는 플러그인 ID 들의 목록(예: org.apache.cordova.file, org.apache.cordova.file-transfer)
  * CORDOVA_HOOK-실행되는 후크를 위한 경로
  * CORDOVA_CMDLINE-코르도바에 전달된 정확한 명령줄 인수 (예: cordova run ios --emulate)

만약 스크립트가 0 이 아닌 종료 코드를 반환 하는 경우에는 부모 코르도바 명령도 실행이 중단됩니다.

또한, Windows 에서 작업하고 있는 경우, 당신의 후크 스트립트가 배치 파일이 아닌 경우 (권장사항이지만, 당신의 스크립트가 비 Windows 운영 체제에서 작동하도록 한다면), 코르도바 CLI 는 첫 번째 줄에 이것이 인터프리터이고 스크립트를 기동하기 위하여 사용되는 shebang 라인이 있을 거라 가정합니다. Shebang 라인은 다음 예제에서 보이는 것과 일치해야 합니다.:

    #!/usr/bin/env [name_of_interpreter_executable]
    

## 샘플 사용법

이 샘플에는 안드로이드 플랫폼에서 생성된 .apk 파일의 크기를 콘솔 출력하기 위한 코르도바 후크 사용법을 보여 줍니다.

비어있는 코르도바 애플리케이션을 만들고, 각 플랫폼에서 빌드 후  `afterBuild.js` 스크립트를 실행하기 위하여 `config.xml` 에 다음 정의를 추가합니다.

    <hook type="after_build" src="scripts/afterBuild.js" />
    

`scripts/afterBuild.js` 파일을 만들고 다음과 같은 구현을 추가합니다. 우리는 후크를 통하여 비동기 기능을 할 수 있는 방법을 보여 주기 위하여  `fs.stat` 메서드의 비동기 버전을 가지고 있습니다.

    module.exports = function(ctx) {
        // make sure android platform is part of build 
        if (ctx.opts.platforms.indexOf('android') < 0) {
            return;
        }
        var fs = ctx.requireCordovaModule('fs'),
            path = ctx.requireCordovaModule('path'),
            deferral = ctx.requireCordovaModule('q').defer();
    
        var platformRoot = path.join(ctx.opts.projectRoot, 'platforms/android');
        var apkFileLocation = path.join(platformRoot, 'build/outputs/apk/android-debug.apk');
    
        fs.stat(apkFileLocation, function(err,stats) {
            if (err) {
                 deferral.reject('Operation failed');
            } else {
                console.log('Size of ' + apkFileLocation + ' is ' + stats.size +' bytes');
                deferral.resolve();
            }
        });
    
        return deferral.promise;
    };
    

위의 예에서 매개 변수 `ctx` 는 코르도바에 의해 전달되고 스크립트의 전체 경로, 대상 플랫폼, 명령줄 인수, 기타의 것들을 가진 실행 컨텍스트를 의미합니다. 또한 추가적으로 도움 기능에서도 이 실행 컨텍스트가 나타냅니다. 보다 자세한 내용은 위의 `스크립트 인터페이스`  단원을 참조 하십시오.

이제 안드로이드 플랫폼을 추가하고 빌드를 실행할 수 있습니다.

    cordova platform add android
    ..
    cordova build
    ..
    Size of path\to\app\platforms\android\build\outputs\apk\android-debug.apk is 1821193 bytes
    

더 좋은 사용 예는 여기에서 찾을 수 있습니다.

<http://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/>