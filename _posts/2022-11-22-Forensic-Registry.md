---
layout: single
title: "Registry Forensic"
categories:
  - Forensic
date: 2022-11-22
last_modified_at:
---

Registry? Registry Artifacts?
{: .notice--primary}

# Registry 

레지스트리란 운영체제와 응용프로그램에 필요한 정보를 가지고 있는 계층형 데이터베이스이다. 데이터는 트리 형식으로 구성되고 트리의 각 노드를 키라고 한다. 각 키에는 하위 키와 값이 모두 포함될 수 있다. 

![대체 텍스트](/assets/images/2.png "레지스트리 구조")<br>
\<레지스트리 구조 예\>

HKEY_CURRENT_USER 키에는 Console, Control Panel 등 하위 키가 있고, 이러한 각 키에도 하위 키가 있다. Colors 하위 키 아래는 GrayText, Hilight 등 값\(Value\)이 있고, 값에 대한 Data Type, Data가 있다.

## Registry Hive

*Hive*는 레지스트리의 키, 하위 키 및 값의 논리적\(사람이 볼 수 있는 형태\) 그룹이다. 
운영체제가 시작되거나 사용자가 로그인할 때 지원 파일 집합이 메모리에 로드된다. 

지원 파일은 물리적인 파일이어서 일반적인 방법으로는 접근할 수 없다. \(Registry View를 사용, 메모리에 로드되어 있기 때문에 FTK Imager로 추출 후 사용하면 된다.\)

활성 시스템의 레지스트리를 구성하는 하이브 목록은
HKLM\\SYSTEM\\CurrentControlSet\\Control\\hivelist에서 볼 수 있다.  

활성 시스템 (Live System)이란, 전원에 연결되어 정상적으로 가동 중인 시스템을 의미한다.
{: .notice--success}


하이브 지원 파일은 대부분 Windows\\System32\\Config \(%SystemRoot%\\System32\\Config\) 폴더에 있다.

| 레지스트리 하이브 | 지원파일 |
|:----------------:|:---------:|
|HKCC|System, System.alt, System.log, System.sav|
|HKCU|Ntuser.dat, Ntuser.dat.log|
|HKLM\\SAM|Sam, Sam.log, Sam.sav|
|HKLM\\Security|Security, Security.log, Security.sav|
|HKLM\\Software|Software, Software.log, Software.sav|
|HKLM\\System|System, System.alt, System.log, System.sav|
|HKU\\.DEFAULT|Default, Default.log, Default.sav|

❓<br>.alt는 HKLM\\System 하이브의 백업 복사본이다.<br>.sav는 하이브의 백업 복사본이다.<br>.log는 하이브의 키 및 값에 대한 변경 내용이다. 
{: .notice--success}




🤔<br>하이브는 파일인가? 
마이크로소프트에서는 하이브 파일이라는 말이 없고 하이브에 대한 지원 파일이라고 나와있다. 하이브는 지원 파일 집합이 메모리에 로드되는 레지스트리의 키, 하위 키 및 값의 논리적 그룹이라고 나와있다. 하지만 많은 블로그에서 하이브 파일은 ~~다라는 글이 많다. 
{: .notice}

# Registry Artifacts



# Reference💻

<https://learn.microsoft.com/ko-kr/windows/win32/sysinfo/registry><br> 
<http://www.forensic-artifacts.com/registry-forensics/main><br>
<https://learn.microsoft.com/ko-kr/troubleshoot/windows-server/performance/windows-registry-advanced-users?source=recommendations><br>
{: .notice--warning}