## 서버 기초개념

서버를 설명하기 위해, 식당의 예시를 들 수 있다.

* 1. 손님 - 클라이언트
    * 클라이언트 종류 : Android, iOS, web
* 2.서빙 - 웹서버 
    * 요리를 전해주기도 하고, 손님한테 휴지를 건네주기도 한다.(서버 자체가 할 수 있는 일도 있음)(파일 다운, 이미지)
    * 서버 종류 : apache, nginx
    * 웹서버의 특징 
        * 1. n:1에서 n과 1이 바뀔 수 있다.
        * 2. 역할이 상대적이다.
        * 3. 서버 각 개인이 할 수 있는 일이 있다.
* 3. 주방(요리사) - Backend language(BL)
    * BL 종류 : php, jsp, asp... node.js, spring
* 4. 냉장고 - DB MS(database management system)
    * 리소스, 데이터 저장, 통신으로 전달 가능
    * DBMS 종류 : mysql, oracle, mssql, mongoDB...

최종 목표는 api, rest-api를 구현하는 것이다.

## 서버단(Server side)

서비스는 웹서버를 거쳐서 이루어진다. 프론트엔드, 즉 클라이언트만으로 이루어진 프로그램은 자신의 컴퓨터에서만 보여주고 통신, 저장 기능은 불가능할 것이다.

가장 난이도가 쉽고 접근하기 쉬운 서버는 아래와 같다. apache, php, mysql 줄여서 apm이다. bitnami로 일괄 다운로드가 가능하다.

local host 주소는 127.0.0.1이다. 

우리가 흔히 말하는 서버는 생각보다 포괄적인 내용이다. server side이라고도 불리는 서버는 총 세 개의 파트로 나눌 수 있다.

### Server program
유닉스 계열뿐 아니라 윈도우 기종에서도 운용할 수 있는 Apache나 비교적 가벼운 nginx가 있다.

### Back-end Language
Spring / node.js / php 등 백엔드 언어는 굉장히 많다.

### DBMS (+DB)
DBMS는 DataBase Management System의 약자로 MySQL / NoSQL 등이 있다.
