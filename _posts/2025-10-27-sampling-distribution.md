---
title: 표본분포
search: true
categories:
- statistics
tags:
- sampling distribution
- chi-squared distribution
- F distribution
---
![표본분포 표]({{site.url}}{{site.baseurl}}/assets/images/statistics/sampling-distribution.jpg){: .align-center}

# 합과 평균의 확률분포
## 적률생성함수의 성질
- 적률생성함수의 유일성: 서로 다른 확률분포는 서로 다른 적률생성함수를 가진다는 성질이다. 
- 반대로, 두 확률변수의 적률생성함수가 동일하다면, 두 확률변수는 같은 확률분포를 따른다는 의미이기도 하다. 
- 이 성질을 통해 특정 확률변수의 적률생성함수를 알면 그 분포가 무엇인지 파악하는 데 사용할 수 있다.

# 표본분산의 확률분포
## 카이제곱분포
- 표준정규분포를 따르는 모집단에서 k 개의 표본을 추출하였을 때, 제곱의 합과 관련한 분포
- 감마분포의 특수한 형태
- 카이제곱 분포의 가법성: 여러 개의 요소 또는 구성 요소가 더해질 때, 그 합이 변하지 않고 일정하게 유지되는 특성을 의미


# 표준화된 표본평균의 확률분포
## t분포
-  표본의 크기가 30보다 적은 경우, 모분산을 모를 경우에 확률표본에서 얻어진 표본분산을 구해 이를 모분산 대신 사용할 때 정규분포가 아닌  t분포를 따른다.

# 표본분산비의 확률분포
## F분포
-  두 집단의 분산을 비교하고 싶을 때 각각의 분산은 카이제곱을 따르는데, 두 분산의 비율이 F-분포를 따른다.


* 자유도:
- 예시: 5개의 숫자 평균이 3이라고 할 때, 5개 중 4개의 숫자는 마음대로 고를 수 있지만, 마지막 한 개의 숫자는 정해져 있다. 1, 3, 5, 7 숫자를 선택했다면 평균 3이 되기 위해서 마지막 숫자는 반드시 -1이 되어야 한다. 이때 숫자 4개는 제가 마음대로 골랐기 때문에 이 경우에 자유도는 4가 된다.

# 참고자료
- [통계학의개념및제문제 - 한국방송통신대학교 출판문화원](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920031618&condLscValue=001&condYr=&condSmst=)
- [카이제곱분포의 가법성](https://datanovice.tistory.com/entry/%EC%B9%B4%EC%9D%B4%EC%A0%9C%EA%B3%B1-%EB%B6%84%ED%8F%AC-Chi-squared-distribution)
- [카이제곱분포 증명](https://blog.naver.com/mykepzzang/220852102307)