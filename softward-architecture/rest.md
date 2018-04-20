# REST (REpresentational State Transfer)

## 1. REST란?
- Software Architecture
- HTTP URI + HTTP Method 이다. URI로 대상 자원을 명시하고 Method로 해당 자원에 대한 행위를 정의한다.

## 2. REST 특징
- **Client-Server** : 클라이언트-서버 스타일은 사용자 인터페이스에 대한 관심(concern)을 데이터 저장에 대한 관심으로부터 분리함으로써 **클라이언트의 이식성**과 **서버의 규모확장성**을 개선한다.
- **Stateless** :  클라이언트와 서버의 통신에는 상태가 없어야한다. 모든 요청은 필요한 정보를 담고 있어야한다. **가시성**이 개선되고, task 실패시 복원이 쉬우므로 **신뢰성**이 개선되며, 상태를 저장할 필요가 없으므로 **규모확장성**이 개선된다.
- **Uniform Interface** : 구성요소(클라이언트, 서버 등) 사이의 인터페이스는 균일해야한다. 인터페이스를 일반화함으로써, 전체 시스템 **아키텍처가 단순**해지고, 상호작용의 **가시성이 개선**되며, 구현과 서비스가 분리되므로 **독립적인 진화**가 가능해진다.
- **Layered System** : 계층으로 구성이 가능해야하며, 각 레이어에 속한 구성요소는 인접하지 않은 레이어의 구성요소를 볼 수 없어야한다.
- **Cacheable** : 캐시가 가능해야한다. 즉 모든 서버 응답은 캐시 가능한지 그렇지 아닌지 알 수 있어야한다. **효율, 규모확장성, 사용자 입장에서의 성능이 개선된다.**
- **Code on Demand**(Optional) : 서버가 네트워크를 통해 클라이언트에 프로그램을 전달하면 그 프로그램이 클라이언트에서 실행될 수 있어야한다. (Java applet, Javascript 같은 것을 말함) 다만 이 제약조건은 필수는 아니다.

## 3. HTTP와 REST
HTTP 프로토콜에 정의된 4개의 메서드들이 Resource에 대한 CRUD를 정의한다.
- POST - Create : 자원을 생성
- GET - Select : 자원의 정보를 읽기
- UPDATE - Update : 자원의 정보를 업데이트
- DELETE - Delete : 자원의 삭제

## 4. REST 구성 요소
- Resource  
: REST에서 가장 중요한 개념은 유일한 ID를 가지는 Resource가 서버에 존재하고, 클라이언트는 Resource의 상태를 조작하기 위해 요청을 보낸다는 것이다. Resource는 user, group과 같은 명사형의 단어이고, HTTP에서 이러한 Resource를 구별하기 위한 ID는 'group/member/100'과 같은 URI이다.


- Method  
: 클라이언트는 URI를 이용해 Resource를 지정하고 해당 Resource를 조작하기 위해 메서드(POST, GET, UPDATE, DELETE)를 사용한다.


- Representational of Resource  
: 클라이언트가 서버로 요청을 보냈을 때, 서버가 응답으로 보내주는 Resource의 상태를 Representation이라 한다. REST에서 하나의 Resource는 여러 형태의 Representation으로 나타내어 질 수 있다. 예를 들어 xml, json, text, rss 등으로 전달할 수 있다.


- URI 구성
  - '/country', '/users' 와 같이 직관적으로 어떤 정보를 제공하는 지 알 수 있는 단어들로 구성
  - '/school/grade/class'와 같이 URI path가 계층적인 구조를 가지도록 구성
  - 상위 path는 하위 path의 집합을 의미하는 단어로 구성
  - CRUD 처리는 URI에 명시적으로 표현하도록 하여 URI를 보더라도 직관적으로 어떤 기능을 제공하는지 알 수 있도록 명명하도록 한다.
