---
layout: single
title: "[Digital Forenisc] - Thumbnail 파일 분석"
excerpt: "썸네일 파일 분석"
categories:
  - Forensic
date: 2024-09-02
last_modified_at: 2024-09-02
---

# 썸네일 (Thumbnail)

-	큰 이미지를 축소하여 많은 양의 이미지를 빠르게 보여주기 위한 기능
-	PDF, HTML, 그래픽 이미지 파일 등 지원
-	처음 열람할 때 썸네일을 저장하고 다시 읽을 때 만들어진 썸네일을 보여줌
-	썸네일은 DB 형식으로 보관된다. 
    - 원본 파일이 삭제되어도 남아있는다.
    - 사용자가 직접 썸네일을 지우지 않는 이상 썸네일은 DB에 남아있는다. 
    - 중요한 증거가 될 수 있다.

경로:<br>
%UserProfile%\AppData\Local\Microsoft\Windows\Explorer\thumbcache_##.db 

썸네일 크기별로 파일이 존재하며 생성되는 포맷도 다르다.<br>

|         File        	|       Description      	|
|:-------------------:	|:----------------------:	|
|  thumbcache_idx.db  	|  썸네일의 인덱스 정보  	|
| thumbcache_16~96.db 	|    bmp 포맷으로 저장   	|
|  thumbcache_256~.db 	| jpg, png 포맷으로 저장 	|


![Thumbnail](/assets/forensic/Thumbnail/Thumbnail.png "Thumbnail")

\#\# 숫자보다 같거나 작은 픽셀 크기의 이미지로 저장된다.<br>
*1280부터는 뭔가 섞여 있는 느낌이 든다. 577x122이도 들어있다. 

Thumbcache viewer 도구로 썸네일을 확인할 수 있다. 

# Thumbnail 구조

시그니처 “CMMM” 기준으로 Header와 Cache Entry로 나눠져 있다. <br>
시그니처 다음 Header, 시그니처 다음 Entry #1, 시그니처 다음 Entry #2 이런 식으로 나눠져 있다.<br> 
여러 Cache Entry가 있으며 각각 썸네일이 저장되어 있다.<br>

| 썸네일 	|      구조      	|
|:------:	|:--------------:	|
| "CMMM" 	|   File Header  	|
| "CMMM" 	| Cache Entry #1 	|
| "CMMM" 	| Cache Entry #2 	|

## Header

|                     Field                    |     Offset (d)    |     Size (Byte)    |                                                                                               Description                                                                                             |
|:--------------------------------------------:|:-----------------:|:------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                   Signature                  |        0 – 3      |          4         |                                                                                                 “CMMM”                                                                                                |
|                Windows Version               |        4 – 7      |          4         |                                                                          Windows 10: 0x20<br> Windows 7: 0x15<br> Windows Vista: 0x14                                                                         |
|                   Cache Type                 |       8 - 11      |          4         |     Windows 10 기준: 16(0x00), 32(0x01), 48(0x02), 96(0x03), 256(0x04), 768(0x05), 1280(0x06), 1920(0x07), 2560(0x08), sr(0x09), wide(0x0A), exif(0x0B), wide_alternate(0x0C), custom_stream(0x0D)    |
|          Offset to First Cache Entry         |       12 – 15     |          4         |                                                                                                 항상 0                                                                                                |
|     Offset to First available Cache Entry    |       16 – 19     |          4         |                                                                                 이게 First Cache Entry 같다.<br> 항상 0x18                                                                               |
|             Total Size of Entries            |       20 - 23     |          4         |                                                                                                                                                                                                       |


![Thumbnail](/assets/forensic/Thumbnail/Header.png "Thumbnail Header")

## Cache Entry 구조


|           Field         |   Offset (d)   |     Size (Byte)    |         Description        |
|:-----------------------:|:--------------:|:------------------:|:--------------------------:|
|         Signature       |      0 – 3     |          4         |            “CMMM”          |
|     Cache Entry Size    |      4 – 7     |          4         |       Cache Entry 크기     |
|     Cache Entry Hash    |      8 – 15    |          8         |     Cache Entry 해시 값    |
|      Filename length    |     16 – 19    |          4         |        파일 이름 길이      |
|       Padding Size      |     20 – 23    |          4         |          패딩 크기         |
|         Data Size       |     24 – 27    |          4         |         데이터 크기        |
|           Width         |     28 – 31    |          4         |             너비           |
|          Height         |     32 – 35    |          4         |             높이           |
|            ??           |     36 - 39    |          4         |              ??            |
|       Data Checksum     |     40 - 47    |          8         |        데이터 해시 값      |
|      Header Checksum    |     48 - 56    |          8         |         헤더 해시 값       |
|         File Name       |     57 - 88    |          32        |          파일 이름         |
|           Data          |       89~      |         가변       |            데이터          |


![Thumbnail](/assets/forensic/Thumbnail/cache_entry.png "Thumbnail Cache Entry")

Thumbcache Viewer 도구로 확인한 모습 

![Thumbnail](/assets/forensic/Thumbnail/thumbcache_viewer.png "thumbcache_viewer")


<span style = "color: red">Data Offset = Cache Entry Offset + (Cache Entry Size – Data Size)</span>

![Thumbnail](/assets/forensic/Thumbnail/Header+Entry.png "Thumbnail Header+Entry")


# 디지털 포렌식 관점

포렌식 활용 분야
-	사진, 동영상, 문서 등 파일의 존재 여부 확인 가능
    - 윈도우 탐색기로 미리보기 하면 자동으로 썸네일 생성되기 때문
    - 썸네일DB 파일을 조사하여 삭제 파일의 존재성을 입증할 수 있다.

-	파일의 일부 내용 확인 가능 (야동 포르노 및 문서 유출의 증거로 활용)
    - 문서 파일의 경우 첫 페이지가 썸네일이 되기 때문에 일부 내용 확인 가능
    - 탐색기에서 “미리 보기 창”과는 좀 다른 거 같다. 
    - 문서 파일 설정에서 변경하여 첫 페이지가 썸네일이 되게 할 수 있다.
    - 멀티미디어의 경우 원본 저작물과 조사 대상 시스템의 썸네일을 비교 분석하여 디지털 증거에 활용할 수 있는 정보를 얻을 수 있다.

-	파일을 처음 열람할 때 썸네일이 생성되므로 활동 추적 가능?
    - 처음 열람할 때 생성되는 썸네일로 활동 추적이 가능할까?
    - 실행했다는 것만 본다면?

<br>
<br>

테스트를 좀 했는데 맞는지 모르겠다.<br> 사진 크기에 따라서 다르게 나올 수 있지만<br>
1636x626 사진으로 테스트한 결과<br>  
큰 아이콘 - 256에 저장<br>
타일 - 96에 저장<br>
내용 - 48에 저장<br>

