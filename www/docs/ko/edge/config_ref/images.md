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

# 아이콘 및 시작화면

이 단원에서는, 코르도바 CLI (명령줄 인터페이스에서 설명) 에서 작업할 때 또는 플랫폼에 특정된 SDK 도구 (플랫폼 가이드들에서 자세히 설명)를 사용할 때의 경우, 두가지 모두에 대하여 앱의 아이콘과 여러 플랫폼의 추가적인 시작화면을 구성하는 방법에 대하여 알아봅니다.

## CLI 를 이용하여 아이콘들을 구성하기

CLI 를 사용하여 작업을 할때 `<icon>` 요소 ( `config.xml` )를 통하여 앱 아이콘들을 지정할 수 있습니다. 만약 아이콘을 지정하지 않으면 기본으로 아파치 코르도바 로고가 사용됩니다.

        <icon src="res/ios/icon.png" platform="ios" width="57" height="57" density="mdpi" />
    

src:  (필수) 이미지 파일의 위치를 프로젝트 디렉터리의 상대위치로 지정합니다

platform: (선택사항) 대상 플랫폼

width: (선택사항) 픽셀단위의 아이콘 너비

height: (선택사항) 픽셀단위의 아이콘 높이

density: (선택사항) 안드로이드만, 아이콘 밀도를 지정합니다.

다음 구성은 하나의 기본 아이콘으로 모든 플랫폼에서 사용할 수 있도록 설정하는 것을 보여줍니다.

        <icon src="res/icon.png" />
    

또한 각 플랫폼에 대해서 서로 다른 화면 해상도들에 대하여 픽셀단위로 화면에 꼭 알맞는 아이콘들을 정의할 수도 있습니다.

아마존 Fire OS

         <platform name="amazon-fireos">
                  <icon src="res/android/ldpi.png" density="ldpi" />
                  <icon src="res/android/mdpi.png" density="mdpi" />
                  <icon src="res/android/hdpi.png" density="hdpi" />
                  <icon src="res/android/xhdpi.png" density="xhdpi" />
         </platform>
    

안드로이드

         <platform name="android">
                  <icon src="res/android/ldpi.png" density="ldpi" />
                  <icon src="res/android/mdpi.png" density="mdpi" />
                  <icon src="res/android/hdpi.png" density="hdpi" />
                  <icon src="res/android/xhdpi.png" density="xhdpi" />
         </platform>
    

블랙베리 10

         <platform name="blackberry10">
                  <icon src="res/bb10/icon-86.png" />
                  <icon src="res/bb10/icon-150.png" />
         </platform>
    

