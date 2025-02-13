---
title: 보이어 무어 Boyer-Moore 알고리즘 
search: true
categories:
  - algorithm
tags:
  - Boyer-Moore
  - string_algorithm
---
<br />
보이어무어는 문자열 매칭이 마지막에 틀릴 가능성이 높다는 특징을 이용한다.  
문자열의 가장 뒷부분을 비교하고, 다르면 일정 길이만큼 이동하며 비교를 계속한다.  
대부분의 워드프로세스, RDB, JAVA언어 검색기능에서 사용된다.  








## 1. 불일치 문자 방법 bad character method
 여기서 'bad character'란 본문의 문자열 Text와 pattern 문자 중 불일치하는 문자를 말한다.  

|         |   | 0 | 1 | 2 | 3 | 4 | 5 | 6                                   | 7 | 8 | 9 | 10| 11| 12| 13|
|---------|---|---|---|---|---|---|---|-------------------------------------|---|---|---|---|---|---|---|
| Text    | = | a | b | a | b | a | b | <span style = "color:red">c</span>  | a | b | a | b | c | a | a |
| Pattern | = | a | b | a | b | <span style = "color:red">c</span> | a | <span style = "color:blue">b</span> |   |   |   |   |   |   |   |

위의 예시를 보면 6번 index의 Text 문자는 c, pattern 문자는 b이므로 불일치한다. 여기서 불일치 문자는 Text 문자를 기준으로 봤을 때 c 이다.
불일치하다면 pattern 문자에서 불일치 문자 c와 일치하는 index를 찾는다. 4번 index이므로 2만큼 이동한다.  

|         |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11| 12| 13|
|---------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Text    | = | a | b | a | b | a | b | <span style = "color:red">c</span> | a | b | a | b | c | a | a |
| Pattern | = |   |   | a | b | a | b | <span style = "color:red">c</span> | a | <span style = "color:blue">b</span> |   |   |   |   |   |

일치한다면 pattern 문자의 길이만큼 이동한다. 여기서는 7이다.   

이러한 경우의 수를 skip table에 미리 저장해서 계산한다. pattern 문자 'ababcab'의 경우 skip table을 만들면 다음과 같다.

|   |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| Pattern | = | **a** | b | **a** | b | c | **a** | b |

먼저 a를 살펴보자. a 가장 오른쪽 자리로 가기 위해서는 a가 현재 있는 index 0, 2, 5 중 가장 큰 index 값을 찾는다. 5번이 가장 큰 값이므로 현재 pattern의 마지막 index 6번 자리로 가기 위해서는 6에서 5를 뺀 값 1을 저장한다.  


| a | b | c |
|---|---|---|
| 1 |   |   |

마찬가지 방식으로 계산해 나머지 문자열의 값을 채우면 skip table은 다음과 같다. 

| a | b | c |
|---|---|---|
| 1 | 0 | 2 |

  
## 2. 일치 접미부 방법 good suffix method
 불일치 문자 방법이 불가능한 경우가 있기 때문에 두 번째 방법인 일치 접미부 방법를 함께 사용한다.   
불가능한 경우는 예를 들어 다음과 같다. 1번 index에서 a와 c 문자 사이에 불일치가 발생했다.  


|         |   | 0 | 1                                   | 2                                  | 3 | 4 | 5 | 6 |
|---------|---|---|-------------------------------------|------------------------------------|---|---|---|---|
| Text    | = | c | <span style = "color:red">a</span>  | a                                  | c | a | c | c |
| Pattern | = | a | <span style = "color:blue">c</span> | <span style = "color:red">a</span> | c |   |   |   |


불일치 문자 a의 skip table을 살펴보면 1이다.  

| a | c |
|---|---|
| 1 | 0 |
  

그러나 오른쪽으로 1을 간다면 여전히 불일치하게 된다. 왜냐하면 skip table은 오른쪽 마지막 자리를 기준으로 계산되었기 때문이다.


|         |   | 0 | 1                                   | 2                                  | 3 | 4 | 5 | 6 |
|---------|---|---|-------------------------------------|------------------------------------|---|---|---|---|
| Text    | = | c | <span style = "color:red">a</span>  | a                                  | c | a | c | c |
| Pattern | = |   | a | <span style = "color:blue">c</span> | <span style = "color:red">a</span> | c |      |   |

