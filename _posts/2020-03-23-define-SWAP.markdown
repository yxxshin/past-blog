---
layout: post
title: "#define SWAP macro"
description: "일반적인 #define SWAP 형태"
date:   2020-03-20 16:00:00 +0900
categories: [ Others ]
tags: [ manual ]
---

SWAP을 자주 사용하는 경우에는, 아래와 같이 임의의 type에 대한 SWAP 함수를 매크로로 지정해 놓으면 편하다.   
(특히, C 언어에서!)


```c++
#define SWAP(a,b,type) do{ \
    type temp; \
    temp=a; \
    a=b; \
    b=temp; \
}while(0)
```

define 매크로에 여러 줄을 넣기 위해서는 do while 문을 활용해야 한다.  
위와 같은 형태로 SWAP 매크로를 작성하면, int 형인 a와 b의 값을 바꿔야 할 때 SWAP(a, b, int) 와 같이 바꿀 수 있다.