## 15.2 Content-Length : 엔터티의 길이
- Content-Length 헤더는 엔터티 본문의 크기를 바이트 단위로 나타낸다. 필수 헤더.

### 15.2.1 잘림 검출
- Content-Length 헤더가 없다면 클라이언트는 커넥션이 정상적으로 닫힌 것인지 오류 값인지 구분하지 못함.
- 클라이언트는 메시지잘림을 검출하기 위해 필요로하는 헤더.
- 메시지 잘림은 캐싱 프락시 서버에서 특히 취약한다.
- 잘린 메시지인지 인식하지 못했다면, 캐시는 결함이 있는 컨텐츠를 저장하고 계속해서 제공하게 될 것이다. 캐싱 프락시 서버는 Content-Length 헤더를 갖고 있지 않은 HTTP 본문은 보통 캐시하지 않음.

### 15.2.2 잘못된 Content-Length
- Content-Lenth가 잘못된 값을 담고 있을 경우 아예 빠진 것보다도 큰 피해를 유발 할 수 있음.
- HTTP/1.1 User 에이전트는 잘못된 길이를 받고 그 사실을 인지했을 때 USER에게 알려준다.

### 15.2.3 Content-Length와 지속 커넥션(Persistent Connection)
- Content-Length는 지속 커넥션을 위해 필수 헤더이다.
- 응답이 지속 커넥션을 통해서 온것이라면, 또 다른 HTTP 응답이 즉시 그 뒤를 이을 것이다.
- Content-Length 헤더는 클라이언트에게 메시지 하나가 어디서 끝나고 다음 시작은 어디인지 알려준다.
- 커넥션이 지속적이기 때문에, 클라이언트가 커넥션이 닫힌 위치를 근거로 메시지의 끝을 인식하는 것은 불가능하다.
- 청크 인코딩과 관련 15.6절

### 15.2.4 컨텐츠 인코딩
- HTTP는 보안을 강화하거나 압축을 통해 공간을 절약할 수 있도록 엔터티 본문을 인코딩할 수 있게 해준다.
- 만약 본문의 컨텐츠가 인코딩되어 있다면, COntent-Length 헤더는 인코딩되지 않은 원본의 길이가 아닌 인코딩된 본문의 길이를 바이트 단위로 정의한다.
- 지속커넥션일 떄, 인코딩 전의 크기를 보내면 심각한 오류 발행.
- HTTP/1.1 명세에서는 인코딩 되지 않은 원 본문의 길이를 보낼 수 없음, 클라이언트가 자신이 수행한 디코딩 검증이 어렵게 만들기도 한다.

### 15.2.5 엔터티 본문 길이 판별을 위한 규칙
1. 본문을 갖는 것이 허용되지 않은 HTTP는 Content-Length 헤더 무시. HEAD 응답일 경우, HEAD 메서드는 GET 요청을 보냈다면 받게 될 응답에서 본문을 제외하고 헤더들만 보내라고 서버에 요청한다. GET 응답은 Content-Length 헤더를 돌려주기 때문에, HEAD 응답 또한 그럴 것이다. 그러나 GET 응답관느 달리 HEAD 응답은 본문을 갖지 않는다. 어떤 헤더 필드가 존재하느냐와 관계없이 헤더 이후의 첫 번째 빈줄에서 끝나야한다.
2. 메시지가 Trnasfer-Encoding 헤더를 포함하고 있다면 메시지가 커넥션이 닫혀서 먼저 끝나지 않는 이상 엔터티는 '0 바이트 청크'라 불리는 특별한 패턴으로 끝나야 한다.
3. 메시지가 Content-Length 헤더를 가지고 메시지 유형이 엔터티 본문을 허용한다면, Transfer-Encoding 헤더가 존재하지 않는 이상 Content-Length 값은 본문의 길이를 담게된다. Content-Length 헤더 필드와 Identity가 아닌 Transfer-Encoding 헤더 필드를 갖고 있는 메시지를 받았다면 반드시 Content-Length헤더를 무시해야한다. 왜냐하면 전송 인코딩은 엔터티 본문을 표현하고 전송하는 방식을 바꿀 것이기 때문이다.
4. 메시지가 'multipart/byteranges' 미디어 타입을 사용하고 엔터티 길이가 별도로 정의되지 안흥면, 멀티파트 메시지는 각 부분은 각자가 스스로의 크기를 정의할 것이다. 멀티파트 유형은 자신의 크기를 스스로 결정할 수 있는 유일한 엔터티 본문유형. 수신자가 이것을 해석할 수 있다는 사실을 송신자가 알기 전까지 절대로 보내지 말아야한다.
5. 위의 어떤 규칙에도 해당되지 않는 경우, 엔터티는 커넥션이 닫힐 떄끝난다. - 서버만 커넥션을 닫을 수 있음.
6. HTTP/1.0 애플리케이션과의 호환을 위해 엔터티 본문을 갖고 있는 HTTP/1.1 요청은 반드시 유효한 Content-Length 헤더도 가지고 있어야 한다. HTTP/1.1은 본문은 있지만 Content-Length 헤더가 없는 경우, 400 Bad Request응답을 보내고 유효한 Content-Length를 요구하고 싶다면 411 Length Required 응답을 보내라고 조언한다.
    
