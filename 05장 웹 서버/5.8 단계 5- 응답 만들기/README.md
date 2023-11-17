# 5.8 단계 5 - 응답 만들기

## Response Entities

주로 이런 내용을 담고 있다.

- Content-Type header: body의 MIME 타입을 나타내야 한다.
- Content-Length header: body의 사이즈를 나타내야 한다.
- 실제 body 내용

## MIME Typing

### mime.types

웹 서버는 파일의 확장자를 통해 MIME 타입을 나타낼 수도 있다.

### Magic typing

자원의 내용을 스캔하고 패턴을 찾아서 알아서 MIME 타입을 알아낼 수도 있다.

### Explicit typing

확장자나 내용에 상관 없이 강제적으로 MIME 타입을 지정할 수도 있다.

### Type negotiation

17장 참고

## Redirection

성공 메세지 대신 redirection 메세지를 리턴할 수도 있다. 브라우저에게 '다른 곳'을 찾아보라고 알려줄 수 있다. 3XX 리턴 코드를 갖는다.

### Permanently moved resources

301 Moved Permanently

리소스가 새로운 곳으로 영원히 옮겨졌을 때 사용된다. 클라이언트는 필요하다면 정보를 업데이트 할 수 있다.

### Temporarily moved resources

303 See Other
307 Temporary Redirect

지금 잠시 옮겨졌지만 나중에 다시 돌아올 수 있으므로 북마크와 같은 것을 업데이트하지 않아도 된다.

### URL augmentation

URL에 서버가 자동으로 유저에 관련된 추가적인 파라미터를 삽입하여 사용자 행동 추적, 경험 맞춤화 등을 할 수 있게 해준다.

> 그냥 header, body, cookie에 하면 되는 게 아닐까?
> 중요한 정보는 URL로 전달되어서는 안되기 때문에 쓸모에 한계가 있다.

### Load balancing

서버가 너무 많은 요청을 받을 경우, 같은 요청을 처리해 줄 수 있는 다른 서버로 요청을 보내준다.

### Server affinity

서버 어피니티, 혹은 세은 어피니티는 클라이언트의 요청을 일정 기간 동안 동일한 서버로 보내는 로드 밸런싱 방식을 뜻한다. 사용자의 정보를 가지고 있는 서버로 보내야만 세션 관리를 할 수 있으므로...

### Canonicalizing directory names

만약 클라이언트가 디렉토리 URL를 슬래시 없이 보냈을 경우, 대부분의 웹 서버는 자동으로 slash (/)를 붙여준다.
