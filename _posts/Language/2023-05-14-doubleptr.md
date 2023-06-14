---
layout: single
title: "[C Language] - 더블포인터"
categories:
  - Language
date: 2023-05-14
last_modified_at: 
---

더블포인터에 대해서..
{: .notice--primary}

# 더블포인터

```c
#include <stdio.h>

int main(){
    int a= 10;
    int *aa = &a;
    int **aaa=&aa;

    printf("%d, %d\n\n", aa, *aaa);
    
    printf("%d\n", &a);
    printf("%d\n", &aa);
    printf("%d\n\n", &aaa);
    
    printf("%d\n", a);
    printf("%d\n", aa);
    printf("%d\n", aaa);

    // *aaa는 한 번 역참조해서 값을 가져옴 
    // **aaa는 두 번 역참조해서 값을 가져옴 
}
```

결과:<br>

6422300, 6422300<br>

6422300<br>
6422296<br>
6422292<br>

10<br>
6422300<br>
6422296<br>