보다 다양한 크기와 로케일 설정을 위하여는 블랙베리의 설명서를 참조 하십시오. [http://developer.blackberry.com/html5/documentation/icon_element.html]

Firefox 운영 체제

         <platform name="firefoxos">
                  <icon src="res/ff/logo.png" width="60" height="60" />
         </platform>
    

iOS

         <platform name="ios">
                  <!-- iOS 8.0+ -->
                  <!-- iPhone 6 Plus  -->
                  <icon src="res/ios/icon-60@3x.png" width="180" height="180" />
                  <!-- iOS 7.0+ -->
                  <!-- iPhone / iPod Touch  -->
                  <icon src="res/ios/icon-60.png" width="60" height="60" />
                  <icon src="res/ios/icon-60@2x.png" width="120" height="120" />
                  <!-- iPad -->
                  <icon src="res/ios/icon-76.png" width="76" height="76" />
                  <icon src="res/ios/icon-76@2x.png" width="152" height="152" />
                  <!-- iOS 6.1 -->
                  <!-- Spotlight Icon -->
                  <icon src="res/ios/icon-40.png" width="40" height="40" />
                  <icon src="res/ios/icon-40@2x.png" width="80" height="80" />
                  <!-- iPhone / iPod Touch -->
                  <icon src="res/ios/icon.png" width="57" height="57" />
                  <icon src="res/ios/icon@2x.png" width="114" height="114" />
                  <!-- iPad -->
                  <icon src="res/ios/icon-72.png" width="72" height="72" />
                  <icon src="res/ios/icon-72@2x.png" width="144" height="144" />
                  <!-- iPhone Spotlight and Settings Icon -->
                  <icon src="res/ios/icon-small.png" width="29" height="29" />
                  <icon src="res/ios/icon-small@2x.png" width="58" height="58" />
                  <!-- iPad Spotlight and Settings Icon -->
                  <icon src="res/ios/icon-50.png" width="50" height="50" />
                  <icon src="res/ios/icon-50@2x.png" width="100" height="100" />
         </platform>
    

타이젠

         <platform name="tizen">
                  <icon src="res/tizen/icon-128.png" width="128" height="128" />
         </platform>
    

윈도우폰 8

         <platform name="wp8">
                  <icon src="res/wp/ApplicationIcon.png" width="99" height="99" />
                  <!-- tile image -->
                  <icon src="res/wp/Background.png" width="159" height="159" />
         </platform>
    

윈도우8

         <platform name="windows8">
                  <icon src="res/windows8/logo.png" width="150" height="150" />
                  <icon src="res/windows8/smalllogo.png" width="30" height="30" />
                  <icon src="res/windows8/storelogo.png" width="50" height="50" />
         </platform>
    

## CLI 을 사용하여 시작화면을 구성하기

최상위 수준에 있는 `config.xml` 파일에 (`platforms` 아래에 있는 것이 아닙니다.), 여기에서 지정된 것과 같은 구성 요소를 추가합니다.

# 예제 구성

"src" 속성의 값은 프로젝트 디렉터리에 대한 상대값으로 설정되지 www 디렉토리를 기준으로 설정되지 않음을 참조 하십시오. 당신은 원하는 소스 이미지 이름을 지정할 수 있습니다. 앱 내부 에서 사용되는 이름은 코르도바에 의해 결정 됩니다.

    <platform name="android">
        <!-- you can use any density that exists in the Android project -->
        <splash src="res/screen/android/splash-land-hdpi.png" density="land-hdpi"/>
        <splash src="res/screen/android/splash-land-ldpi.png" density="land-ldpi"/>
        <splash src="res/screen/android/splash-land-mdpi.png" density="land-mdpi"/>
        <splash src="res/screen/android/splash-land-xhdpi.png" density="land-xhdpi"/>
    
        <splash src="res/screen/android/splash-port-hdpi.png" density="port-hdpi"/>
        <splash src="res/screen/android/splash-port-ldpi.png" density="port-ldpi"/>
        <splash src="res/screen/android/splash-port-mdpi.png" density="port-mdpi"/>
        <splash src="res/screen/android/splash-port-xhdpi.png" density="port-xhdpi"/>
    </platform>
    
    <platform name="ios">
        <!-- images are determined by width and height. The following are supported -->
        <splash src="res/screen/ios/Default~iphone.png" width="320" height="480"/>
        <splash src="res/screen/ios/Default@2x~iphone.png" width="640" height="960"/>
        <splash src="res/screen/ios/Default-Portrait~ipad.png" width="768" height="1024"/>
        <splash src="res/screen/ios/Default-Portrait@2x~ipad.png" width="1536" height="2048"/>
        <splash src="res/screen/ios/Default-Landscape~ipad.png" width="1024" height="768"/>
        <splash src="res/screen/ios/Default-Landscape@2x~ipad.png" width="2048" height="1536"/>
        <splash src="res/screen/ios/Default-568h@2x~iphone.png" width="640" height="1136"/>
        <splash src="res/screen/ios/Default-667h.png" width="750" height="1334"/>
        <splash src="res/screen/ios/Default-736h.png" width="1242" height="2208"/>
        <splash src="res/screen/ios/Default-Landscape-736h.png" width="2208" height="1242"/>
    </platform>
    
    <platform name="wp8">
        <!-- images are determined by width and height. The following are supported -->
        <splash src="res/screen/wp8/SplashScreenImage.jpg" width="768" height="1280"/>
    </platform>
    
    <platform name="windows8">
        <!-- images are determined by width and height. The following are supported -->
        <splash src="res/screen/windows8/splashscreen.png" width="620" height="300"/>
    </platform>
    
    <platform name="blackberry10">
        <!-- Add a rim:splash element for each resolution and locale you wish -->
        <!-- http://developer.blackberry.com/html5/documentation/rim_splash_element.html -->
        <rim:splash src="res/screen/windows8/splashscreen.png"/>
    </platform>
    
    
    <preference name="SplashScreenDelay" value="10000" />
    

# 지원되는 플랫폼

지금 현재 (코르도바 3.5.0, 2014년 7월) 아래의 플랫폼들에 대하여 시작화면을 지원합니다.

    android
    ios
    wp8
    windows8
    blackberry10
    

# 시작화면(Splashscreen) 플러그인

아파치 코르도바는 앱이 시작하는 동안에 프로그래밍 방식으로 시작화면을 보이거나 감출수 있는 기능을 제공하는 특별한 시작화면 플러그인(Splash Screen Plugin)을 제공합니다.
 https://github.com/apache/cordova-plugin-splashscreen