이럴 때 일치 접미부 방법이 필요하다. 불일치가 발생한 1번 index를 기준으로 그 오른쪽 index 2, 3번의 경우는 일치했음을 알 수 있다. 따라서 text 문자 기준으로 index 2, 3번 문자인 a, c가 일치 접미부이다.


|         |   | 0 | 1                                    | 2                                    | 3                                    | 4 | 5 | 6 |
|---------|---|---|--------------------------------------|--------------------------------------|--------------------------------------|---|---|---|
| Text    | = | c | <span style = "color:red">a</span>   | <span style = "color:green">a</span> | <span style = "color:green">c</span> | a | c | c |
| Pattern | = | <span style = "color:green">a</span> | <span style = "color:green">c</span> | a                                    | c |      |   |

pattern 문자에서 일치 접미부 a, c와 일치하는 자리는 index 0, 1이다. 가장 작은 index 0을 기준으로 text 문자의 일치 접미부가 시작하는 index 2로 이동한다.

|         |   | 0 | 1                                  | 2                                    | 3                                    | 4 | 5 | 6 |
|---------|---|---|------------------------------------|--------------------------------------|--------------------------------------|---|---|---|
| Text    | = | c | <span style = "color:red">a</span> | <span style = "color:green">a</span> | <span style = "color:green">c</span> | a | c | c |
| Pattern | = |  |                                    | <span style = "color:green">a</span> | <span style = "color:green">c</span> | a                                    | c |


만약 일치 접미부와 동일한 문자를 pattern에서 찾을 수 없다면 일치 접미부를 왼쪽부터 한 문자씩 줄여가며 반복해서 조사한다.  
index 1에서 불일치가 발생했고, 일치 접미사는 a, b, c, a인 상황이다. index 1을 기준으로 왼쪽의 pattern 문자 c, a에는 일치 접미사와 동일한 문자열을 발견할 수 없다.  

|         |   | 0                                     | 1                                     | 2                                    | 3                                    | 4                                    | 5 | 6 | 7 | 8 | 9 |
|---------|---|---------------------------------------|---------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--|---|---|---|---|
| Text    | = | b                                     | <span style = "color:red">c</span>    | <span style = "color:green">a</span> | <span style = "color:green">b</span> | <span style = "color:green">c</span> | <span style = "color:green">a</span> | a | b | c | a |
| Pattern | = | <span style = "color:orange">c</span> | <span style = "color:orange">a</span> | a                                    | b                                    | c                                    | a |



일치 접미사를 b, c, a로 줄이고 다시 찾아본다. 이 과정을 반복한다. 


|         |   | 0 | 1                                  | 2 | 3                                    | 4                                    | 5                                    | 6 | 7 | 8 | 9 |
|---------|---|---|------------------------------------|---|--------------------------------------|--------------------------------------|--------------------------------------|---|---|---|---|
| Text    | = | b | <span style = "color:red">c</span> | a | <span style = "color:green">b</span> | <span style = "color:green">c</span> | <span style = "color:green">a</span> | a | b | c | a |
| Pattern | = | <span style = "color:orange">c</span> | <span style = "color:orange">a</span> | a                                    | b                                    | c                                    | a                                    |


일치 접미사가 c, a일 때 pattern 문자의 index 0, 1인 c, a 와 일치한다.  일치 접미사의 index 위치 3으로 옮긴다.  


|         |   | 0 | 1                                  | 2 | 3 | 4                                    | 5                                     | 6 | 7 | 8 | 9 |
|---------|---|---|------------------------------------|---|---|--------------------------------------|---------------------------------------|---|---|---|---|
| Text    | = | b | <span style = "color:red">c</span> | a | b | <span style = "color:green">c</span> | <span style = "color:green">a</span>  | a | b | c | a |
| Pattern | = |  | |          |   |                                     <span style = "color:orange">c</span> | <span style = "color:orange">a</span> | a | b | c | a |

만약 일치 접미사를 모두 줄여도 pattern에서 동일한 문자를 발견할 수 없다면 pattern의 길이만큼 오른쪽으로 이동한다.
  
<br />
<br />
<br />

## 참고 자료
- [[문자열 매칭] 보이어무어(Boyer-Moore) - Good Suffix Heuristics]( https://jie0025.tistory.com/538)
- 방통대 알고리즘 교재 328-337쪽