---
title: 점추정량의 비교 - 카이제곱분포의 분산
search: true
mathjax: true
categories:
- statistics
tags:
- chi-squared variance
---
카이제곱분포 $$ \chi^2(k) $$ 의 분산을 구해본다.

---

# 💡 핵심 개념

카이제곱 분포는 **표준정규분포를 따르는 값의 제곱을 더한 것**.

예를 들어

$$
Z_1, Z_2, \cdots, Z_k \sim N(0,1)
$$

라면

$$
\chi^2(k) = Z_1^2 + Z_2^2 + \cdots + Z_k^2
$$
  

# ✨ Step 1 : 먼저 $$Z^2$$ 의 평균과 분산을 구하기

$$
E(Z) = 0,\quad \operatorname{Var}(Z) = 1
$$

- 정규분포의 성질 중 하나:

$$
E(Z^2) = \operatorname{Var}(Z) + (E(Z))^2 = 1 + 0 = 1
$$

-  $$Z^4$$ 의 기댓값 구하기 위해 표준정규분포의 확률밀도함수를 이용한다.

$$
f(z)=\frac{1}{\sqrt{2\pi}} e^{-z^2/2}
$$

- 따라서

$$
E(Z^4)=\int_{-\infty}^{\infty} z^4 f(z), dz
= \int_{-\infty}^{\infty} z^4 \frac{1}{\sqrt{2\pi}} e^{-z^2/2}dz
$$

- 이 적분의 결과가 **3**

$$
\operatorname{Var}(Z^2)
= E(Z^4) - [E(Z^2)]^2
= 3 - 1^2 = 2
$$

- 표준정규의 제곱 $$Z^2$$ 는 **평균 1**, **분산 2**
  

# ✨ Step 2 : k개 더하면?

- 카이제곱 정의:

$$
\chi^2(k) = \sum_{i=1}^{k} Z_i^2
$$

- 독립이므로 평균은

$$
E(\chi^2(k)) = \sum_{i=1}^{k} E(Z_i^2) = k \cdot 1 = k
$$

- 분산은 

$$
\operatorname{Var}(\chi^2(k)) = \sum_{i=1}^{k} \operatorname{Var}(Z_i^2)
= k \cdot 2 = 2k
$$

  

# 🎯 결론

$$
\boxed{\operatorname{Var}(\chi^2(k)) = 2k}
$$

  
  
# 참고자료
- [통계학의개념및제문제 - 한국방송통신대학교 출판문화원](https://press.knou.ac.kr/goods/textBookView.do?condCmdtCode=9788920031618&condLscValue=001&condYr=&condSmst=)
- [chatGPT 답변](https://chatgpt.com/s/t_692648a7f584819183bebaadd0cc05a5)