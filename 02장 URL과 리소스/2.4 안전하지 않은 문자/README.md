# 2.4 안전하지 않은 문자

URL은 호환 가능하도록 설계되었다.

SMTP의 경우 몇 개의 문자에 대한 누락이 발생한다.

이를 방지하기 위해 URL은 오직 한정된 몇 가지 알파벳만 사용된다.

그런데 읽는 것도 가능해야 한다. 그래서 보이지 않는 특수문자들이 금지되었다. (공백 띄어쓰기 문자도 금지되었다.)

거기에 complete 해야 한다. 모든 종류의 데이터를 담을 수 있어야 한다. 그래서 escape mechanism도 있어야 한다.

## The URL Character Set

처음에는 US-ASCII를 썼다. 그런데 세상 모든 문자들을 포용할 수는 없다.

그리고 몇몇 URL은 바이너리 데이터도 가지고 있다.

때문에 escape sequence라는 것이 등장한다!

## Encoding 원리

한정된 글자들만 URL에 쓸 수 있다는 한계를 극복하기 위해, 인코딩 스킴이 고안되었다.

% + 0xXX, 즉 퍼센트 사인과 2개의 16진수로 그 문자의 ascii 코드를 나타냈던 것이다.

SPACE의 ascii code 번호는 32, 16진수로 0x20이다.

**따라서 URL에서 띄어쓰기는 %20으로 나타내는 것이다.**

## 문자 제한

위에서 쓰인 퍼센트와 같이, 많은 문자들이 special meaning을 가지고 있기 때문에 직접 URL에 쓰이면 안된다.

| Character | Reservation/Restriction         |
|-----------|---------------------------------|
| %         | escape token                    |
| /         | splitting path segments         |
| .         | path                            |
| ..        | path                            |
| #         | fragment delimit                |
| ?         | query string delimit            |
| ;         | params delimit                  |
| :         | delimit, user/passwd, host/port |
| $,+       | Reserved                        |
| @&=       | special meaning in some schemes |
| {}\|\^~[]` | unsafe handling by transport agents like gateways |
| <>" | Unsafe |
|0x00-0x1F, 0x7F| Restricted |
| > 0x7F | Restricted |

## 기타

가끔 URL에 ~같은 거 써도 괜찮을 때가 있다.

하지만 그래도 안 될 수도 있으니 쓰지 말자.
