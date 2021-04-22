# Restful, FrameWork

HTTP 통신 방식, 데이터 포맷 (JSON) 개념 이해

## **Restful API**

표준 설계 방법으로, 클라이언트, 서버 개발자가 서로 소통해야 한다는 점에서 중요하다.

구성은 아래와 같다.

- **자원(RESOURCE)** - URI
- **행위(Verb)** - HTTP METHOD
- **표현(Representations)** 

### REST API 디자인 가이드

#### **1) URI는 정보의 자원을 표현해야 한다. (리소스명은 동사보다는 명사를 사용)**

URI는 자원을 표현하는데 중점을 두어야 한다. delete,block 등과 같은 행위에 대한 표현이 들어가면 안된다.

즉, 명사형, 리소스 단위로 끝을 내야 한다.

- 도메인/block/3 (x)
- 도메인/blocked_user/3 (o)

#### 2) 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현

자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE, PATCH 등)로 표현할 수 있다.

간단하게 PATCH와 PUT의 차이점을 알아보았다.

- PATCH: 리소스 일부 수정이 가능하다.
    - 실무에서는 보안을 위해 PUT, DELETE보다 PATCH를 사용하는 편이다.
- PUT:  리소스를 모두 수정해야한다.

ex)

- 사용자 조회 api: GET Method를 통해 User 리소스를 다룬다.
- 회원가입 api: POST Method를 통해 User 리소스를 다룬다.

추가로, GET과 DELETE는 body가 필요없고, POST,PUT,PATCH는 body가 필요하다. 

GET과 POST의 보안상의 차이가 있을까? 패킷의 header와 body에서 POST Method는 body에, GET Method은 header에 path variable에 넣을 뿐 보안상의 차이는 없다. 패킷 자체를 뺐기지 않는 것이 중요하다.

#### 3) URI 설계 시 주의할 점

1) 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용한다. 

2) URI 마지막 문자로 슬래시(/)를 포함하지 않는다.

**3) 하이픈(-)은 URI 가독성을 높이는데 사용 (명사-명사)**

4) 밑줄(_)은 URI에 사용하지 않는다.

5) URI 경로에는 소문자가 적합하다.

6) 파일 확장자는 URI에 포함시키지 않는다.

#### 4) 리소스 간의 관계를 표현하는 방법

 /리소스명/리소스 ID/관계가 있는 다른 리소스명
    ex)    GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)

만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있다.

  GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)

#### 5) 자원을 표현하는 Colllection과 Document (Path Variable의 구성)

DOCUMENT는 문서, 컬렉션은 문서들의 집합, 객체들의 집합. 컬렉션과 도큐먼트는 모두 리소스라고 표현할 수 있으며 URI에 표현된다. 

- http:// restapi.example.com/sports/soccer/players/13

sports, players 컬렉션과 soccer, 13(13번인 선수)를 의미하는 도큐먼트로 URI가 이루어진다. **컬렉션은 복수**. 

검색 API의 경우 뒤에 query string을 덧붙이는 경우도 있다. 

## **server to server 통신**

API 설계를 할 때, 인증번호 보내기/이메일 보내기 등을 직접 개발하기는 힘들기 때문에 네이버와 구글 등의 API를 빌려와서 사용한다. 이 때의 API를  3rd party server라 할 수 있고, 쉽게 라이브러리라고 생각할 수 있다. 

이러한 통신을 ServerToServer 통신이라고 한다. 

## Library vs Framework

프레임워크 php, node.js, springboot

- 프레임워크
    - 뼈대/기반구조
    - 객체 지향 개발을 하면서 일관성 부족 등의 문제를 해결
    - 유지 보수에 용이
    - 소프트웨어의 특정 문제를 해결하기 위해서 상호 협력하는 클래스와 인터페이스의 집합
    - 소스 코드 작성 매뉴얼
    - Node.js → Express / Spring Framework 등
- 라이브러리
    - 특정 기능에 대한 도구 or 함수들을 모은 집합
    - 단순 활용이 가능한 도구들의 집합
    - 단순 API

---

[참고링크1](https://meetup.toast.com/posts/92)

[참고링크2](https://mangkyu.tistory.com/4)
