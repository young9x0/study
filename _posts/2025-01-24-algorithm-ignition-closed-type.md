---
title: 알고리즘 점화식과 폐쇄형 증명
search: true
categories: 
  - ignition-closed-type
tags:
  - algorithm

---

## 기본 점화식과 폐쇄형
1. T(n) = T(n-1) + Θ(1), T(1)=Θ(1) → Θ(n)
2. T(n) = T(n-1) + Θ(n), T(1)=Θ(1) → Θ(n^2)
3. T(n) = T(n/2) + Θ(1), T(1)=Θ(1) → Θ(logn)
4. T(n) = T(n/2) + Θ(n), T(1)=Θ(1) → Θ(n)
5. T(n) = 2T(n/2) + Θ(1), T(1)=Θ(1) → Θ(n)
6. T(n) = 2T(n/2) + Θ(n), T(1)=Θ(1) → Θ(nlogn)
   <br />

## 증명
5, 6번 점화식을 풀어 폐쇄형을 구하는 과정은 다음과 같다.
<br />

![5,6번 증명]({{site.url}}{{site.baseurl}}/assets/images/proof-of-closed-type-5-to-6.jpeg)

## 참고 문서
[1. 3 알고리즘의 설계](https://3catpapa.tistory.com/29)