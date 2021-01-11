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

- 모든 패킷은 1바이트의 플래그와 그 플래그에 맞는 데이터로 구성되어 있다.

| 1byte flag | nbyte data |
| ---------- | ---------- |

