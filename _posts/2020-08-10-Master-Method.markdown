---
layout: post
title: "The Master Method"
description: "마스터 정리"
date:   2020-08-10 16:00:00 +0900
categories: [ Others ]
tags: [ manual ]
use_math: true
---

분할정복에 대하여 공부하던 도중, 점화식 형태로 시간복잡도 식이 나타날 때  
이 시간복잡도를 계산할 수 있는 공식을 알게 되었다.

## 마스터 정리, The Master Method

구하고자 하는 경우의 시간복잡도 T(n)이 다음과 같이 표현된다고 하자.

$ T(n) \, = \, O(1) \qquad \qquad \qquad \quad if \; n \, = \, 1 $  
$ \qquad \; \, = \, a \, T(n/b) \, + \, f(n) \qquad otherwise $

조건: $ a \, \geq \, 1, \, b \, \geq \, 1 $ , $f(n)$은 점근적으로 양수 함수값을 가지는 함수

다음과 같은 경우에 대해 시간복잡도 계산이 가능하다!

1. 어떤 상수 $ \epsilon \, > \, 0 \, $에 대해 $ f(n) \in O(n^{\log_b a-\epsilon}) $ 이면, $ T(n) \in O(n^{\log_b a}) $ 이다.

2. 만약 $ f(n) \in O(n^{\log_b a}) $ 이면, $ T(n) \in O(n^{\log_b a} \, \log n) $ 이다.

3. 만약 어떤 상수 $ \epsilon \, > \, 0 $ 에 대해 $ f(n) \in \Omega (n^{\log_b a+\epsilon}) $ 이고, $ c \, < \, 1 $ 과 충분히 큰 $n$에 대해 $af({n \over b}) \leq cf(n) $ 이 성립하면, $ T(n) \in O(f(n)) $ 이다.