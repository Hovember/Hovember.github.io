---
layout: single
title: "윈도우 비트락커 잠금, 잠금 해제 명령어"
excerpt: "BitLocker 잠그기"
categories:
  - ETC
date: 2025-09-29
last_modified_at: 2025-09-29
---
<br>
<br>
관리자 권한으로 CMD 실행<br>

## 잠금 명령어 

```yaml
manage-bde.exe -lock -ForceDismount <드라이브명:>
Example: manage-bde.exe -lock -forcedismount d:
```

## 잠금 해제 명령어

```yaml
manage-bde.exe -unlock <드라이브명:> -password
Example : manage-bde -unlock D: -password
```

```yaml
manage-bde.exe -unlock <드라이브명:> -recoverypassword 복-구-키
Example : manage-bde -unlock D: -recoverypassword 111111-222222-333333-444444-555555-666666-777777-888888
```

```yaml
manage-bde.exe -unlock <드라이브명:> -recoverykey "경로"
Example : manage-bde -unlock D: -recoverykey "D:\RecoveryKey\123456-789012-...-888888.BEK"
```

