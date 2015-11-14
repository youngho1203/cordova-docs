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

# Parallels Desktop 구성

이 단원에서는 코르도바를 사용하여 윈도우폰 응용 프로그램을 생성 하는 맥에 Parallels Desktop을 구성하는 방법을 보여줍니다.

[마이크로소프트 개발자 네트워크][1] Parallels Desktop에서 윈도우를 실행하는 방법에 대한 일반적인 지침을 제공합니다. 윈도우를 설치한 후 다음이 단계를 따르십시오.

 [1]: http://msdn.microsoft.com/en-US/library/windows/apps/jj945424

1.  Parallels Desktop에서 준비 했습니다 윈도우 8 디스크 이미지를 선택하고 **설정** 을 선택.

2.  **일반 → CPU** 옵션을 선택합니다. *2 개의* CPU를 지정합니다. 권장된 범위를 벗어나는 경우에 적어도 2GB의 메모리를 지정합니다.
    
    ![][2]

3.  윈도우 8 가상 컴퓨터 내에서 장치 에뮬레이터 이미지를 실행할 수, **최적화** 옵션을 선택하고 **중첩 된 가상화** 를 사용하도록 설정.
    
    ![][3]

 [2]: img/guide/platforms/wp8/parallel_cpu_opts.png
 [3]: img/guide/platforms/wp8/parallel_optimize_opts.png

이러한 단계를 완료되면 윈도우폰 SDK를 설치할 준비가 되었습니다. 자세한 내용은 윈도우폰 8 플랫폼 설명서를 참조하십시오.