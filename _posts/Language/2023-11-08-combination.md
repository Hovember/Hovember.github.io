---
layout: single
title: "[C Language] - ����"
categories:
  - Language
date: 2023-11-08
last_modified_at: 
---

����, Combination
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
	// printf("%d\n", comb1(n) / (comb1(n - k) * comb1(k))); // n�� Ŀ���� StackOverflow �߻� 
	printf("%d\n", comb2(n, k));
	printf("%d\n", comb3(n, total) / (comb3(n - k, total) * comb3(k, total)));
	printf("%d\n", solution(n, k));
}

int comb1(int a) {  // ���丮�� ����Ѵ�. �ڱ� �ڽ��� ȣ���� �� ����� ��ٸ��鼭 ���� ���� 
	
	if (a == 1) return 1;

	return a * comb1(a - 1);
	

}

int comb2(int a, int b) { // ���丮���� ������� �ʴ´�. 
	if (a == b) return 1; // 3���� 3���� ���� ����� �� 1��

	else if (b == 1) return a; // 3���� 1���� ���� ����� �� 3�� 

	else return comb2(a - 1, b) + comb2(a - 1, b - 1); 
	// ������ ���� ���� �ʾ��� �� + ����� �� 

	/* 
	1, 2, 3, 4 �� 2���� ���� ����� �� 
	1, 2
	1,    3
	   2, 3
	1,       4
	   2,    4 
	      3, 4
	4�� ����� �� 1, 2, 3 �� 1���� ���� �ȴ�. -> 1, 2, 3 �� 1���� ���� ����� ���� 3�� 
	4�� ���� �ʾ��� �� 1, 2, 3 �� 2���� ���� �ȴ�. 
	-> 1, 2, 3 �� 2���� ���� ����� �� 
	1, 2
	1,    3
	   2, 3
	3�� ����� �� 1, 2 �� 1���� ���� �ȴ�. -> ����� �� 2�� 
	3�� ���� �ʾ��� �� 1, 2 �� 2���� ���� �ȴ�. -> ����� �� 1�� 

	���� 6��
	*/
}

int comb3(int a, int total) { // ����Լ� ���� �ذ� ����� ���� ��� �Լ� ��� 
	
	if (a == 1) return total;

	else return comb3(a - 1, a * total);

}

```