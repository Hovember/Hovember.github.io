---
layout: single
title: "[Digital Forenisc] - IconCache"
excerpt: "IconCache"
categories:
  - Forensic
date: 2024-09-02
last_modified_at: 2024-09-02
---

# IconCache

- 윈도우에서 사용되는 아이콘을 DB 형식으로 저장
- 원본 파일이 삭제되어도 남아있다.


경로: 썸네일.db 파일이 있는 같은 곳에 위치에 있다. 

%UserProfile%\AppData\Local\Microsoft\Windows\Explorer\iconcache_##.db 

아이콘 크기별로 파일이 존재하며 생성되는 포맷도 다르다.<br>

16, 32, 48 - bmp<br>
256 - png<br>

thumbcache.db 파일과 동일한 구조를 가지기 때문에 
마찬가지로 Thumbcache Viewer 도구로 확인할 수 있다.

# 디지털 포렌식 관점 

- 응용프로그램 사용 여부(아이콘이 있다는 것은 시스템에 존재했다는 것)
- 안티 포렌식 도구의 사용 여부
- 삭제된 응용프로그램의 존재 여부
- 외부저장매체를 통해 실행 여부?
- 아이콘이 존재하는 악성코드 흔적 확인 (스파이웨어 감염 흔적)
- 파일 다운로드 흔적 확인 (파일 다운로드 시 자동 생성)


생성했을 때 생긴다.

# 번외

윈도우 기본 아이콘 위치: %SystemRoot%system32\shell32.dll

아이콘 추출 도구: IconsExtract
[https://www.nirsoft.net/utils/iconsext.html](https://www.nirsoft.net/utils/iconsext.html)

