---
title: 점추정의 비교 - 평균제곱오차 증명
search: true
categories:
- statistics
tags:
- mean-square error
- MSE
- 평균제곱오차
---
 통계량 T가 θ의 추정통계량일 때 통계량 T에 대한 평균제곱오차는 다음과 같이 정의할 수 있다.

> MSE(T) = E[(T−θ)^2]

왜 위의 식을 증명할 때 다음 식에서 중간항이 사라지는가?  

> E[T−E(T)]^2+2E[(T−E(T))[E(T)−θ]]+[E(T)−θ]^2

다음 중간 항에서 **E[T−E(T)]** 부분이 0이기 때문이다.
> 2E[T−E(T)][E(T)−θ]]

그렇다면 왜 다음 첫번째 항은 사라지지 않는가?
> E[T−E(T)]^2

첫번째 항은 엄밀히 표현하면 '평균의 제곱'이 아니라 '제곱의 평균'이기 때문이다.
> E[(T−E(T))^2]

예를 들어 T−E(T)가 −1 또는 +1로 나올 확률이 반반이라면,
> E[T−E(T)] = {(-1) + 1}/2 = 0
> E[(T−E(T))^2] = {(−1)^2+(1)^2}/2 = 1

즉, **흔들림(변동성)**이 존재하기 때문에 E[(T−E(T))^2]의 값은 0이 아니다.
  
따라서 다음과 같이 표현할 수 있다.
> MSE(T) = E[(T−θ)^2] = Var(T) + bias(T)^2

* 이때  θ의 추정량 T의 편의(bias)는 다음과 같다.
> bias(T) = E(T) − θ

[//]: # (![표본분포 표]&#40;{{site.url}}{{site.baseurl}}/assets/images/statistics/sampling-distribution.jpg&#41;{: .align-center})


# 참고자료
- [통계학의개념및제문제 - 한국방송통신대학교 출판문화원](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920031618&condLscValue=001&condYr=&condSmst=)
- [chatgpt answer](https://chatgpt.com/s/t_69040c5458e48191849dd8f95fd5c28a)
