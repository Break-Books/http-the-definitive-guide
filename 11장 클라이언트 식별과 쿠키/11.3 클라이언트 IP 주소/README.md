## 11.3 Client IP 주소
- 과거 USER 식별에 클라이언트의 IP주소를 사용.

### Client IP로 USER를 식별하는 방법의 단점
- Client IP 주소는 USER가 아닌, USER가 사용하는 COM을 가리킨다. - 여러 USER가 사용하는 COM 일경우, 식별하기 어려움
- 많은 인터넷 서비스 제공자(ISP)는 USER가 로그인하면 동적으로 IP 주소를 할당 - USER는 매번 다른 주소를 할당받는다.
- NAT(Network Address Translation) 방화벽을 통해 인터넷을 이용하며 NAT는 실제 IP주소를 숨기고 방화벽 IP 주소와 다른 포트번호로 변환된다.
- HTTP 프락시와 게이트웨이는 원서버에 새로운 TCP 연결을 하고 Client IP 주소 대신 프락시 서버 IP주소를 확인한다.


