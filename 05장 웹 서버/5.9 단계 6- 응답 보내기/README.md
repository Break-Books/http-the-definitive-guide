# 5.9 단계 6 - 응답 보내기

nonpersistent connection의 경우, 응답을 보내고 connection을 닫는다.

persistent connection의 경우, Content-Length header를 계산하는데에 각별히 조심해야 한다.

실수하면 client는 response가 끝났는지 영영 알 방법이 없다.
