# 20.3 리다이렉션 프로토콜의 개요

**라다이렉션의 목표는 HTTP 메시지를 가용한 웹 서버로 가급적 빨리 보내는 것이다.**    
HTTP 메시지가 인터넷을 통해 나아가는 방향은 HTTP 애플리케이션과 라우팅 장치에 영향을 받는다.

+ 브라우저 애플리케이션의 사용자는 브라우저가 클라이언트 메시지를 프락시 서버로 보내도록 설정 할 수 있다.
+ DNS 분석자는 메시지의 주소를 지정할때 사용될 IP 주소를 선택하게 되는데, 클라이언트의 지리적 위치에 따라 달라질 수 있다.
+ 메시지는 주소가 지정된 여러 개의 패킷으로 나뉘어 네트워크를 통과한다. 스위치와 라우터들은 패킷의 TCP/IP 주소를 검증하고 그에 근거하여 패킷을 어떻게 라우팅할 것인지 결정하게 된다.
+ 웹 서버는 HTTP 리다이렉트를 이용해 요청이 다른 웹 서버로 가도록 할 수 있다.

주의할 사항은, DNS 리다이렉션을 비롯한 대부분의 기법들이 트래픽을 보내려는 곳이 어떤 서버냐에 상관없이 사용될 수 있는 것에 반해 브라우저 설정과 같은 방법은 프락시로 향하는 리다이렉트 트래픽에서만 사용할 수 있다는 점을 유의해야 한다.

