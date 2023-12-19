# 7.10

웹 서버마다 **다른 메커니즘**을 사용해서 HTTP 헤더들을 설정한다.

### 7.10.1 아파치로 HTTP 헤더 제어하기

---

아파치 웹 서버는 HTTP 캐시 제어 헤더 설정할 수 있는 여러 메커니즘을 제공한다.

- **mod_headers**
    
    : **개별 헤더**들을 설정할 수 있게 해준다.
    
    → **아파치 정규식** + **필터** ⇒ **개별 콘텐츠**에 헤더 **연결** 가능하다. (계속 추가 가능)
    
    ```java
    <Fils *.html>
     Header set Cache-control no-cache
    </Files>
    ```
    
- **mod_expires**
    
    : **Expire 헤더** 자동 생성 로직을 제공한다.
    
    → **유연하게 표기**가 가능하고 **최종 수정일**로 부터 기간이 발효된다.
    
    ```java
    ExpiresDafault A3600
    ExpiresDafault M86400
    ExpiresDafault  "access plus 1 week"
    ExpiresByType text/html "modification plus 2 days 6 hours 12 minutes"
    ```
    
- **mod_cern_meta**
    
    : HTTP 헤더들의 파일을 **특정 객체와 연결**시켜준다.
    
    → 제어하고자 하는 파일의 **메타 데이터들이 생성**되고, 메타 데이터에 헤더 추가하면 된다.
    

### 7.10.2 HTTP-EQUIV를 통한 HTML 캐시 제어

---

: 기존의 설정 파일로 캐시 헤더 정보를 제어했는데, HTML2.0에서는 <META HTTP-EQUIV>태그를 사용해서 **설정 파일없이도 HTTP 헤더 정의**가 가능하다.

```java
<HTML>
	<HEAD>
		<TITLE>My Document</TITLE>
		<METAHTTP-EQUIV="Cache-control" CONTENT="no-cache">
	</HEAD>
```

→ HTML 문서의 **최상단**에 위치.

※ 해당 기능을 지원하는 프락시는 거의 없다.

1. **서버 부하 가중.**
2. **설정값 정적.**
3. **다른 타입의 파일은 지원하지 않음.**

⇒ 문서의 캐시 제어 요청과 커뮤니케이션하는 유일하게 확실한 방법

: 올바르게 설정된 **서버가 보내온 HTTP 헤더**를 이용하는 것.