---
title: pandas 함수 매핑 시 map vs apply 
search: true
categories:
  - pandas
tags:
  - function-mapping
  - apply
  - map
---
pandas 함수 매핑 시 map와 apply 메서드의 차이를 Series 객체와 DataFrame 객체인 경우 두 가지로 나누어 살펴본다.
<br />

### Series 객체의 경우
  - map 함수는 함수뿐만 아니라 딕셔너리를 이용해 매핑할 수 있으며, 이는 lambda 함수를 이용한 매핑보다 더 간결하고 속도도 빠르다. 그래서 시리즈에서는 map 함수를 주로 매핑에 사용한다.
<br />

```python
import pandas as pd

ab_strs = pd.Series(list('ababaabb'))
ab_mapper = {'a':0, 'b':1}

ab_strs.map(ab_mapper)
+-+---------+
|0|0        |
|1|1        |
|2|0        |
|3|1        |
|4|0        |
|5|0        |
|6|1        |
|7|1        |
+-+---------+

# 위의 결과와 같다
ab_strs.apply(lambda x: ab_mapper[x])
```

<br />

### DataFrame 객체의 경우
  - apply 메소드는 데이터프레임의 행이나 열에 함수를 적용하고, map과 다르게 모든 원소에 직접 적용되지 않는다.
    - 참고로 이전 버전의 applymap 메소드가 공식적으로 더 이상 지원되지 않아 현재 map으로 통합되었다.

<br />

```python
import pandas as pd
# 데이터 프레임 선언
df = pd.DataFrame({"A":["2000원","3000원","4000원","5000원"],
                   "B":["1000원","2000원","3000원","4000원"],
                   "C":["1000원","2000원","3000원","4000원"]})

df_map=df.map(lambda x: x[:3])
df_map

# 모든 원소에 슬라이스가 적용되어 뒤의 '0원'이 삭제되었다
+-+---+---+---+
| |A  |B  |C  |
+-+---+---+---+
|0|200|100|100|
|1|300|200|200|
|2|400|300|300|
|3|500|400|400|
+-+---+---+---+


df_apply=df.apply(lambda x: x[:3])
df_apply

# 행 단위로 적용하므로 마지막 행에 슬라이스가 적용되어 3행이 삭제되었다.
+-+----+----+----+
| |A   |B   |C   |
+-+----+----+----+
|0|200원|100원|100원|
|1|300원|200원|200원|
|2|400원|300원|300원|
+-+----+----+----+
```

<br />
<br />

# 참고 자료
[시리즈에 apply 대신 map 함수로 매핑하는 이유](https://kimpanda.tistory.com/124)
[apply를 무분별하게 쓰면 안되는 이유](https://kimpanda.tistory.com/199)
[apply(), map(), applymap() 함수의 적용 대상과 차이점](https://m.blog.naver.com/youji4ever/222292901767)
[파이썬 머신러닝 판다스 데이터 분석](https://github.com/tsdata/pandas-data-analysis) 355쪽