---
title: RESTful API 개념 정리
search: true
categories:
- Computer-Science
tags:
- restful-api
- Model
- probability
- random variable
---

## 개념
* HTTP URI를 통해 자원을 명시하고, HTTP Method (POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD OPERATION을 적용하는 것을 의미한다.
## 필요성
* RESTful APIs 개발하는 가장 큰 이유는 Client Side를 정형화된 플랫폼이 아닌 모바일, PC, 어플리케이션 등 플랫폼에 제약을 두지 않는 것을 목표로 했기 때문이다.하지만 스마트 기기들이 등장하면서 TV, 스마트 폰, 테블릿 등 Client 프로그램이 다양화 되고 그에 맞춰 Server를 일일이 만다는 것이 꽤 비효율적인 일이 되어 버렸다. 이런 과정에서 개발자들은 Client Side를 전혀 고려하지 않고 메시지 기반, XML, JSON과 같은 Client에서 바로 객체로 치환 가능한 형태의 데이터 통신을 지향하게 되면서 Server와 Client의 역할을 분리하게 되었다.
## 구성
* 자원(Resource)
* 행위(Verb)
* 표현(Representations)

### 자원 Resource
* 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
* 자원을 구별하는 ID는 /orders/order_id/1 와 같은 HTTP URI 이다.
### 행위 Verb
* HTTP 프로토콜의 Method를 사용한다.
* HTTP 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공한다.
### 표현 Representaion of Resource
* Client가 자원의 상태 (정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답 (Representation)을 보낸다.
* REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타낼 수 있다.
* 현재는 JSON으로 주고 받는 것이 대부분이다.
## 단점
1. REST는 point-to-point 통신모델을 기본으로 한다. 따라서 서버와 클라이언트가 연결을 맺고 상호작용해야하는 어플리케이션의 개발에는 적당하지 않다.
2. REST는 URI, HTTP 이용한 아키텍처링 방법에 대한 내용만을 담고 있다. 보안과 통신규약 정책 같은 것은 전혀다루지 않는다. 따라서 개발자는 통신과 정책에 대한 설계와 구현을 도맡아서 진행해야 한다.
3. HTTP에 상당히 의존적이다. REST는 설계 원리이기 때문에 HTTP와는 상관없이 다른 프로토콜에서도 구현할 수 있기는 하지만 자연스러운 개발이 힘들다. 다만 REST를 사용하는 이유가 대부분의 서비스가 웹으로 통합되는 상황이기에 큰 단점이 아니게 되었다.
4. CRUD 4가지 메소드만 제공한다. 대부분의 일들을 처리할 수 있지만, 4가지 메소드 만으로 처리하기엔 모호한 표현이 있다.


# 참고자료
[RESTful API 이란](https://velog.io/@somday/RESTful-API-%EC%9D%B4%EB%9E%80)
