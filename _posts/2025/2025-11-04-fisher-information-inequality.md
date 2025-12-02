---
title: 피셔의 정보량 부등식
search: true
categories:
- statistics
tags:
- Fisher's Information Inequality
- Cramér-Rao Lower Bound
---
- **피셔의 정보량 부등식(Fisher's Information Inequality)**은 **크라메르-라오 하한(Cramér-Rao Lower Bound, CRLB)**이라고도 불리며, 모수(θ)의 임의의 불편 추정량(unbiased estimator, θ^)가 가질 수 있는 최소 분산(variance)의 이론적인 하한을 규정하는 부등식이다.
> Var(θ^)≥1/I(θ)
- Var(𝜃^): 추정량의 흔들림 (분산)
- I(θ): 피셔의 정보량
- 아무리 똑똑한 추정법을 써도, 그 분산(오차)은 피셔 정보량의 역수보다 작아질 수 없다.

## 예시
- 안개 낀 곳에서 무언가를 본다고 해보자.
- 안개가 짙을수록 정보량이 작고, 물체를 구별하기 어렵다.
- 안개가 옅을수록 정보량이 커지고, 더 정확히 볼 수 있다.
- 이를 피셔의 정보량으로 비유해보면,
  - 피셔 정보량이 많을수록 → 분산이 작아짐 → 정확한 추정 가능
  - 피셔 정보량이 적을수록 → 분산이 커짐 → 추정이 흔들림
   
## UMVUE와 피셔의 정보량 부등식의 관계
- 추정의 정확도에는 정보량에 따라 정해진 한계가 있다는 피셔의 정보량 부등식에 따라 그 한계 안에서 다음 두 가지 조건을 만족할 때, 가장 정확하고 공평한 추정량이 UMVUE이다.  
1. 불편(Unbiased): 추정의 평균이 모수와 같다.
2. 최소분산(Minimum Variance): 가능한 모든 불편추정량 중에서 분산이 가장 작다.
- 이 조건을 모든 θ에서 균일하게 만족하면 **균일최소분산불편추정량 (UMVUE)**이다.
  
  

# 참고자료
- [통계학의개념및제문제 - 한국방송통신대학교 출판문화원](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920031618&condLscValue=001&condYr=&condSmst=)
- [피셔의 정보량 부등식과 UMVUE의 예시](https://chatgpt.com/s/t_690965bb9cac8191bee7741367bb7828)
