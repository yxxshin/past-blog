---
layout: post
title: "Floyd-Warshall Algorithm"
description: "최단 경로 알고리즘 - 플로이드 워셜 알고리즘"
date:   2020-09-20 15:00:00 +0900
categories: [ Algorithm ]
tags: [ asp ]
use_math: true
---

ASP는 모든 정점이 출발점이 되어, 모든 정점에 대한 최단 거리를 구하는 것이다.

기존에 배운 두 가지 SSP (Dijkstra, Bellman-Ford) 를 정점의 개수만큼 진행하여도 답을 얻을 수 있지만, 굉장히 많은 연산이 소요된다.  
따라서, ASP 문제를 해결하기 위해서는 새로운 알고리즘을 이용해야 한다.

이번에 알아볼 ASP (All Pairs Shortest Path) 는 플로이드 워셜 알고리즘 (Floyd-Warshall Algorithm) 이다.

---

플로이드 워셜 알고리즘은 음의 가중치인 간선이 없어야 한다. 
기본적인 아이디어는 **Dynammic Programming** 이고, 최단 거리의 정보를 담는 2차원 배열을 놓고 모든 경우를 대입해 보면 된다.  

조금 더 자세히 살펴보자.  
2차원 배열 dp에 대해, `dp[from][to] = value` 가 되도록 하겠다.  

처음에는 INF (도달할 수 없음) 으로 초기화해 준다.  
이후, 점 i 에서 점 j 로 갈 때 점 temp 를 거치는 경우! 와 같이 세분화하여 3중 for 문을 돌린다.  
( 즉, 시간복잡도는 $O(V^3)$ 이다. )

** 가장 바깥쪽 temp, 그 안쪽이 i, 가장 안쪽이 j 에 대한 for문이다. (중요!!) **  
각 경우에 대하여, 기존 dp에 저장되어 있던 값과 새로 temp를 거치는 값을 비교하여 새 값이 더 작다면 갱신해 주면 된다.

필자가 직접 구현한 코드는 [Baekjoon 11404 (플로이드)][my] 에서 확인할 수 있다.

[my]: 