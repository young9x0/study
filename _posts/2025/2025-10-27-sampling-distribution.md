---
title: 표본분포 sampling distribution
search: true
categories:
- statistics
tags:
- sampling distribution
- chi-squared distribution
- F distribution
---

- 일반적으로 모집단 전체를 조사하는 것이 불필요하거나 불가능하여 모집단에서 표본을 추출하여 추론하게 된다.
- 모집단에서 추출한 표본을 바탕으로 모집단의 모수를 추정하는 방법을 찾을 때 모수 추정에 적합한 확률표본의 함수인 통계량을 고려해야 한다.
- 모집단의 평균과 분산을 추정하는 데 적합한 통계량인 표본평균과 표본분산이 대표적인 통계량이다.
- 표본평균과 표본분산은 확률표본 X₁, X₂, … , Xn의 함수로 나타낼 수 있으며 따라서 통계량은 확률변수로 나타내는 또 다른 확률변수이다.
* 통계량의 분포를 표본분포라고 하며, 모수와 통계량의 관계를 보여준다.


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
* 가법성(加法性, Additivity, 덧셈 사상, 가산 사상)
  * 여러 개의 요소 또는 구성 요소가 더해질 때, 그 합이 변하지 않고 일정하게 유지되는 특성을 의미
  * 정의역의 두 함수들에 대한 함수와 항상 각 함수의 값 합계가 서로 같은 값을 반환한다는 함수의 성질
* 카이제곱분포를 그래프로 설명: [카이제곱분포란?](https://math100.tistory.com/44)~



# 표준화된 표본평균의 확률분포
## t분포
- 다음 통계량 t의 분포는 정규분포가 아닌 t분포를 따른다(1908, 고셋 증명함)
- ![t분포 공식](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAYIAAACCCAMAAAB8Uz8PAAAAgVBMVEX///8AAADt7e2/v78+Pj7d3d3Y2Ng5OTn29vbHx8fOzs4aGhry8vKzs7N8fHx1dXVMTEwpKSkgICCcnJwvLy+Ojo4ICAhHR0e4uLjR0dFWVlarq6va2trn5+eKioqYmJhjY2NpaWlTU1MTExMzMzOkpKQcHByLi4teXl6CgoJ5eXlOAlS2AAAEtElEQVR4nO3d6XaqOgAFYDZjUCiTTCoqDj3i+z/gBbR1aHsr5whZrfv7E1pkNSWQ2URRiIiIiIiIiIiIiIiIiO4knDdCdlSe1WocHgWZ7Kg8KyM/MVXZUSEiouGJbOfWZm59rM3aI9aKhiWWK9QmUX0ctUcxk2BgQswS7OftsYfVnE0DGSzAbkIbkeyoPCsXWNTPvj2OZcfkaYkEm0LJJ5XsiDyxP8BODQ8sBeQxgCT0OqaAN24LkKJ0+4jSsxEV4Hd9B5C0SbDAvocYPZ8MnW/kCL7RhCVYiD+AKIHQ7nbNAm3ZYaToeCF9ZrUuE3ysDxWZe+VqMCHFsgmyDQaK5G8mPGuuWtDN2xOz1+DKZHQ+VwSh1oQR0uFi+luJOMwV5VDXSz+cmZtX5hfnskRvhndU7/gy0D8Q0abJzOt66b7LkNkfTJvAsGAohtNP1J7FDG2GomyBvMNlJQ5NkANCXXW5kG7FpxRQ7E71UlNv66J1VWql5Ouij5g9Bce0PayPpXChAbDvzlKypMmInCXql6Fkw+CvxZtmjKZ9hkU7cIPthyL5CzskeFnup5ofVBOjz0j+PF26GYr53DDmRntJHdbH5p1ZiuMhzpexpirFLmI2dCUbpo5oTMBH/wv+MEkwQsiK6BeSZJCu4wglBxc+Z0Ifoo4uppgN8Gd+pCVWQzydYvr6oUOJatOtlWBjTdhpI407i4Okmu3O/ZnF6BZnTvfMDsKre1wl42sbviE9i2Bd/VzYt9iM6pd4waLLx9WH6e1f+mkMH6PvP/XOnuiPYa2ZBic2cFMlFbcuT6qZ9iA222knbjuOm5/vxyL1r6X39oTSXxHtOG4enItc+/Byo/OEE+GonO5+N9Vvhh6rrhMT/5eWpr6+Yq/onUQJQ4n8R96vDLEhjNeHpuqvpmG917vUib6jprrSpMOKNZ57FbPsoc+rFm6br358nGFEQxkF2FRsUctUN7ebMX3O25VInZUhkPI9kEW1m46kHQJNdkyelQG0A9Fp8MhaFnVgY9LMpXbCPZsFkpht17dRbjhrV5rdZF36QTr//pPUF5G7OTMhIiIiIiIiei7mfdhg7s90a90h4JyW/hTGPeZ8C4hoaJzFIpuq+wfvUskkGViMsrqane0xCYZl6FPZUXh2UafFuujxipSL8UrmciVYyZyxx1Vv5Hpbv5GkCffNSyCyxU5VhBsvIn7fZmDucd2hbLLEIl9Zy2Wgs49uUKL9rpmi+pkCtDNMK3DDiEGdSgJTN+okqJrnv/pkgXd6tPOAjLoK2lB7Uezjwu6Cq4QPYJe+14E0HHcsUAtlAa85MtNOC43QX1A94G1nJ2elv9d/1qcNI8ANI3rmvBxKvJ7awzbet+0wtu0vRYVSEawT9UkYinrc6q+Wnldkdzfbpn1QTGArGTdn71uJcVsi5xc7XsbHDSM0bB0x5RKlfTNxzPen1ntJUFeE2gXyl3Uw0jmHpW/1/W4W99IuXgJTP64SPsIyB/Oh/tlJ/RqI8mKRteJQtqETTdfMhgagltgq9tWSpupbcnAxxmHskOxi8GZL5PgANwCXKwIs1nukEgl742RbbLk/gWzsByIiIiIiIiIiIiIiIqLH+A/Z5UIB7GneRwAAAABJRU5ErkJggg==)
- 표본의 크기가 30보다 적은 경우, 모분산을 모를 경우에 확률표본에서 얻어진 표본분산을 구해 이를 모분산 대신 사용할 때 정규분포가 아닌 t분포를 따른다.


# 표본분산비의 확률분포
## F분포
-  두 집단의 분산을 비교하고 싶을 때 각각의 분산은 카이제곱을 따르는데, 두 분산의 비율이 F-분포를 따른다.


* 자유도:
- 예시: 5개의 숫자 평균이 3이라고 할 때, 5개 중 4개의 숫자는 마음대로 고를 수 있지만, 마지막 한 개의 숫자는 정해져 있다. 1, 3, 5, 7 숫자를 선택했다면 평균 3이 되기 위해서 마지막 숫자는 반드시 -1이 되어야 한다. 이때 숫자 4개는 제가 마음대로 골랐기 때문에 이 경우에 자유도는 4가 된다.

# 참고자료
- [통계학의개념및제문제 - 한국방송통신대학교 출판문화원](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920031618&condLscValue=001&condYr=&condSmst=)
- [카이제곱분포의 가법성](https://datanovice.tistory.com/entry/%EC%B9%B4%EC%9D%B4%EC%A0%9C%EA%B3%B1-%EB%B6%84%ED%8F%AC-Chi-squared-distribution)
- [카이제곱분포 증명](https://blog.naver.com/mykepzzang/220852102307)
- [t분포 증명](https://blog.naver.com/mykepzzang/220853827288)