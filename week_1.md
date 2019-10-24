# Review of C language

## 1. Function
### - Example 1
#### - Make a function that sums from 1 to N and output the result.
```C++
#include<stdio.h>
int sum(int n);

void main() {
	int n;
	printf("1부터 n까지의 합 계산 \n");
	printf("정수 n 입력 :");
	scanf_s("%d", &n);
	printf("1부터 %d까지의 합:%d \n", n, sum(n));
}
int sum(int n) {
	int a = 0;
	for (int i = 1; i <= n; i += 1) {
		a += i;
	}
	return a;
}
```
### - Example 2
#### - Get the score(integer) as an input and output the grade (A, B, C, D, E)
```C++
#include<stdio.h>
#include<Windows.h>

void Grade(int a) {
	int i, sum = 0;
	if (a >= 80) printf("A");
	else if ((a >= 60) && (a < 80)) printf("B");
	else if ((a >= 40) && (a < 60)) printf("C");
	else if ((a >= 20) && (a < 40)) printf("D");
	else if ((a >= 0) && (a < 20)) printf("E");
}

int main() {
	int a;
	int sum;
	printf("100보다 작은 정수 하나를 입력하시오 : ");
	scanf_s("%d", &a);

	Grade(a);

	Sleep(10000);
	return 0;
}
```

### - Task (1)
```C++
#include <stdio.h>

int Add(int a, int b){
  int sum;
  /* Write down your own code */
  return sum;
}

int Add3Input(int a, int b, int c){
  int sum;
  /* Write down your own code */
  return sum;
}

int Average(int a, int b, int c){
  int average;
  /* Write down your own code */
  return average;
}

int AverageFunc(int a, int b, int c){
  int average;
  /* Write down your own code(Using Add3Input function) */
  return average;
}

int main(void){
  int math = 99, c_language = 100, english = 49;
  int sum=0, sum_3input;
  double average, average_func;
  
  sum = Add(math, c_language);
  sum = Add(sum, english);
  sum_3input = Add3Input(math, c_language, english);
  
  average = Average(math, c_language, english);
  average_func = AverageFunc(math, c_language, english);
  
  printf("the sum of my scores is %d. it's equal to %d \n", sum, sum_3input);
  printf("my average is %.3f. it's equal to %d \.3f", average, average_func);
  return 0;
}
```

## 2. Pointer
### - Example 1
```C++
#include <stdio.h>

int main(void) {
	int k = 8, i = 3;
	int *ptr;
	
	ptr = &k;

	printf("K's value : %d \n", k);
	printf("value of pointed p : %d \n", *ptr);

	*ptr = i;
	
	printf("K's value : %d \n", k);
	printf("value of pointed p : %d \n", *ptr);

	return 0;
}
```
### - Task (2)
```C++
#include <stdio.h>

int main(void){
  int i = 10;
  int *pi = &i;
  printf("i = %d, pi = %p \n", i ,pi);
  (*pi)++;
  
  printf("i = %d, pi = %p \n", i, pi);
  *(pi++);
  
  printf("i = %d, pi = %p \n", i, pi);
  
  return 0;
}
```

## 3. Array
### - Example 1
```C++
#include <stdio.h>
#include <stdlib.h>

int main(void) {
	int a[30] = { 0, };
	int i;

	for (i = 0; i < 30; i++) {
		a[i] = rand();
	}

	for (i = 0; i < 30; i++) {
		printf("%d \n", a[i]);
	}

	return 0;
}
```
### - Task (3)
```C++
#include <stdio.h>
#include <iostream>

int main(void) {
	int a[] = { 10, 20, 30, 40 };
	int *p;
  
  p = a;
  
  printf("a[0]=%d a[1]=%d a[2]=%d", a[0], a[1], a[2]);
  printf("p[0]=%d p[1]=%d p[2]=%d", p[0], p[1], p[2]);
  
  p[0] = 60;
  p[1] = 70;
  p[2] = 80;
  
  printf("a[0]=%d a[1]=%d a[2]=%d", a[0], a[1], a[2]);
  printf("p[0]=%d p[1]=%d p[2]=%d", p[0], p[1], p[2]);
  
	return 0;
}
```
## 4. Structure
### - Example 1
```C++
#include <stdio.h>
#include <iostream>
#include <Windows.h>

char copy_str(char *dest, const char *src);

struct Books {
	// 책 이름
	char name[30];
	// 저자 이름
	char auth[30];
	// 출판사 이름
	char publ[30];
	// 대출 여부?
	int borrowed;
};

int main() {
	struct Books Harry_Potter;

	copy_str(Harry_Potter.name, "Harry Potter");
	copy_str(Harry_Potter.auth, "J.K. Rolling");
	copy_str(Harry_Potter.publ, "Scholastic");
	Harry_Potter.borrowed = 0;

	printf("책 이름 : %s \n", Harry_Potter.name);
	printf("저자 이름 : %s \n", Harry_Potter.auth);
	printf("출판사 이름 : %s \n", Harry_Potter.publ);
	Sleep(10000);
	return 0;
}

char copy_str(char *dest, const char * src) {
	while (*src) {
		*dest = *src;
		src++;
		dest++;
	}
	*dest = '\0';
	return 1;
}
```

### - Task (4)
```C++
#include <stdio.h>
struct student{
  char *name;
  int student_num;
  double height;
  char *bestfriend[3];
};

int main(void){
  struct student sewoong = {"sewoong", 2008035433, 191.9, {"SongJa", "MalJa", "Chamja"}}
  struct student *ptr;
  
  /*
  
    Write down your own code
  
  */
  
  printf("student name : %s\n", ptr->name);
  printf("student num : %d\n", ptr->student_num);
  printf("student height : %.1f\n", ptr->height);
  printf("student friend1 : %d\n", ptr->bestfriend[0]);
  printf("student friend2 : %d\n", ptr->bestfriend[1]);
  printf("student friend3 : %d\n", ptr->bestfriend[2]);
}
```
