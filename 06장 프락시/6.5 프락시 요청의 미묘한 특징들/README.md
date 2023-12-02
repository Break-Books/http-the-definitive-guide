# 6.5 프락시 요청의 미묘한 특징들

- Proxy request와 Server request의 차이는 무엇인가?
- 인터셉터와 리버스 프로싱이 왜 서버 호스트 정보를 숨기는가?
- URI 수정 룰
- URI auto-completion에 어떤 영향을 주는가?

## 6.5.1 Proxy URIs Differ from Server URIs

서버로 보낼 때는

```http
GET /index.html HTTP/1.0
```

```http
GET /www.abcdabcdabcd.com/index.html HTTP/1.0
```

생략해도 되었다???

클라이언트가 오직 하나의 서버에만 직접적으로 대화했기 때문에?

어차피 연결이 되어 있으면 scheme, host, port 정보가 없어도 연결할 수 있다?

## 6.5.2 The Same Problem with Virtual Hosting

한 대의 서버에 여러 웹 서버가 돌아가고 있으면 그 중 어떤 웹 서버에 요청하는지를 모르므로 scheme, host, port에 대한 정보가 필요하다.

## 6.5.3 Intercepting Proxies Get Partial URIs

하지만 클라이언트가 자기가 프록시에게 요청을 보내고 있는 건지 전혀 모를 수도 있다. 그럴 때는 partial uri만 보내진다.

주로 surrogate이나 intercepting proxy를 통하는 요청이 그러한데, 이 둘의 차이점이 무엇일까?

- surrogate은 hostname이나 ip address 앞에서 모든 요청을 받고 알아서 caching하든, proxy request를 실 서버로 보내주든 역할을 하는 프록시이다.
- intercepting proxy는 네트워크 플로우에서 traffic을 hijack하고 캐시된 응답을 보내거나 실 서버로 보내는 프록시 서버이다.

## 6.5.4 Proxies Can Handle Both Proxy and Server Requests

때문에 Partial URI, Full URI 둘 다 지원한다.

룰은 다음과 같다.

- full URI가 주어지면 그걸 사용한다.
- partial URI가 주어지면 Host Header가 origin server name과 port number를 알아내는 데에 사용된다.
  - proxy가 surrogate이라면 알아서 실제 서버로 보내주도록 설정된다.
  - 만약 traffic이 중간에 가로채졌다면, 인터셉터가 IP 주소와 열고 프록시가 그 포트를 사용 가능하도록 설정한다.
  - 전부 실패할 경우 에러 메세지를 돌려준다.

## In-Flight URI Modification

어떤 프록시들은 URI들을 표준에 맞게 변경한다. 포트를 80으로 명확하게 설정한다든지, illegal reserved characters들을 escape한다든지 등의 변경을 하는데, 이는 상호운용성에 문제를 일으킬 수 있다.

때문에 그런 변경을 하지 않도록 최대한 노력해야 한다. Protocol policemen이 되려고 해서는 안된다.

## URI Client Auto-Expansion and Hostname Resolution

생략

## URI Resolution Without a Proxy

1. oreilly를 찾는다.
2. unknown
3. <www.oreilly.com를> 찾는다.
4. 찾았다! 그러면 브라우저는 자동으로 <www.oreilly.com>으로 변한다.
5. 성공할 때까지 모든 IP 주소에 연결하려 한다.
6. 연결 성공한다.
7. HTTP request를 보낸다.
8. HTTP response를 받는다.

## URI Resolution with an Intercepting Proxy

1. oreilly를 찾는다.
2. 프록시가 명시적으로 적용되어 있기 때문에 브라우저가 프록시 서버의 DNS를 찾는다.
3. 프록시로 그 후 연결한다.
4. 연결 성공!
5. 자동으로 <www.oreilly.com>으로 변한다.
6. HTTP request를 보낸다.
