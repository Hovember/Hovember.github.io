---
layout: single
title: "윈도우 비트락커 재부팅 없이 잠그는 방법"
excerpt: "BitLocker 잠그기"
categories:
  - ETC
date: 2025-09-29
last_modified_at: 2025-09-29
---

cmd 관리자 권한 실행<br>
```yaml
manage-bde.exe -lock -ForceDismount <드라이브명:>
```
e.g., manage-bde.exe -lock -forcedismount d: <br>
