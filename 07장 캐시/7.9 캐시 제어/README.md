# 7.9 캐시 제어

문서가 만료되기 전까지 **얼마나 오랫동안 캐시**될 수 있게 할 것인지 **서버가 설정**할 수 있는 방법의 우선순위

1. **Cache-Control: no-stroe 헤더**
2. **Cache-Control: no-cache 헤더**
3. **Cache-Control: must-revalidate 헤더**
4. **Cache-Control: max-age 헤더**
5. **Expires 날짜 헤더**
6. **휴리스틱 방법** (아무 만료 정보 없이 오직 캐시가 스스로 경험한 것을 토대로 결정하는 것)

### 7.9.1 no-cache와 no-store 응답 헤더

---

1. **no-store**
    
    : 사본 만드는 거 **금지**하고 client에 **no-cache 응답**하며, 해당 객체는 **삭제**한다.
    
    ```java
    Cache-Control: no-store
    ```
    
2. **no-cache**
    
    : 로컬에 **저장**은 하지만 **재검사** 없이는 client에게 제공하지 않는다.
    
    (= Do-Not-Serve-From-Cache-Without-Revalidation 이 더 나은 이름 같다! → 직관적)
    
    ```java
    Cache-Control: no-cache
    ```
    
3. **Pragma: no-cache**
    
    : HTTP/1.0+와 하위호환성을 위해 HTTP/1.1에 포함되어 있다.
    
    (HTTP1.0 애플리케이션이 아니라면 Cache-Control: no-cache를 사용해야 함.)
    

### 7.9.2 Max-Age 응답 헤더

---

 : **유효 기간**을 **초**로 환산하여 표기.

→ 공용 캐시에서는 ‘**s_maxage**’로 표기.

→ max-age를 **0**으로 설정해서 **매접근마다 문서 캐시하지 않거나** **매 접근마다 리프레시**하도록 설정할 수 있다.

```java
Cache-Control: max-age=3600 // -> 1H
Cache-Control: s-maxage=3600 // -> 1H
```

### 7.9.3 Expires 응답 헤더

---

: 실제 **만료 날짜** 명시

→ 많은 서버가 **동기화 되어 있지 않고**, **부정확한 시계**를 가지고 있으므로 더 이상 사용을 권하지 않는다. (**max-age를 더 선호**.)

→ **신선도 수명의 근사값** : (만료일 - 생성일)을 초단위로 환산.

→ ‘**Expires: 0**’ : 항상 만료. (문법 위반 → 소프트웨어 문제를 일으킴.)

### 7.9.4 Must-Revalidate 응답 헤더

---

: **신선하지 않은** 사본이면 **서버의 재검사** 없이 제공해서는 안됨을 의미한다.

→ 원서버에서 **사용할 수 없는 데이터**라면 ‘**504 Gateway Timeout error**’를 반환한다.

### 7.9.5 휴리스틱 만료

---

 : 만료 정보 없이 **경험적인 방법**으로 **최대 나이**를 계산하는 것이다.

→ 최대 나이 값이 24H 보다 크면 **Heuristic Expiration 경고 헤더**가 응답 헤더에 추가되어야 한다.

e.g.) **LM 인자 알고리즘**

: 최근 변경 일시 포함시 사용 가능.

- 캐시된 문서의 마지막 변경일이 **상당히 예전**이면 그대로 보관해도 **안전**.
- 캐시된 문서의 마지막 변경일이 **최근**이면 서버와 재검사하기 전까지 **짧은 기간** 동안만 캐시.

⇒ 많은 서버들이 아직 Expires와 max-age 헤더 생성을 하지 못한다. → 휴리스틱 신선도 계산은 흔하게 사용되고, 신선도 유지기간은 보통 1주일이나 하루로 설정한다.

⇒ 신선도에 대해 아무런 단서가 없는 문서는 기본 신선도 유지기간(1시간이나 하루)을 설정한다.

### 7.9.6 클라이언트 신선도 제약

---

: 웹 브라우저에서는 리프레시 버튼으로 **강제로** ‘GET 요청’을 발생시켜 **재검사** 또는 데이터를 **무조건 가져**온다.

→ 이때, 엄격(최신 유지 필요)과 느슨(성능, 신뢰성, 비용 고려)으로 할 수 있다.