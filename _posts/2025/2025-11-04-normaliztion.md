---
title: 정규화 예시
search: true
categories:
  - database
tags:
  - normalization
---
1정규형에서 5정규형까지 예시를 들면 다음과 같다.
<br/>
<br/>

## 1정규형(1NF): 원자값으로 구성
### before

| id | email                             |
|----|-----------------------------------|
| 1  | test1@gamil.com; test2@gamil.com; |

- 테이블 내의 속성값을 원자값으로 변경

### after

| id | email           |
|---|-----------------|
| 1 | test1@gamil.com |
| 1 | test2@gamil.com |


<br/>
<br/>

## 2정규형(2NF): 부분 함수 종속 제거
### before

| name | service  | price   | period  |
|------|----------|---------|---------|
| john | health   | 7,0000  | 1 month |
| john | swimming | 10,0000 | 2 month |
| lily | swimming | 10,0000 | 2 month |

- 부분함수 종속을 제거해 완전함수 종속 관계로 바꾼다.
- 위 예시의 영향 관계는 다음과 같다.
  -  name, service -> period
  -  service -> price
- 부분 관계인 'service -> price'를 별도의 테이블로 둔다.

### after

| name | service  | period  |
|------|----------|---------|
| john | health   | 1 month |
| john | swimming | 2 month |
| lily | swimming | 2 month |

| service  | price   |
|----------|---------|
| health   | 7,0000  |
| swimming | 10,0000 |

<br/>
<br/>

## 3정규형(3NF): 이행함수 종속 제거
### before

| number | name  | price  | publisher | homepage  |
|--------|-------|--------|-----------|-----------|
| 1      | host  | 2,0000 | a         | www.a.com |
| 2      | smile | 1,0000 | b         | www.b.kr  |
| 3      | happy | 1,5000 | b         | www.b.kr  |

- number -> publisher, publisher -> homepage 이므로, 이행함수 종속 관계이다.
- number와 homepage는 영향을 주는 관계가 아니므로 테이블을 number -> publisher, publisher -> homepage 둘로 분리한다.
### after

| number | name  | price  | publisher |
|--------|-------|--------|-----------|
| 1      | host  | 2,0000 | a         |
| 2      | smile | 1,0000 | b         |
| 3      | happy | 1,5000 | b         |


| publisher | homepage  |
|-----------|-----------|
| a         | www.a.com |
| b         | www.b.kr  |

<br/><br/>

## 보이스-코드 정규형(BCNF): 결정자 후보키가 아닌 함수 종속 제거
### before

| id    | subject  | professor |
|-------|----------|-----------|
| 20201 | database | jane      |
| 20006 | database | jane      |
| 20006 | c        | mike      |

-  id, subject -> professor, professor -> subject 일 때 professor가 결정자임에도 후보키가 아니다.
- prfessor가 후보키 역할을 하도록 테이블을 분리한다.

### after

| id    | professor |
|-------|-----------|
| 20201 | jane      |
| 20006 | jane      |
| 20006 | mike      |



| professor | professor |
|:---------:|-----------|
|   jane    | database  |
|   mike    | mike      |

<br/><br/>

## 4정규형(4NF): 다치 종속 제거
### before

| name | certification | language |
|------|---------------|----------|
| jane | os            | c        |
| sam  | security      | java     |
| sam  | big data      | python   |

- name -> certification, language 일 때, name 마다 여러 개의 certification, language이 존재하는 다치 종속 관계이다.
- certification, language 2가지로 테이블을 분리한다.
### after

| name | certification |
|------|---------------|
| jane | os            |
| sam  | security      |
| sam  | big data      |


| name | language |
|------|----------|
| jane | c        |
| sam  | java     |
| sam  | python   |

<br/><br/>

## 5정규형(5NF): 조인 종속 제거
### before

| name | certification |
|------|---------------|
| jane | os            |
| sam  | security      |
| sam  | big data      |


| name | language |
|------|----------|
| jane | c        |
| sam  | java     |
| sam  | python   |

- 위의 두 테이블을 카디션 조인하면 4차 정규화 수행 이전 데이터와 다르게 되는 문제인 조인 종속이 발생한다.



| name | certification | language |
|------|---------------|----------|
| jane | os            | c        |
| sam  | security      | java     |
| sam  | big data      | java     |
|  sam | security      | python   |
|  sam | big data      | python   |

- 조인 결과가 원래 데이터와 일치하도록 name -> certification, name -> language, certification -> language테이블을 3개로 분리한다.

### after

| name | certification |
|------|---------------|
| jane | os            |
| sam  | security      |
| sam  | big data      |


| certification | language |
|---------------|----------|
| os            | c        |
| security      | java     |
| big data      | python   |


| name | language |
|------|----------|
| jane | c        |
| sam  | java     |
| sam  | python   |

<br/><br/>


# 참고자료
- [2023 수제비 정보처리기사 실기 2권](https://product.kyobobook.co.kr/detail/S000200847120)