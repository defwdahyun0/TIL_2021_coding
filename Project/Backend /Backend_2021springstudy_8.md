# Regex, Test Env, Social Token, In-app Billing, etc

## Test env, Product env

- 백엔드 개발자가 미완성인 API를 서버에 올리고 사용한다면, 앱에서 문제가 발생할 수 있다.
- 그래서 개발하는 공간과 완성된 것을 올리는 공간을 나누어야 한다.
    - Test env : 개발하는 서버
    - Product env : 완성된 API를 올리는 서버, 프론트엔드가 사용
- 동기화
    - github/gitlab등 리모트 저장소에 올리고, 클라이언트 개발자들은 다운로드해서 완성된 API만 사용한다.
    - 나누는 방법
        - URL
        - 폴더
        - 서브 도메인
        - (+) port number
        - (+) 서버 직접 분리

## 보안 검증 (Validation)

- post, put, patch
- 서버에서 데이터를 담아서 넘겨줄 때, 데이터를 검증해야 한다
    - 길이 등 저차원의 검증
    - 정규표현식 (Regex)
        - 이메일 형식
        - 휴대폰 010 시작
        - 위도, 경도 형식
        - 차량 번호 형식
    - 논리적 검증
        - 실제로 있는 유저인지 check
        - db
    - query string, path variable까지 검증을 해줘야 한다.
        - ex) 숫자만 들어가야 한다.
- Validation이 중요한 이유: SQL injection
    - SQL injection: 악의적인 사용자가 보안상의 취약점을 이용하여, 임의의 SQL 문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위

## 소셜 로그인 토큰 검증

1. Client가 ID,PW를 입력해서 카카오에 보낸다.
2. kakao는 서버에서 검증 과정을 거치고, 유저 정보가 존재한다면 카카오 식별자(Access Token)를 클라이언트에 넘겨준다.
3. Server는 식별자를 클라이언트로부터 받는다.
4. Server는 식별자가 존재하는지 kakao에 다시 한 번 요청을 보내서 확인한다.
5.  Server에서 DB에 저장한다. 
6. DB는 response를 보내 Client에 '로그인 성공' 등의 메시지를 남긴다.

## 인앱 결제 토큰 검증

1. Cleint에서 카카오페이로 결제 요청을 보낸다.
2. 카카오페이는 카드사로 충전 요청을 보내고 충전 금액을 받는다.
3. 카카오페이는 클라이언트에 영수증을 보내준다.
4. Client에서 영수증을 받아서 영수증을 Server로 보내준다.
5. Server에서 카카오페이로 요청을 보내 식별자가 유효한지 확인한다.
6. Server에서 DB에 저장한다.
7. DB는 response를 보내 Client에서 '결제 완료' 등의 메시지를 남긴다.