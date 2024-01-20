# 16.6 기타 고려사항

## Headers and Out-of-Spec Data

헤더는 아스키로만 적혀야 합니다. 가끔 벗어나는 헤더들이 있습니다.

## Dates

HTTP는 GMT 날짜 형식을 명확히 정의하지만 모든 웹 서버가 이걸 준수하는 것은 아닙니다. 서버에서 로컬 언어로 표현된 HTTP Date를 보내는 경우도 있습니다.

유연하게 처리해야 하고, 이해할 수 없으면 보수적으로 처리해야 합니다.

## Domain Names

책에는 지원 안한다고 되어 있지만, IDN 같은게 현재 있다고 합니다.

Punycode에 대해서도 알아봐야 할 듯 합니다.

ec2에서 리버스 프록시 서버를 돌리고 있는데 계속 punycode 워닝이 떠서 뭔지 의아했습니다.

```
For example, a domain name like "例子.测试" (Chinese for "example.test") would be represented in Punycode as "xn--fsq.xn--0zwm56d".
```

둘이 똑같다고 합니다.

예전에 한글 도메인을 산 팀들이 따로 아스키 URL도 왠지 모르게 생겼다고 했는데 이게 원인이었던 것 같습니다.
