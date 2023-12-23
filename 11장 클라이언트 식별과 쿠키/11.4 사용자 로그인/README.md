## 11.4 USER 로그인
- 로그인을 통해서 USER에게 식별 요청 방법
- HTTP는 WWW-Authenticate와 Authorization 헤더를 사용해 웹 사이트에 USER 이름을 전달.
- 한 번 로그인하면, 브라우저는 사이트로 보내느 모든 요청이 이 로그인 정보와 함께 보내진다.

### HTTP 인증 헤더를 사용하여 USER 등록
- 그림 11-2 (a) Client의 request
- 그림 11-2 (b) Server의 401 Login Required HTTP 응답 코드와 WWW-Authenticate 헤더를 반환하여 클라이언트에게 로그인 요청
- USER가 로그인을 입력하고 브라우저는 기존 요청을 다시 보내서 USER 식별을 시도한다.
- 서버는 이제 USER의 식별 정보를 알게된다. 이후, 브라우저는 요청마다 해당 USER의 식별정보 토큰을 Authorizationn 헤더에 담아 서버로 전송하고 세션 동안 USER의 식벽을 유지한다.

