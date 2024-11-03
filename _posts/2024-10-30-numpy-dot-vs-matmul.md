---
title: numPy dot과 matmul 차이
search: true
categories: 
  - numPy
tags:
  - numPy
  - numPy.dot
  - numPy.matmul
---
<br />
numPy dot과 matmul 함수 계산 방법의 차이를 알아본다.

# 용어 정리
  * 행렬(matrix): 일반적으로 2차원 구조(행과 열)를 갖는 것
  * 텐서(Tensor): 행렬을 일반화한 것(즉, 3차원, 4차원 등으로 확장한 것)


<br />

# 정의

- numpy.dot(a, b, out=None)
: Dot product of two arrays.


- numpy.matmul(a, b, out=None)
: Matrix product of two arrays.


numpy.dot은 두 배열의 내적곱(dot product)라고 적혀있는 반면에, numpy.matmul은 두 배열의 행렬곱(matrix product)라고 적혀있다.

# 계산 방식 비교
![2024-10-30-numpy-dot-vs-matmul](https://recursive-o.github.io/voice-processing/assets/images/numpy-dot-vs-matmul.png)

<br />

# 예시 코드

```python
 import numpy as np

 A = np.array([
        [[3, 1],
        [3, 3]],
  
        [[1, 1], 
        [3, 2]]])
 B = np.array([
        [[3, 3],
        [3, 3]],

        [[1, 3],
        [2, 1]]])

 print(np.dot(A, B))
        [[[[12 12]
        [ 5 10]]
        
        [[18 18]
        [ 9 12]]]

        [[[ 6  6]
        [ 3  4]]
        
        [[15 15]
        [ 7 11]]]]

 print(np.matmul(A, B))
        [[[12 12]
        [18 18]]
        
        [[ 3  4]
        [ 7 11]]]
```

<br />

# 출처
[정의](https://blog.naver.com/combioai/221356884894)
[코드 예제](https://velog.io/@limdy/numpy-%EC%8B%AC%ED%99%94-1)