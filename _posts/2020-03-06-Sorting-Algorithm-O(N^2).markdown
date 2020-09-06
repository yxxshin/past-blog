---
layout: post
title: "Sorting Algorithm - O(N^2)"
description: 가장 간단한 정렬 알고리즘
date:   2020-03-06 04:00:30 +0900
categories: Algorithm-theory
---

시간복잡도가 $$O(n^2)$$ 인 정렬에는 **선택정렬, 삽입정렬, 버블정렬** 등이 있다.

참고) 아래의 정렬 구현 시에는 다음과 같은 매크로를 사용하였다.  
`#define SWAP(x,y,temp) ( (temp)=(x), (x)=(y), (y)=(temp) )` 

### 1. 선택 정렬 (Selection Sort)
```c++
void selection_sort(int list[], int n) {
 int i, j, min, temp;
 
 //마지막 숫자는 자동 정렬이므로 n-1번 반복
 for(i=0; i<n-1; i++) {
  min = i;
  
  //최솟값 탐색
  for(j=i+1; j<n; j++) {
   if(list[j]<list[min])
    min = j;
  }
  if(i != min) SWAP(list[i],list[min],temp);
 }
}
```
전체 배열에서 최솟값을 찾고, 가장 앞의 숫자와 바꾼다.  
그 다음 숫자는 두 번째로 작은 숫자와 바꾼다.  

![선택정렬](https://imgur.com/s7Wjsxu.png)

### 2. 삽입 정렬 (Insertion Sort)
```c++
void insertion_sort(int list[], int n) {
 int i, j, key;
 for(i=1; i<n; i++) {
  key = list[i]; // 삽입될 숫자(i번째 정수)를 key 변수로 복사
  // 현재 정렬된 배열은 i-1 까지이므로 i-1부터 역순으로 조사한다
  // key 보다 정렬된 배열에 있는 값이 크면 j번째를 j+1번째로 이동
  for(j=i-1; j>=0 && list[j]>key; j--) {
   list[j+1] = list[j];
  }
  list[j+1] = key;
 }
}
```
두 번째 숫자는 첫 번째 숫자와 비교한다.  
세 번째 숫자는 앞의 두 숫자와 비교하여, 자리에 맞게 정렬한다. 단, 자신의 바로 앞 숫자부터 앞으로 가면서 비교한다.   
오름차순 정렬의 경우,  자신(key)보다 숫자가 크다면 그 숫자를 한 칸 뒤로 보내고, 자신(key)는 앞으로 한 칸씩 옮긴다. 자신(key)보다 숫자가 작이지는 순간 그 자리에 key를 삽입한다.

![삽입정렬](https://imgur.com/JMAjMFh.png)


### 3. 버블 정렬 (Bubble Sort)
```c++
void bubble_sort(int list[], int n){
 int i, j, temp;
 
 for(i=n-1; i>0; i--) {
  for(j=0; j<i; j++) {
   if(list[j+1]<list[j]) SWAP(list[j+1],list[j],temp);
  }
 }
}
```
인접한 두 개씩을 비교하여 정렬하는 방식이다.  
오름차순 정렬의 경우, 1회전을 하면 가장 큰 숫자가 맨 뒤로 가게 된다.  
한 회전을 할 때마다 뒤에 (알맞게 정렬된) 숫자를 하나씩 쌓는다.

![버블정렬](https://imgur.com/r0wYOOr.png)
