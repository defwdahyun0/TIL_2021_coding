## 1. HTTP
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
## 2. 데이터포맷
* 데이터를 보낼 때 어떤 형식을 사용할지
* XML -> JSON
* JSON 장점
    * 1) 데이터의 무게가 가볍다.
    * 2) 객체 단위로 지정이 가능해서 유지보수에 용이하다.
* GET의 경우 읽어오기만 하면 돼서 JSON이 필요 없다.
* POST는 생성하는 것이므로, JSON body 안에 꼭 넣어야한다.

손님 <-> 종업원 <-> 주방장

손님이 식당에 간다는 상황을 가정해보자.

어떤 스테이크 -> API / 어떻게 -> 프로토콜 / 누구한테 -> 아이피

## 3. API 
API는 Application Programming Interface의 약자로, 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 의미한다.

interface 단어에 초점을 맞추면, **맞대는 면**으로 해석해볼 수 있다.
사용자가 스마트폰을 사용할 때, 전원 버튼을 눌러 화면을 끈다. 
사용자의 입장에서 내부로직은 몰라도 된다.
버튼이 API, 즉 매개체 역할을 하는 것이다. 

추가로, API 명세서를 통해서 클라이언트와 서버가 소통할 수 있다.

## 4. Rest API

REST는 REpresentational State Transfer 의 약자로 **HTTP 기반으로 필요한 자원에 접근하는 방식**을 정해놓은 규칙을 뜻한다. 

REST에는 아래와 같은 4개의 속성이 존재한다.

* 서버에 있는 모든 리소스는 클라이언트가 바로 접근할 수 있는 고유 URI가 존재한다. 
* 클라이언트가 요청할 때마다 필요한 정보를 주기 때문에 서버에서는 세션 정보를 포관할 필요가 없다.
* GET / POST / PUT / DELETE 등의 HTTP method를 사용한다.
* 서비스 내 하나의 리소스가 주변에 연관된 리소스들과 연결되어 표현되어야 한다.

그리고 REST는 resource / method / message 세 가지로 구성되어 있다.

### 1) Resource

REST에서는 자원에 접근 할 때 URI(Uniform Resource Identifier)로 하게 된다. URI는 자원의 위치를 나타내는 일종의 식별자인데, URI설계시 지켜야하는 설계규칙에 대해 살펴볼 것이다.

#### (1) / 는 계층 관계를 나타내는 데 사용되며 마지막 문자로는 사용하지 않는다.
ex: http://www.happy-zoo/animals/dogs/john
#### (2) URI를 이루는 resource들은 동사보다는 명사로 이루어져야한다.
#### (3) 리소스 간의 관계
REST 리소스 간에 연관 관계가 있을 수 있는 경우 다음과 같은 표현방법을 사용한다.
```php
/리소스명/리소스 ID/관계가 있는 다른 리소스명
 GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```
만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있습니다. 예를 들어 사용자가 ‘좋아하는’ 디바이스 목록을 표현해야 할 경우 다음과 같은 형태로 사용될 수 있다.
```php
GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)
```
#### (4) URI에서는 _(언더바)보다 -(하이픈)을 권장한다.
```php
/users/{user-idx}
```

#### (5) 파일 확장자는 URI에 포함시키지 않는다.
```python
https://restapi.example.com/members/soccer/345/photo.jpg (X)
```
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다. 
Accept header를 사용해야 한다.
```python
GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```
### 2) Method
다음은 HTTP 메소드에 대한 설명이다. 자원에 접근할 때 어떤 성격의 요청인지 HTTP 메소드가 알려준다. 그 종류는 다음과 같다. 

* GET : 조회
* POST : 생성
* PUT : 수정
* PATCH : 일부 수정
* DELETE : 삭제

### 3) Message
메시지는 HTTP header와 body, 응답상태코드로 구성되어 있으며 header와 body에 포함된 메시지는 메시지를 처리하기 위한 충분한 정보를 포함합니다.

* Body: 자원에 대한 정보를 전달(데이터 포맷: JSON/ XML/ 사용자 정의 포맷)
* Header: HTTP 바디에 어떤 포맷으로 데이터가 담겼는지 정의. 요청 HTTP 헤더는 ‘Accept’ 항목으로 응답, HTTP 헤더는 ‘Content-type’으로 컨텐츠 타입을 설명.
* 응답상태코드: 응답상태코드를 통해 리소스 요청에 대한 응답.

### 4) 장단점
* 장점
    * 어언어와 플랫폼에 독립적이다.
    * SOAP(다른 통신방식)보다 개발이 쉽고 단순하다.
    * REST가 지원하는 프레임워크나 언어등 도구들이 없어도 구현이 가능하다.
    * 기존 웹 인프라를 사용가능하다. HTTP를 그대로 사용하기 때문에 그런 것이다.
* 단점
    * HTTP 프로토콜만 사용이 가능하다.
    * p2p 통신 모델을 가정했기 때문에 둘 이상을 대상으로 하는 분산환경엔 유용하지 않다.
    * 보안, 정책등에 대한 표준이 없기 때문에 관리가 어렵고 이러한 부분까지 고려해서 구현 할 경우 설계나 구현에서 좀 더 어려움을 갖는다.

## 4. 구조

백엔드 언어의 구조는 다음과 같다고 생각할 수 있다.

* route: 경로를 정해준다.
    * controller: route paht-var query-string, body 받아오기. 하위 서비스가 서로 기능을 공유할 때 컨트롤러를 거친다.
        * service: insert,delete,update 주로 사용. DB 연결 시에 사용한다. select 사용할 때는 provider에서 가져와서 실행해야한다.
        * provider: select 주로 사용.
            * Dao: 실질적인 sql query를 실행한다. sql 파일을 dao 파일에 넣어서 실행후 위로 넘겨주어서 client가 볼 수 있게 한다. Rows.

* php에는 route 파일이 없다. indexphp에서 그 역할을 대신한다.
* node.js는 위 형식 따라간다.
* springboot는 route파일이 없고, controller 파일 안에 경로를 지정하는 방식이다.


## 5. Validation (유효성 검증)
데이터를 db에 넣기 전 검증을 통해서 맞지 않은 데이터는 걸러준다.
### 1) 형식적 validation
* type, 빈값, int/string/null/길이, 정규표현식(이메일, 전화번호 등등)
* controller에서 해준다.
### 2) 의미적 validation
* 중복된 유저 아이디 등
* 데이터베이스에 들어가서 있는지 확인후 출력한다. 확인 후 중복된 게 있으면 걸러내준다. 
* service나 provider에서 해준다.

## 6. 관리

파일을 관리할 때는 도메인별로 해줘야 한다.

* 예시) 쿠팡: 상품별, 사용자별 분류

* user 
    * user service
    * user provider
    * user controller

* product 
    * product service
    * procuct provider
    * product controller
    
서비스 중심으로 묶어준다.

---

[참고링크](https://dydrlaks.medium.com/rest-api-3e424716bab)