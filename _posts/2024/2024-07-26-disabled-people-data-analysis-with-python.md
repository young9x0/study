---
title: 공공데이터 분석 - 서울시 자치구별 장애인콜택시 이용빈도수 분석하기
search: true
categories:
  - data analysis
tags:
  - public data analysis
  - call taxi for disabled data
---
장애인콜택시 이용 정보 공공데이터를 이용해 서울시 자치구별 장애인콜택시 이용 빈도수를 분석해 보았습니다.

기준 데이터는 서울특별시에서 제공하는 서울시 장애인 현황 (장애유형별) 통계와 장애인콜택시 이용 정보 공공데이터입니다.  

분석 결과...

1. 서울시 자치구별 장애인 현황을 보면 강서구와 노원구에 가장 많은 인구가 거주하고 있습니다.  

![disabled-people-count-at-2023.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/call-taxi-for-disabled/disabled-people-count-at-2023.png)

<br />
<br />

2. 올해 6월 한달 간 장애인콜택시 이용 정보를 분석해보면 출발지와 목적지 빈도수를 더했을 때 노원구, 강서구, 서대문구 순으로 이용빈도가 높습니다.
* 출발지 기준으로는 노원구, 강서구, 강남구/ 목적지 기준으로는 영등포구, 노원구, 서대문구 순입니다.
  <br />

![start-count-2024-06.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/call-taxi-for-disabled/start-count-2024-06.png)
<br />


![arrive-count-2024-06.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/call-taxi-for-disabled/arrive-count-2024-06.png)
<br />

  

![start-and-arrive-count-2024-06.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/call-taxi-for-disabled/start-and-arrive-count-2024-06.png)

<br />
<br />

3. 
- 서울시 자치구별 장애인구 백명 당 장애인 콜택시 이용빈도 수를 비교해보면 노원구, 영등포구, 강서구 순으로 많습니다.
- 거주 인구가 많은 노원구와 강서구는 인구수와 콜택시 이용수가 비례합니다.
- 영등포의 경우 거주인구수는 총 25개 자치구 중 11위이지만 인구수 대비 콜택시 이용자수가 상대적으로 많습니다.


![by-per-hundred-2024-06.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/call-taxi-for-disabled/by-per-hundred-2024-06.png)

<br />

[관련 코드](https://github.com/young9x0/data-with-python/blob/main/disabled_call_taxi/disabled_call_taxi.ipynb)

<br />
<br />

출처:
- 서울시 장애인 현황 (장애유형별) 통계: https://data.seoul.go.kr/dataList/18/S/2/datasetView.do
- 장애인콜시스템(장애인콜택시 이용 정보): https://data.seoul.go.kr/dataList/OA-15558/A/1/datasetView.do

