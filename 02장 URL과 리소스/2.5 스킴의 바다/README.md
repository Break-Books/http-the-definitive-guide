# 2.5 스킴의 바다


| Scheme      | Description                                       |
|-------------|---------------------------------------------------|
| http        | Hypertext Transfer Protocol                       |
| https       | http with Secure Sockets Layer                    |
| mailto      | email address                                     |
| ftp         | File Transfer Protocol                            |
| rtsp, rtspu | for audio and video media resources               |
| file        | files directly accessible on a given host machine |
| news        | access specific articles or newsgroups            |
| telnet      | access interactive services                       |

## ftp

FTP를 사용해서 FTP서버에서 자료를 다운받고 업로드 할 수 있다.

웹이 만들어지기 전에도 있었는데, 이를 데이터 액세스 스킴으로 받아들였다. 

## rtsp

U가 붙으면 UDP다.

## file

직접 기계에서 접근 가능한 파일들

## news

location independent하다. 어디서 가져올지 몰라도 된다. 예를 들어 브라우저에 NNTP 뉴스 서버를 설정해두면 이것이 브라우저에게 해당 뉴스를 얻기 위해 어디에 접근해야 하는지 알려준다.

## telnet

Object를 represent하지는 않지만, 텔넷 프로토콜을 사용해서 인터렉티브하게 서비스를 접근할 수 있다.
