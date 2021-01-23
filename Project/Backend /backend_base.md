서버를 설명하기 위해, 식당의 예시를 들 수 있음

1) 손님 - 클라이언트
클라이언트 종류 : Android, iOS, web
2) 서빙 - 웹서버 : 요리를 전해주기도 하고, 손님한테 휴지를 건네주기도 함(서버 자체가 할 수 있는 일도 있음)(파일 다운, 이미지)
서버 종류 : apache, nginx
서버의 특징 : 1. n:1에서 n과 1이 바뀔 수 있음. 2. 역할 적개? 3. 휴지(서버 각 개인이 할 수 있는 일이 있음)
3) 주방(요리사) - Backend language(BL)
BL 종류 : php, jsp, asp... node.js, spring
4) 냉장고 - DB MS(database management system) : 리소스, 데이터 저장, 통신으로 전달 가능
DB MS 종류 : mysql, oracle, mssql, mongoDB...

최종 목표 : api, rest-api 구현

<br>
<br>

서비스는 웹서버를 거쳐서 이루어짐. (만약 프론트엔드, 즉 클라이언트만으로 이루어진 프로그램은 자신의 컴퓨터에서만 보여주고 통신, 저장 기능은 불가능할 것임.)

가장 난이도가 쉽고 접근하기 쉬운 서버, BL, DB 종류 : apache, php, mysql 줄여서 apm
bitnami로 일괄 다운로드 가능

local host : 127.0.0.1
mapm,rinvx,lamp (?)


<br>
<br>

OS 종류 : window, ubuntu, ios, android, mac, linux 등 
대한민국에서는 window의 점유율이 높지만 전세계적으로는 linux의 점유율이 높음(70%)
이유 : 무료배포 -> 오픈소스 -> 집단지성..

리눅스 OS : 레드헷->centOS, 데미안->ubuntu(진입장벽 낮음, osupdate)
리눅스 OS에 apache, php, mysql 설치해볼 것임.

(우분투 64-bit 18.04.5.2)

<br>
<br>

리눅스 OS에 apache, php, mysql 설치.

쉽게 apt-get으로 설치 가능
그러나 보안의 문제(회사), 필요하지 않은 부분까지 깔림(apt-get, yum)

과제 : 리눅스에 apache,php,mysqp 컴파일설치/소스설치
ubuntu 18.04 apm + 소스설치/컴파일

얻을 수 있는 효과
1) 리눅스와 친해지기
2) cli, 컴파일 익숙해지기
3) 에러 메시지 구글링, 구글링 실력

블로그 - ubuntu 18.04 설치했음. 이후 버전 설치해도 됨.
용량은 넉넉한 게 좋음
apt-get x 