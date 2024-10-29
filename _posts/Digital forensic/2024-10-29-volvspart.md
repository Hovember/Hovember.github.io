---
layout: single
title: "[Digital Forenisc] - 파티션과 볼륨의 차이"
excerpt: "파티션과 볼륨의 차이"
categories:
  - Forensic
date: 2024-10-29
last_modified_at: 2024-10-29
---

<br>
<br>

파티션과 볼륨의 차이는 "공간의 연속 여부"<br>

볼륨은 물리적으로 연속된 공간의 사용 여부와 관계 없이 섹터들의 집합인 반면 

파티션은 연속된 공간이어야, 연속된 섹터야 한다.  

파티션은 볼륨의 개념 중 하나? 

하나의 디스크는 연속된 공간으로 이루어져 있어 디스크 하나는 파티션을 통해 공간을 나누어 사용 가능

하지만, 여러 디스크는 각각의 물리적 장치로 연속된 공간으로 볼 수 없다. 

![Slack Space Area](/assets/forensic/Slack/partition.png "File Slack")