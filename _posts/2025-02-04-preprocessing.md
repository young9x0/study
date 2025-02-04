---
title: 데이터 사전 처리 data preprocessing
search: true
categories:
  - data_preprocessing
tags:
  - one_hot_encoding
  - feature_scaling
---
<br />

## 원 핫 인코딩 one-hot encoding
- 카테고리를 나타내는 범주형 데이터를 컴퓨터가 인식 가능한 입력값으로 변환할 필요가 있을 때 숫자 0 또는 1로 표현되는 더미 변수를 사용한다.
  - 여기서 0과 1은 수의 크고 작음을 나타내지 않고, 어떤 특성이 있는지(1) 없는지(0) 여부를 표시한다
- 원 핫 인코딩 one-hot encoding은 범주형 데이터를 컴퓨터가 인식할 수 있도록 숫자 0과 1로만 구성되는 원핫벡터로 변환하는 작업이다.
- sklearn LabelEncoder와 OnehotEncoder

## 피처 스케일링 feature scaling
- 각 변수(데이터프레임의 열)에 들어 있는 숫자 데이터의 상대적 크기 차이 때문에 머신러닝 분석 결과가 달라질 수 있다.
  - 예를 들어 A변수는 0-1000 범위의 값이고, B는 0-1 범위의 값을 갖는다면, 상대적으로 큰 숫자값을 갖는 A 변수가 결과에 더 큰 영향을 미친다.
- 피처 스케일링은 이와 같은 문제를 방지하기 위해 숫자 데이터들의 상대적인 크기 차이를 제거하기 위해 데이터의 특성들이 가지는 값의 범위를 일정한 수준으로 맞추는 전처리 과정이다.
- 대표적인 방법
  - min-max scaling 
    - 각 열(변수)의 데이터 중에서 해당 열의 최솟값을 뺀 값을 분자로, 해당 열의 최대값과 최소값의 차를 분모로 하는 수를 계산한다.
    - 정규화하면 0과 1 사이 값이 된다.
    - sklearn MinMaxScaler 
  - standard scaling
    - 열의 각 데이터에서 평균을 빼고 다시 표준편차로 나눈다.
    - 특히 데이터가 정규분포를 가정하는 경우 의미가 있다.
    - sklearn StandardScaler 

# 참고 자료
[파이썬 머신러닝 판다스 데이터 분석](https://github.com/tsdata/pandas-data-analysis) 292, 296쪽