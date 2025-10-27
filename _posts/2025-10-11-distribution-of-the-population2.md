---
title: 모집단의 분포 개념 정리 2
search: true
categories:
- statistics
tags:
- continuous distribution
---



## 모집단의 확률분포 probabiliy distribution⠀
### 연속형 분포 continuous distribution
![확률분포 표]({{site.url}}{{site.baseurl}}/assets/images/statistics/probability-distribution.jpg){: .align-center}
  

#### 연속 균등분포 continuous uniform
* 특정 구간에서 확률밀도가 일정한 분포. 
* 연속형 확률분포에서는 “끝점 포함 여부”는 확률에 영향을 주지 않는다.  연속형 확률에서 어떤 한 점에서의 확률은 0이기 때문
  - P(a≤X≤b)=P(a<X<b)
  - P(X=a) = 0, P(X=b) = 0

#### 지수분포 exponential
* 단위시간(t)당 평균 발생횟수가 λ일 때(포아송분포  Poisson(λt)를 따를 때), 사건이 처음 발생할 때까지 걸리는 시간이 T이하일 확률에 대한 분포
* 사건이 처음 발생할 때까지 걸리는 시간이 T 이하일 확률은 지수분포의 누적분포함수인 F(T)로 나타낸다.
* 포아송분포란 일정 구간 내에서 성공횟수의 확률분포이라면 지수분포는 한 사건이 발생한 이후 다음 사건이 발생할 때까지의 시간에 대한 확률 밀도이다.
* 지수분포의 망각성: X~Exp( λ)일 때, 처음 a시간 동안 사건이 발생하지 않았다면, 사건 발생까지 b시간을 더 기다릴 확률은 P(X≥a+b | X≥a)= P(X≥b)이다.
* 예를 들어,
  * 길냥이를 3일(b) 이후 만났을 확률이 20%라면, 5일(a) 이전에 못만났을 확률과 상관없이 5일 이후에서 다시 3일이 지났을 때(즉, 8일이 지나서) 만났을 확률은 20%이다.
  * P(X≥5+3 | X≥5)= P(X≥3) = 20%
* 참고자료: [https://hsm-edu.tistory.com/1552](https://hsm-edu.tistory.com/1552). 

#### 감마분포 gamma
* 어떤 사건의 발생이 포아송분포  Poisson(λt)를 따를 때 그 사건이 a번째로 발생할 때까지 대기시간의 분포, 즉, 총 α번의 사건이 발생할 때까지 걸린 시간에 대한 확률분포
* 정규분포로 설명할 수 없는 부분을 보완하기 위해 나온 확률 분포
* 참고자료: https://blog.naver.com/mykepzzang/220842759639  

#### 정규분포 Normal
* 평균을 중심으로 좌우대칭인 종 모양(bell-shape)의 분포
* 표준정규분포(Standard Normal Distribution): 평균이 0이고 표준편차가 1인 정규분포
* 정규분포 그리기: https://homepage.divms.uiowa.edu/~mbognar/applets/normal-vi.html

# 참고자료
- [통계학의개념및제문제 - 한국방송통신대학교 출판문화원](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920031618&condLscValue=001&condYr=&condSmst=)
- [\[수리 통계학\] 정리 노트](https://gagadi.tistory.com/49?category=950402)