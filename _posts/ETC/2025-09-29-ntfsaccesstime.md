---
layout: single
title: "윈도우 NTFS 접근 시간"
excerpt: "업데이트 변경"
categories:
  - ETC
date: 2025-09-29
last_modified_at: 2025-09-29
---

<br>
<br>

 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem<br>
 NtfsDisableLastAccessUpdate Key

- 0x80000000: User Managed, the “Last Access” updates are enabled,<br>
- 0x80000001: User Managed, the “Last Access” updates are disabled,<br>
- 0x80000002: System Managed, the “Last Access” updates are enabled, (default)<br>
- 0x80000003: System Managed, the “Last Access” updates are disabled.
