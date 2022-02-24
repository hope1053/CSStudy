# TCP 3 way handshake & 4 way handshake

# 3 way handshake : 연결 성립

TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정

- SYN: Synchronize sequence numbers
    - 연결 설정,  Sequence Number를 랜덤으로 설정하여 세션을 연결하는데 사용하며 초기에 Sequence Number를 전송함
- ACK: Acknowledgment
    - 응답 확인, 패킷을 받았다는 의미
    - Acknowledgement Number 필드가 유효한지 나타냄

## 배경

- TCP는 정확한 전송을 보장해야함, 통신하기에 앞서 `논리적인 접속을 성립`하기 위해 3 way handshake 과정 진행

## 역할

- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장, 실제로 데이터 전달이 시작하기 전에 한쪽이 다른쪽이 준비되었다는 것을 알 수 있도록 한다.

## 과정

![Untitled](TCP%203%20way%20%20f1e7a/Untitled.png)

1. 클라이언트가 서버한테 접속을 요청하는 **SYN** 패킷을 보냄 (sequence: x) → 이때 클라이언트는 SYN을 보내고 SYN/ACK응답을 기다리는 SYN_SENT 상태가 됨, 서버는 LISTEN
2. 서버가 SYN(x)를 받고 클라이언트로 받았다는 신호인 **ACK**와 **SYN** flag가 설정된 패킷을 보냄 (sequence: y, ACK: x+1), 클라이언트가 다시 ACK로 응답하기를 기다림 → 이때 서버는 SYN_RECEIVED 상태가 됨, 클라이언트는 CLOSED
3. 클라이언트는 서버의 응답인 ACK(x+1), SYN(y) 패킷을 받고 **ACK**(y+1)을 서버로 보냄 → 클라이언트는 ESTABLISHED, 서버는 SYN_RCV → ACK → ESTABLISHED

→ 이렇게 3번의 통신이 완료되면 연결이 성립된다, 데이터가 오가기 시작

# 4 way handshake : 연결 해제

![Untitled](TCP%203%20way%20%20f1e7a/Untitled%201.png)

- 3 way handshake로 연결을 성립한 후, 모든 통신이 끝나면 연결을 해제해야함

1. 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보냄(Half Close)
    1. Half-Close 기법을 사용하면 종료 요청자가 처음 보내는 FIN 패킷에 승인 번호를 함께 담아서 보내게 되는데, 이때 승인 번호의 의미는 **"일단 연결은 종료할건데 귀는 열어둘게. 이 승인 번호까지 처리했으니까 더 보낼 거 있으면 보내"**(ACK 포함)
2. 서버는 FIN 받고 확인했다는 ACK를 클라이언트에게 보냄 (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 됨)
3. 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보냄
4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다. (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다린다.)
- 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)

> 그런데 만약 "Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN패킷보다 늦게 도착하는 상황"이 발생한다면 어떻게 될까요?
> 
> 
> Client에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop되고 데이터는 유실될 것입니다.
> 
> 이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도 일정시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 "TIME_WAIT" 라고 합니다.
> 

> **Q. TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?**
> 
> 
> A. Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다.
>