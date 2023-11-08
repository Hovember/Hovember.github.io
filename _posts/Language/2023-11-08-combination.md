---
layout: single
title: "[C Language] - 조합"
categories:
  - Language
date: 2023-11-08
last_modified_at: 
---

조합, Combination
{: .notice--primary}

```c
#include <stdio.h>

int main() {
	//printf("!1:\t%d\n", !1);
	//printf("!0:\t%d\n", !0);
	//printf("!!1:\t%d\n", !!1);
	//printf("!!0:\t%d\n", !!0);
	int n = 4;
	int k = 3;
	int total = 1;
	// printf("%d\n", comb1(n) / (comb1(n - k) * comb1(k))); // n이 커지면 StackOverflow 발생 
	printf("%d\n", comb2(n, k));
	printf("%d\n", comb3(n, total) / (comb3(n - k, total) * comb3(k, total)));
	printf("%d\n", solution(n, k));
}

int comb1(int a) {  // 팩토리얼 사용한다. 자기 자신을 호출한 뒤 결과를 기다리면서 스택 부하 
	
	if (a == 1) return 1;

	return a * comb1(a - 1);
	

}

int comb2(int a, int b) { // 팩토리얼을 사용하지 않는다. 
	if (a == b) return 1; // 3개중 3개를 고르는 경우의 수 1개

	else if (b == 1) return a; // 3개중 1개를 고르는 경우의 수 3개 

	else return comb2(a - 1, b) + comb2(a - 1, b - 1); 
	// 마지막 것을 고르지 않았을 때 + 골랐을 때 

	/* 
	1, 2, 3, 4 중 2개를 고르는 경우의 수 
	1, 2
	1,    3
	   2, 3
	1,       4
	   2,    4 
	      3, 4
	4를 골랐을 때 1, 2, 3 중 1개를 고르면 된다. -> 1, 2, 3 중 1개를 고르는 경우의 수는 3개 
	4를 고르지 않았을 때 1, 2, 3 중 2개를 고르면 된다. 
	-> 1, 2, 3 중 2개를 고르는 경우의 수 
	1, 2
	1,    3
	   2, 3
	3을 골랐을 때 1, 2 중 1개를 고르면 된다. -> 경우의 수 2개 
	3을 고르지 않았을 때 1, 2 중 2개를 고르면 된다. -> 경우의 수 1개 

	따라서 6개
	*/
}

int comb3(int a, int total) { // 재귀함수 단점 해결 방법인 꼬리 재귀 함수 사용 
	
	if (a == 1) return total;

	else return comb3(a - 1, a * total);

}

```