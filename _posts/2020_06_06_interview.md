---
title:  "면접 대비 질문 모음"
search: false
categories: 
  - interview
last_modified_at: 2020-06-06T20:00:00+09:00
---

# 면접 질문 모음

## OOP
1. 객체지향 개발 원칙인 'SOLID'에서 원칙과 그것에 대한 간단한 설명을 할 수 있는가?

2. SOLID 윈칙중 OCP에 대해 설명하고, 이 원칙을 적용하여 해결 할 수 있는 문제의 예시를 들어 볼것

3. 

## MSA
https://bcho.tistory.com/tag/%EB%A7%88%ED%8B%B4%ED%8C%8C%EC%9A%B8%EB%9F%AC

- SRP을 중시함
- 작은 단위로 분해된 서비스들이 꼭 같은 언어나 프레임웍을 사용할 필요는 없음. 프로토콜만 맞추면 됨 
- 모놀리틱 서비스는 특정 부분에 트래픽이 심해지는 경우 전체를 스케일 아웃 해야 하지만  MSA는 특정 서비스만 확장 할 수 있고 다른 서비스의 무결성을 지킬 수 있음  단점 > 
- 서비스간 통신 방법이 필요
- 데이터 중복이 발 생 할 수 있음
- 트랜잭션 롤백 플랜들을 구상하기 어려 울 수 있음


1. MSA 도입함으로써 생기는 장점과 단점

2. 모놀리스 -> MAS 아키텍쳐로 작업을 이관할때 각 'Service'들을 나누는 관점

3. 

## 네트워크 관련 질문

1. OSI 7 Layer와 각 계층에 대한 간단한 설명
OSI 7 Layer 란 통신 접속에서 완료까지의 과정을 7단계로 정의한 국제 통신 표준 규약으로 다음과 같이 분류된다. 

* 물리계층 : 전송하는데 필요한 기능을 제공. 장비로는 통신 케이블, 허브가 존재한다. 데이터가 무엇인지, 어떤 에러가 있는지 등에는 전혀 신경 쓰지 않는다. 
* 데이터링크계층 : 송/수신을 확인. MAC Address를 가지고 통신. 장비로는 브릿지와 스위치가 존재한다. 
* 네트워크계층 : 패킷을 네트워크 간의 IP를 통하여 데이터를 전달, 장비로는 라우팅이 존재한다.
* 전송계층 : 두 호스트 시스템으로부터 발생하는 데이터의 흐름을 제공한다.
* 세션계층 : 통신 시스템 사용자간의 연결을 유지 및 설정한다.
* 표현계층 : 세션 계층 간의 주고받는 인터페이스를 일관성 있게 제공한다.
* 응용계층 : 사용자가 네트워크에 접근할 수 있도록 서비스를 제공한다.

2. NGINX vs APACHE
NGINX 
- Event Drivne 방식 (프로세스나 스레드 개념은 사용하지 않고)
- 큰 트래픽이 발생하는 경우 처리하기 좋음
APACHE
- 요청이 많을 수록 CPU와 메모리 사용이 증가하기 때문에 성능이 저하 될 수 있다.
- 요청 하나당 스레드 하나가 처리하는 구조 - Nginx 보다 다양한 모듈이 존재, 안정성, 확장성, 호환서 우세

3. UDP vs TCP
4. 프로토콜? 컴퓨터나 원거리 장비들간의 메세지를 주고 받기 위한 일종의 규약 
5. HTTP (Hyper Text Transfer Protocol) 인터넷에서 데이터를 주고 받을 수 있는 프로토콜 
6. HTTPS 통신 방식 
7. 3-way handshake TCP/IP프로토콜을. 이용하여 통신을 하는 응용 프로그램이 데이터를 전송하기전에 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정 SYN : synchronize sequence numbers ACK : acknowledgment


### HTTP + RestfulAPI
1. GET, POST, PUT, DELETE 외에 다른 메서드를 사용해본 경험


2. PUT, PATCH 메서드의 동작 차이
https://medium.com/backticks-tildes/restful-api-design-put-vs-patch-4a061aa3ed0b
PUT이 해당 자원의 전체를 교체하는 의미를 지니는 대신, PATCH는 일부를 변경한다는 의미를 지니기 때문에 최근 update 이벤트에서 PUT보다 더 의미적으로 적합하다고 평가받고 있다. 또한 PUT의 경우는 멱등하지만, PATCH의 경우는 멱등하지 않다. PUT은 전체 자원을 업데이트 하기 때문에 동일 자원에 대해서 동일하게 PUT을 처리하는 경우 멱등하게 처리된다. 반면 PATCH로 처리되는 경우 자원의 일부가 변경되기 때문에 멱등성을 보장할 수 없다.

* 개발에서의 '멱등성(Idempotence)'?
  연산을 여러번 수행해도 결과가 달라지지 않는 성질을 의미함

  수학적으로 표현하면,

  ``` math
    f(f(x)) = f(x)
  ```

  HTTP 메서드에서 GET, PUT, DELETE 등이 멱등성이 있다. 라고 표현 할 수 있다. (POST는 멱등성이 보장 되지 않는다.)



### Docker, Kubernetes
#### DOCKER
컨테이너 기반의 오픈소스 가상화 플랫폼
OS를 가상화 하는것이 아니라 프로세스를 격리하는 방식이 등장함 

1. 유니온 파일시스템
2. 도커 사용의 강점

3. 도커의 네트워크 모드 (Bridge 모드 --net=host등의 차이)


### DJANGO

1. django orm은 lazy evaluation이 일어나는데 실제로 어떤 경우에 lazy evaluation이 일어나는지 설명하시오
-> iteration, len(), repr(), list(), bool(), slicing, if statement, pickling, Caching

2. django orm의 caching이 사용 되는 순간은?
-> callable 하지 않은 속성들의 값은 캐시가 된다. (객체 속성들등 )

3. iterator()를 사용함으로써 캐시가 쿼리셋 단에서 진행되는 것을 방지할 수 있음 (결과는 caching됨)

4. aggregation 사용 경험?

5. 1:N, 1:1로 FK를 통해 연결되어 있는 데이터를 같이 가져오ㅜ는 방법 select_related, prefetch_related

PYTHON
http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-5-%EC%83%81%EC%86%8D%EA%B3%BC-%EC%84%9C%EB%B8%8C-%ED%81%B4%EB%9E%98%EC%8A%A4inheritance-and-subclass/

1. GIL(Global Interpreter Lock)
  'Thread-safe 하다'의 의미 => race condition을 발생시키지 않으면서 각자의 일을 수행할 수 있는 것을 의미.

  MUTEX


2. Composition 
  특정 클래스의 메서드만 활용하고 싶을때 사용하는 방법, 명시적 선언

3. Closure
  프리변수 (코드블럭안에서 사용은 하지만 해당 코드블럭에 선언되지 않은 변수)
  클로저는 함수의 프리변수 값을 어딘가에 저장함 (사용하지 않으면 저장 x)

4. Method Resolution Order 

5. Django Middleware