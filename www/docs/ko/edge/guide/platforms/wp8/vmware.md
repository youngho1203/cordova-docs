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

# Vm 웨어 퓨전을 구성

이 단원에는 코르도바를 사용하여 윈도우폰 응용 프로그램을 생성 하는 맥에서 vm 웨어 퓨전을 구성하는 방법을 보여줍니다.

[마이크로소프트 개발자 네트워크][1] 는 vm 웨어 퓨전에서 윈도우를 실행하는 방법에 대한 일반적인 지침을 제공합니다. 윈도우를 설치한 후 다음이 단계를 따르십시오.

 [1]: http://msdn.microsoft.com/en-US/library/windows/apps/jj945426

1.  Vm 웨어 퓨전, 선택 윈도우 8 디스크 이미지를 준비 하 고 **설정** 을 선택.

2.  **프로세서 및 메모리** 구성 옵션을 선택합니다. *두 개의* 프로세서 코어를 지정해야 및 **이 가상 머신에서 하이퍼바이저**응용 프로그램:
    
    ![][2]
    
    윈도우폰 에뮬레이터 혼자 전반적 vm 웨어에 대한 최소 2 GB를 보유 해야 절반을 기가 바이트의 메모리를 사용합니다.

3.  **고급** 설정을 선택합니다. 활성화는 **기본 가상화 엔진: EPT와 인텔 VT x** 옵션:
    
    ![][3]

4.  수정 *.vmx* 파일을 추가 또는 다음 설정을 수정 합니다.
    
        hypervisor.cpuid.v0 = "FALSE" mce.enable = "TRUE" vhv.enable = "TRUE"
        

 [2]: img/guide/platforms/wp8/vmware_memory_opts.png
 [3]: img/guide/platforms/wp8/vmware_advanced_opts.png

이러한 단계를 완료 하면 일단 준비가 다음 윈도우폰 SDK를 설치합니다. 자세한 내용은 윈도우폰 8 플랫폼 설명서를 참조하십시오.