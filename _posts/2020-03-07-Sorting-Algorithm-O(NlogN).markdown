---
layout: post
title: "Sorting Algorithm - O(NlogN)"
description: 조금 더 빨라진 정렬 알고리즘
date:   2020-03-07 15:00:00 +0900
categories: [ Algorithm ]
tags: [ sorting ]
---

시간 복잡도가 O(n^2)인 정렬은 간단하다는 장점이 있으나, 시간이 오래 걸린다는 단점을 피해갈 수 없다. 따라서 시간을 단축시키기 위해서는 시간 복잡도가 O(nlogn)인 정렬을 사용해야 한다.  본 글에서는 시간 복잡도가 O(nlogn)인 정렬로 **힙 정렬, 합병 정렬**을 소개한다.

### 1. 힙 정렬 (Heap Sort)
'힙(Heap)'은 완전 이진 트리의 일종이다. 최대 힙(max heap)과 최소 힙(min heap)이 있는데, 각각은 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은(작거나 같은) 힙을 의미한다.

![힙](https://imgur.com/Yum328r.png)

힙은 표준적으로 배열을 이용하여 저장한다(사진 참고). 쉬운 구현을 위해 index 0을 사용하지 않으며 (즉, 1부터 시작), index들은 다음과 같은 관계를 가진다.

1. 왼쪽 자식의 index = (부모의 index) * 2
2. 오른쪽 자식의 index = (부모의 index) * 2 + 1
3. 부모의 index = (자식의 index) / 2

![힙저장](https://imgur.com/ylBc3Re.png)
다음과 같이 구조체를 이용하여 표현해 볼 수 있다.
```c++
typedef struct {
    int heap[MAX_ELEMENT];
    int heap_size;
} HeapType;
```


이제, 최소 힙의 구현을 생각해 보자. (위의 그림은 최대 힙임)  
우선, 힙을 추가하는 경우(숫자를 대입하여 정렬하는 경우)를 생각한다.  

힙이 추가되면, 우선 가장 마지막 index에 대입한다. 이후, 부모 노드와 비교하면서 부모 노드가 본인보다 작을 때까지 부모 노드와 자신을 교환한다.

```c++
// 현재 요소의 개수가 heap_size인 힙 h에 data을 삽입한다.
void insert_heap(HeapType *h, int data) {
    int i;
    i = ++(h->heap_size);   // 힙 크기를 하나 증가

    // 트리를 거슬러 올라 가며 부모 노드와 비교하는 과정
    // i가 루트 노드가 아니고,data 값이 부모노드(i/2)보다 작으면
    while( (i!=1) && (data < h->heap[i/2])) {
        h->heap[i] = h->heap[i/2];
        i /= 2;
    }
    h->heap[i] = data;
}
```

다음으로, 최소 힙(가장 작은 숫자)을 삭제하는 경우(숫자를 빼내는 경우. 마지막 출력할 때)를 생각한다.   
최소 힙을 삭제하고, 가장 마지막 index의 힙을 그 자리(맨 위)로 올린다.  
이후, 힙의 성격에 맞게 정렬을 한다. 단, 주의할 점은 두 자식노드를 비교하여 정렬해야 한다는 점이다. 예로 최소 힙의 경우에는 두 자식 중 더 작은 자식 노드와 교환해야 한다.

```c++
int delete_heap(HeapType *h) {
    if(h->heap_size == 0) return -1;

    int ret = h->heap[1];
    int temp = h->heap[(h->heap_size)--];   // 마지막 노드를 temp에 담고 heap_size를 1 줄임.
    int parent = 1, child = 2;

    while(child <= h->heap_size) {

        // 현재 노드의 자식 노드 중 더 작은 자식 노드를 찾는다.
        if( child < h->heap_size && h->heap[child] > h->heap[child+1] )
            child++;

        // 더 작은 자식 노드보다 마지막 노드가 작으면 while문 정지
        if( temp <= h->heap[child] ) break;

        // 그렇지 않으면, 부모 노드와 작은 자식 노드 교환
        h->heap[parent] = h->heap[child];
        parent = child;
        child *= 2;
    }

    h->heap[parent] = temp;
    return ret;
}
```
우리는 힙의 삽입, 삭제를 이용하여 힙 정렬을 할 수 있다.  
완성된 전체 코드는 다음과 같다. (백준 2751 수 정렬하기(2))
```c++
#include <stdio.h>
#define MAX_ELEMENT 1000010

typedef struct {
    int heap[MAX_ELEMENT];
    int heap_size;
} HeapType;

// 현재 요소의 개수가 heap_size인 힙 h에 data을 삽입한다.
void insert_heap(HeapType *h, int data) {
    int i;
    i = ++(h->heap_size);   // 힙 크기를 하나 증가

    // 트리를 거슬러 올라 가며 부모 노드와 비교하는 과정
    // i가 루트 노드가 아니고,data 값이 부모노드(i/2)보다 작으면
    while( (i!=1) && (data < h->heap[i/2])) {
        h->heap[i] = h->heap[i/2];
        i /= 2;
    }
    h->heap[i] = data;
}

int delete_heap(HeapType *h) {
    if(h->heap_size == 0) return -1;

    int ret = h->heap[1];
    int temp = h->heap[(h->heap_size)--];   // 마지막 노드를 temp에 담고 heap_size를 1 줄임.
    int parent = 1, child = 2;

    while(child <= h->heap_size) {

        // 현재 노드의 자식 노드 중 더 작은 자식 노드를 찾는다.
        if( child < h->heap_size && h->heap[child] > h->heap[child+1] )
            child++;

        // 더 작은 자식 노드보다 마지막 노드가 작으면 while문 정지
        if( temp <= h->heap[child] ) break;

        // 그렇지 않으면, 부모 노드와 작은 자식 노드 교환
        h->heap[parent] = h->heap[child];
        parent = child;
        child *= 2;
    }

    h->heap[parent] = temp;
    return ret;
}

int main() {

    int N, data;
    scanf("%d",&N);
    HeapType heap1;
    heap1.heap_size = 0;

    for(int i=0; i<N; i++){
        scanf("%d",&data);
        insert_heap(&heap1,data);
    }

    for(int i=0; i<N; i++) {
        printf("%d\n", delete_heap(&heap1));
    }

}
```

힙 정렬의 시간 복잡도는 다음과 같이 구할 수 있다:  
힙 트리의 높이는 logn, 따라서 한 힙을 삽입할 때 걸리는 시간 logn,  
총 n개의 힙을 삽입할 때 걸리는 총 시간은 nlogn.  
또한, 힙 정렬은 안정 정렬(기존의 순서가 정렬 후에도 유지)이라는 성질이 있다.

### 2. 합병 정렬 (Merge Sort)
합병 정렬은 폰 노이만(Von Neumann)이 제안한 방법이며, 분할 정복 알고리즘의 하나이다.  
분할 정복(Divide and Conquer)은 문제를 분리하여 각각을 해결한 다음, 결과를 모아 원래 문제를 해결하는 전략이다.  

따라서 합병 정렬은 분할 > 정복 > 결합 의 순서로 이루어진다.  
분할 단계에서는 입력 받은 배열을 크기가 같은 두 개의 부분 배열로 분할한다.  
정복 단계에서는 각각의 부분 배열을 정렬한다. 부분 배열의 크기가 2보다 크다면 재귀 호출을 통해 그 부분 배열에서의 분할 단계로 넘어간다.  
결합 단계에서는 정렬이 끝난 부분 배열들을 하나의 배열로 합친다.  

![합병정렬](https://imgur.com/RBNFwIC.png)

합병 정렬의 시간 복잡도는 다음과 같이 구할 수 있다:  
합병 단계 수 logn, 비교 연산은 각 정렬 단계(혹은 크기 2인 부분 배열)에서 최대 n번,  
따라서 총 nlogn의 시간 복잡도를 가진다.