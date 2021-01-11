# connectsix-protocol
Communication protocol for connect6 game based on tcp

## Protocol

### Server-Client Model

- 7기 오델로 프로토콜에서 이용하였던 Server-Client Model을 채택하여 사용한다
- 채택 이유는 [othello-server repository](https://github.com/umbum/othello-server)를 참고

#### Server to Client

- [READY](#READY)
- [START](#START)
- [TURN](#TURN)
- [RESULT](#RESULT)
- [OVER](#OVER)
- [ERROR](#ERROR)

#### Client to Server

- [IN](#IN)
- [PUT](#PUT)

### Packets

- 모든 패킷은 1바이트의 플래그와 그 플래그에 맞는 데이터로 구성되어 있다

| flag | data |
| ---- | ---- |
| 1byte | nbit |

- flag의 각 비트는 아래와 같은 의미를 가진다

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| - | - | - | - | - | - | - | - |
| [IN](#IN) | [READY](#READY) | [START](#START) | [PUT](#PUT) | [RESULT](#RESULT) | [OVER](#OVER) | [RESERVED](#RESURVED) | [ERROR](#ERROR) |

#### IN

게임 참가 의사를 표현

- 구성

| flag |
| ---- |
| 1byte |

- 예시

| 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| - | - | - | - | - | - | - | - |

#### READY

게임 참가가 완료되었음을 전달

- 구성

| flag |
| ---- |
| 1byte |

- 예시

| 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| - | - | - | - | - | - | - | - |

#### START

게임 시작 안내

- 구성

| flag | color |
| ---- | ----- |
| 1byte | 1bit |

- 예시
	- 흑돌로 게임을 시작하는 경우

| 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 |
| - | - | - | - | - | - | - | - | - |

#### PUT

바둑돌을 둘 위치 전송

- 구성

| flag | color | vertical | horizontal |
| ---- | ----- | -------- | ---------- |
| 1byte | 1bit | 1byte | 1byte |

- 예시
	- 흑돌을 C2(2,1) 에 두는 경우

| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |

#### RESULT

바둑돌을 둔 이후 결과를 안내

- 구성

| flag | privcolor | vertical | horizontal | nextcolor |
| ---- | --------- | -------- | ---------- | --------- |
| 1byte | 1bit | 1byte | 1byte | 1bit |

- 예시
	- 이전에 흑돌이 C2(2,1) 에 두었고, 다음은 흰돌의 차례인 경우

| 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |

