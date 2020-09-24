---
layout: post
title: "Dynamic Programming - Knapsack Problem"
description: Dynamic Programming을 이용한 Knapsack problem
date:   2020-03-20 15:00:00 +0900
categories: [ Algorithm ]
tags: [ dp ]
---

두 번째로 소개할 Dynamic Programming 알고리즘은 **배낭 문제(Knapsack problem)**이다.

Knapsack Problem(배낭문제)란, 주어진 가치와 무게를 가진 짐들을 배낭에 넣을 때, 주어진 무게의 최댓값을 넘지 않으면서 가치의 합이 최대가 되도록 짐을 넣는 방법을 찾는 문제이다. 짐을 쪼갤 수 있는 경우는 분할가능 배낭문제(Fractional Knapsack Problem)이라 하고, 쪼갤 수 없는 경우는 **0-1 배낭문제(0-1 Knapsack Problem)**이라 한다. 본 글에서는 Dynamic Programming을 이용하여 0-1 Knapsack Problem을 해결할 것이다.

문제 상황은 [Baekjoon 12865][prob]를 참고하자. N개의 물건과, 최대 K의 무게를 담을 수 있는 배낭이 주어진다. 각 물건은 무게 W와 가치 V를 가진다. 우리는 가치의 최대가 되도록 물건들을 담아야 한다.

아이디어는 다음과 같다: 
```
D[i][j] 의 2차원 배열을 선언하는데, 이는 i번째 보석까지 탐색, 무게가 j만큼 사용되었을 때 가치의 최댓값이다.
```

`W[i], V[i]`를 i번 물건의 무게, 가치라고 하자.   
본 알고리즘에서는 i를 하나씩 늘려가며 `D[i][j]`를 계산할 것이다. 만약 i번째 보석을 가져간다면, `D[i][j] = D[i-1][j-W[i]] + V[i]` 이다. i번째 보석을 가져가지 않는다면, `D[i][j] = D[i-1][j]` 이다. 각 순간마다 위에서 제시한 `D[i-1][j], D[i-1][j-W[i]]+V[i]` 중 큰 경우를 선택하면 된다.

필자의 코드는 [여기][my] 에서 확인할 수 있다.

[prob]: https://www.acmicpc.net/problem/12865
[my]: https://yxxshin.github.io/category/baekjoon/Baekjoon-12865/
