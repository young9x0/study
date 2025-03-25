---
title: 공공데이터 분석 - 전국 축산농가 수와 지하수 오염 현황 데이터 전국 지도로 그리기
search: true
categories:
  - data_analysis
tags:
  - public_data_analysis
  - call_taxi_for_disabled_data
  
  - seoul_disabled_people_data
---
전국 축산농가 수와 지하수 오염 현황 데이터를 분석해 보았습니다.

전국 축산농가 수 현황을 분석한 결과...  

![animal-farm-total-excel-data.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/animal-farm/animal-farm-total-excel-data.png)
* 축산농가 수는 2021년 기준 전체 176,393 호입니다.
* 경북(32,655), 전남(26,333), 경남(22,648) 순으로 많습니다.
* 그에 비해 서울(44), 광주(298), 대전(428) 순으로 적습니다.
* 경북과 서울의 축산농가 수는 700배 이상의 차이를 보입니다.
* 지역별로 축산농가가 불균형하게 분포하고 있음을 알 수 있으며 특히 도시로부터 떨어진 지방에 주로 분포하고 있음을 알 수 있습니다.

![total-animal-farm-2021.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/animal-farm/total-animal-farm-2021.png)




전국 지하수 오염예측도/취약성도 지도는
농림축산식품 공공데이터 포털에서 shp파일 데이터를 카카오지도 위에 입힌 결과입니다.


![water-pollution-2023.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/animal-farm/water-pollution-2023.png)


![water-pollution-expect-2023.png]({{site.url}}{{site.baseurl}}/assets/images/data-analysis-with-python/animal-farm/water-pollution-expect-2023.png)


서울보다는 축산 농가가 위치한 지방 중심으로 지하수가 오염되어 있는 모습을 확인할 수 있습니다.





출처:
1. 농가현황
   가축위생방역지원본부에서 보유하고 있는 전국 축산농가정보를 운영상태와 시·도 별로 구분·산출하여 데이터화한 자료

2. 한국농어촌공사_지하수 오염예측도
   농어촌지하수관리조사 결과 분석된 지하수 오염예측도(DRASTIC INDEX모델+단위면적당오염발생부하량)정보

3. 한국농어촌공사_지하수 오염취약성도
   농어촌지하수관리조사 결과 분석된 지하수 오염취약성도(DRASTIC INDEX모델) 정보