# 14.9 프락시를 통한 보안 트래픽 터널링

클라이언트는 웹 서버에 접근하기 위해 웹 프록시 서버를 사용하기도 한다.

많은 회사들이 보안 경계에 프록시를 설치해둔다.

문제는 이제 클라이언트가 서버로 보내는 데이터를 암호화하기 때문에, 프록시가 데이터를 어디로 보내야 할 지 알 수가 없다. 헤더를 더 이상 읽을 수 없기 때문에...

따라서 HTTPS가 프록시와 함께 동작하려면 몇 가지 수정 사항들을 반영해야 한다.

한 가지 인기 있는 방법은 'HTTPS SSL tunneling protocol'이다.

이 방법을 사용하면 우선 클라이언트가 프록시에게 호스트와 포트를 알려준다.

이건 암호화하기 전에 plain text로 보내기 때문에 프록시가 정보를 읽을 수가 있다.

여기서 HTTP CONNECT 메서드를 사용한다.

이 메서드는 프록시로 하여금 클라이언트와 서버 호스트 사이의 터널링 역할을 하게 만든다.

다음과 같이 생겼다.

```http
CONNECT home.netscape.com:443 HTTP/1.0
User-agent: Mozilla/1.1N

<raw SSL-encrypted data would follow here...>
```

프록시는 연결이 성공하면 다음과 같이 보낸다.

```http
HTTP/1.0 200 Connection established
Proxy-agent: Netscape-Proxy/1.1
```
