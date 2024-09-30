---
layout: single
title: "[Digital Forenisc] - Hash Check method"
excerpt: "cmd, powershell"
categories:
  - Forensic
date: 2024-09-29
last_modified_at: 2024-09-30
---

# cmd

## Certutil

윈도우에서 간단하게 해시값을 구할 수 있다.<br>
인증서 관련 명령어지만 해시값을 구하기 위해 많은 사람들이 사용하는 것 같다.

![HashCheck](/assets/forensic/HashCheck/Certutil.png "Certutil")

![HashCheck](/assets/forensic/HashCheck/Certutil_use.png "Certutil")

![HashCheck](/assets/forensic/HashCheck/hashcheck.png "Certutil")


# PowerShell

## Get-FileHash

[Get-FileHash 설명](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.4)

![HashCheck](/assets/forensic/HashCheck/powershell.png "Get-FileHash")

![HashCheck](/assets/forensic/HashCheck/powershell2.png "Get-FileHash")

format-list 파이프 명령어를 입력해서 편하게 볼 수 있다. 