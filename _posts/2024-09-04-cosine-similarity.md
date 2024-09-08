---
title:  "방통대 자연언어처리 강의노트1 - 코사인 유사도"
search: true
categories:
  - math
tags:
  - 자연언어처리-강의노트
  - 방통대-자연언어처리
  - gensim-similarities
  - cosine-similarity
last_modified_at: 2024-09-04T23:06:00-05:00
---

2강
BoW에 기반한 단어 표현 방법인 TF-IDF에서 코사인 유사도를 이용하여 문서의 유사도를 구한다

## [코사인 유사도](https://bkshin.tistory.com/entry/NLP-8-문서-유사도-측정-코사인-유사도)란?
![cosine function graph](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcoDff%2FbtqBS6dC19R%2FOMWSZLio9mqXXyGmch7Ack%2Fimg.jpg){: .align-center}
* θ를 두 벡터 간의 사잇각이라고 했을 때 θ=0이면, cosθ = 1.
  코사인 유사도가 1이면 두 벡터는 완전히 동일한 벡터.
  마찬가지로 두 벡터 간의 사잇각이 90도이면, 코사인 유사도가 0이되고 두 벡터는 상관 관계가 없다.
  두 벡터 간의 사잇각이 180도 이면 코사인 유사도는 -1이며, 두 벡터는 완전히 반대인 벡터.
  <br />
  <br />
* [백터의 외적에서는 사인값 사용](https://blockchainstudy.tistory.com/80)
  * 이유: 외적은 얼마나 두 벡터가 수직인지를 확인하는 것이다. (내적은 얼마나 두 벡터가 동일 선상에 있는지(collinear) 확인하는 것이다.)
    sin90의 값이 1 이기 때문에, 이 경우가 외적의 최댓값이 된다. (sinθ는 항상 1보다 같거나 작기 때문에, sinθ의 최댓값은 1이다.)
    두 벡터가 완벽히 수직일 때, 외적 값은 최댓값이 된다.<br />
    내적의 ||a||||b||cosθ로 돌아가보면, θ가 0일 때 cosθ의 값이 1이므로 내적값이 최대가 된다.
    즉, 두 벡터가 동일선상에 있을 때이다.
    따라서 같은 방향을 향하는 두 벡터가 있을 때 내적이 최대가 되며, 외적은 그들이 수직일 때 최대가 된다.
    <br />

* [외적 오른손 법칙](https://assortrock.tistory.com/m/24?category=635936)
<br />
  ![외적 오른손 법칙](https://t1.daumcdn.net/cfile/tistory/2743733B5732EF912A){: .align-center}
