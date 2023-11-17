# 5.7 단계 4 - 리소스 매핑과 접근

웹 서버란 리소스 서버이다.

정적, 동적 컨텐츠를 서빙한다.

서빙하기 전에, URI를 통해 요청이 어떤 자원을 원하는지 식별해야 한다.

## Docroots

가장 쉬운 방법은 URI를 web server의 파일 시스템에다가 매핑하는 것이다.

웹 서버의 파일 시스템 내부에 있는 특별한 폴더가 예약되어 있다. 이를 document root, 혹은 docroot라고 한다.

URI를 받아서 docroot에다가 append한다.

> static serving을 말하는 듯 하다?

### Virtually hosted docroots

여러 개의 웹 사이트를 하나의 웹 서버에서 호스팅하는 것을 말한다.

이 경우, 각각의 사이트는 각자의 docroot가 필요하다.

### User home directory docroots

GET /~bob/index.html

위 요청은 /home/bob/public_html로 매핑된다.

> 2015년에 학교에서 웹 서버를 제공받았을 때 사용하던 방식으로 기억한다.

## Directory Listings

만약 client가 directory URL을 요청한다면

- 에러
- index file 리턴
- 디렉토리를 스캔하고 그 내용을 담은 html 파일을 리턴

등의 선택을 할 수 있다.

> 그래서 Apache 서버를 사용하면 디렉토리 내부의 파일들을 정적인 html 형식으로 바로 볼 수 있었던 것으로 기억한다!

## Dynamic Content Resource Mapping

때로는 URI를 동적인 컨텐츠, 즉 그때 그때 필요한 자원들을 생성해내는 프로그램에 매핑할 수도 있다.

이러한 역할을 하는 웹 서버를 application servers라고 부른다.

## Server-Side Includes (SSI)

> Server Side Rendering의 기초 버전인 듯 하다.

## Access Controls

IP나 비밀번호에 따라 접근 제어도 할 수 있다.
