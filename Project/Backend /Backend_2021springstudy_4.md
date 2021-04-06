1. HTTP
* packet(패킷)  -> 택배상자 
    * header -> 라벨지 -> ip주소 -> 데이터의 데이터
    * body -> 내용물 -> data -> 실제 데이터
* method(메서드)
    * GET : 쿼리스트링으로 데이터교환, 쿼리스트링 구성 keyval2, " userid_r"
    * PUT
    * POST : body, form
    * PATCH
    * DELETE
    * 예시: damoain.com/users?

2. 데이터포맷
* 데이터를 보낼 때 어떤 형식을 사용할지
* XML -> JSON
* JSON 장점
    * 1) 데이터의 무게가 가볍다.
    * 2) 객체 단위로 지정이 가능해서 유지보수에 용이하다.
* GET의 경우 읽어오기만 하면 돼서 JSON이 필요 없다.
* POST는 생성하는 것이므로, JSON body 안에 꼭 넣어야한다.

손님 <-> 종업원 <-> 주방장
손님이 식당에 간다는 상황을 가정해보자.
어떤 스테이크 -> API
어떻게 -> 프로토콜
누구한테 -> 아이피

3. API 
API는 Application Programming Interface의 약자로, 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 의미한다.

interface 단어에 초점을 맞추면, **맞대는 면**으로 해석해볼 수 있다.
사용자가 스마트폰을 사용할 때, 전원 버튼을 눌러 화면을 끈다. 
사용자의 입장에서 내부로직은 몰라도 된다.
버튼이 API, 즉 매개체 역할을 하는 것이다. 

추가로, API 명세서를 통해서 클라이언트와 서버가 소통할 수 있다.

4. Rest API

REST는 REpresentational State Transfer 의 약자로 **HTTP 기반으로 필요한 자원에 접근하는 방식**을 정해놓은 규칙을 뜻한다. 

REST에는 아래와 같은 4개의 속성이 존재한다.

* 서버에 있는 모든 리소스는 클라이언트가 바로 접근할 수 있는 고유 URI가 존재한다. 
* 클라이언트가 요청할 때마다 필요한 정보를 주기 때문에 서버에서는 세션 정보를 포관할 필요가 없다.
* GET / POST / PUT / DELETE 등의 HTTP method를 사용한다.
* 서비스 내 하나의 리소스가 주변에 연관된 리소스들과 연결되어 표현되어야 한다.

그리고 REST는 resource / method / message 세 가지로 구성되어 있다.

**1) Resource**
REST에서는 자원에 접근 할 때 URI(Uniform Resource Identifier)로 하게 된다. URI는 자원의 위치를 나타내는 일종의 식별자인데, URI설계시 지켜야하는 설계규칙에 대해 살펴볼 것이다.

/ 는 계층 관계를 나타내는 데 사용되며 마지막 문자로는 사용하지 않는다.

```php
/users/sangmin/ (x)
```
URI를 구성하는 리소스들은 명사로 이루어져야하며 소문자로 작성한다.
```php
/users/sangmin
```

URI에서는 _(언더바)보다 -(하이픈)을 권장한다.
```php
/users/{user-idx}
```

파일 확장자는 URI에 포함시키지 않는다.
```php
/users/sangmin/logo.png (x)
```

> Method
위에서 잠깐 언급한 HTTP method에 대해서 알아보자. 서버 측 자원에 대한 행위라는 것을 꼭 기억해야 한다.

* GET : 조회
* POST : 생성
* PUT : 수정
* PATCH : 일부 수정
* DELETE : 삭제

GET과 POST 방식의 차이점을 보안이라는 측면에서 설명하는 사람들이 많다. 나도 여태껏 이렇게 생각해왔는데, 이는 정확한 답변이 아니라고 한다.
클라이언트는 GET으로 요청할 때 querystring을 이용한다. 반면 POST 같은 경우 packet body 부분에 넣어서 보낸다. 대부분 이러한 이유 때문에 GET 방식이 POST 방식보다 보안에 취약하다고 생각할 것이다. 하지만 POST 방식으로 요청할 때도 마음만 먹으면 손쉽게 데이터를 가로챌 수 있다.
그러므로 보안성보다는 행위 자체에 초점을 두어야 한다. GET은 저장되어 있는 리소스를 조회하는 것이고, POST는 클라이언트에서 준 데이터를 새롭게 저장해달라는 요청이다.

> Message
클라이언트에서 서버로 요청할 때나 서버에서 클라이언트로 응답할 때 HTTP packet(혹은 message)을 사용한다. 택배 상자를 떠올리면 더 쉽게 이해할 수 있다. 표면에 송장(Header)이 붙어 있고 안에 내용물(Body)을 담는다. Header에는 내용 타입이나 언제 보냈는지에 대한 정보, 인증 토큰처럼 metadata가 들어있으며 Body는 말 그대로 진짜 데이터를 포함한다. 추가적으로 상태 코드에 대한 내용은 Mozilla에 자세히 나와 있다.

4. 구조

* route
    * controller
        * service
        * provider
            * Dao
백엔드 언어의 구조는 다음과 같다고 생각할 수 있다.

route: 경로를 정해준다.
controller: 컨트롤러를 거쳐서 어디로 가야할지 
service: 서비스 파일에서는 insert,delete,update같은 명령 실행. 서비스에서 select 사용할 때는 provider에서 가져와서 실행해야함
provider: select 주로 사용.
Dao: 실질적인 sql 쿼리 작성. sql 파일을 dao 파일에 넣어서 실행후 위로 넘겨주어서 client가 볼 수 있게 한다.


5. Validation (유효성 검증)
검증을 통해서 바로 db에 들어가기 때문에, 맞지 않은 데이터는 걸러줌

1) 형식적 validation: type, 빈값,(int string null 길이), 정규표현식(이메일, 전화번호 등등) : controller에서 해준다.
2) 의미적 validation: 중복된 유저 아이디. 데이터베이스에 들어가서 있는지 확인후 출력. 확인 후 중복된 게 있으면 걸러내줌. service나 provider에서 해줘야 한다.

예시)
회원가입, 이메일 주소를 입력할 때 123 -> 형식이 맞지 않는다.
.com .net 이런 부분이 없어서
이런 부분을 서버에서 관리해줘야 한다.
input을 받아서 reject을 해준다.
올바른 형식을 입력해주십시오.

파일을 관리할 때는 도메인별로 해줘야 한다.
예시로 쿠팡, 상품별로 사용자별로 자료들이 있다.
이런 경우에는
user - user service
    - user provider
    - user controller

product - product service
        - procuct provider
        - product controller
    
서비스 중심으로 묶어주기


(php에는 route파일이 없음 -> indexphp)
(node.js는 형식 따라감)
(springboot는 route파일이 없고, controller 파일 안에 경로를 지정하는 방식)

[참고링크](https://dydrlaks.medium.com/rest-api-3e424716bab)