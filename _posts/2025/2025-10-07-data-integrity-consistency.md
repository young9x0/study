---
title: 데이터 무결성 vs 데이터 정합성 개념 비교
search: true
categories:
- database
tags:
- data_integrity
- data_consistency
---

# 개념 정리
- 데이터 무결성(Data Integrity):  데이터가 정확하고 완전해야 한다
- 데이터 정합성(Data Consistency): 데이터가 서로 모순이 없이 일관되게 일치해야 한다  

# 비교
## 무결성 훼손 예시
product table

| product_id | product_name |
|------------|--------------|
| -1         | 냉동 블루베리   |

order table

| order_id | product_id | product_name |
|----------|------------|--------------|
| 1        | -1         | 냉동 블루베리      |

product table와 order table에서 product_id는 반드시 1 이상의 값을 가져야할 때,
- product_id는 모두 -1로 일치하므로 데이터 정합성은 지켜졌으나, 1 이상의 값을 가지지 않음으로 데이터 무결성은 훼손되었다.

## 정합성 훼손 예시
product table

| product_id | product_name |
|------------|--------------|
| 1          | 냉동 블루베리      |

order table

| order_id | product_id | product_name |
|----------|------------|--------------|
| 1        | 2          | 냉동 블루베리      |

product table와 order table에서 product_id는 반드시 1 이상의 값을 가져야할 때,
- product_id는 모두 1 이상의 값을 가지므로 데이터 무결성은 지켜졌으나, 테이블마다 서로 값이 일치하지 않음(product.product_id=1, order.product_id=2)으로 데이터 정합성은 훼손되었다.


# 사용 예시 
## 트랜잭션 Transaction
- 데이터베이스의 상태를 변화시키기 해서 수행하는 작업의 단위
- 데이터베이스의 상태는 INSERT, SELECT, UPDATE, DELETE와 같은 DML(데이터 조작어, Data Manipulation Language)로 변화하는데 이때 트랜잭션은 여러 조작어를 하나의 단위로 묶을 때 사용한다.
- 트랜잭션을 사용하면 게시판에 게시글을 새로 등록하고(INSERT), 게시판에 전체 게시글 조회하기(SELECT) 를 하나의 단위로 처리할 수 있게 된다.

## 트랜잭션의 ACID 원칙

### Atomic (원자성)
트랜잭션의 모든 작업이 모두 성공하거나, 모두 실패해야 한다. (부분적으로 실행된 상태는 존재하지 않는다.)
 
### Consistent (일관성)
트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 한다. 이 부분이 바로 **무결성**을 직접적으로 지키는 속성이다.
 
### Isolated (고립성)
둘 이상의 트랜잭션이 동시에 실행되고 있을 경우 어떤 하나의 트랜잭션이라도, 다른 트랜잭션의 연산에 끼어들 수 없다.
 
### Durable (지속성)
트랜잭션이 성공적으로 완료됐을 경우, 결과는 영구적으로 반영되어야 한다.



# 참고자료
- [관계형 데이터 모델링 프리미엄 가이드 DB구축 (2014년)](http://www.gurubee.net/lecture/3583)
- [무결성과 정합성이란 무엇인가?](https://velog.io/@yangsijun528/%EB%AC%B4%EA%B2%B0%EC%84%B1%EA%B3%BC-%EC%A0%95%ED%95%A9%EC%84%B1%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
- [트랜잭션\(Transaction\)이란?](https://mommoo.tistory.com/62)