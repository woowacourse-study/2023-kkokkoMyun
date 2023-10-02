## Q. TCP와 UDP의 차이에 대해 설명해 주세요.

## A. TCP는 연결 지향적이고 신뢰성 있는 데이터 전송을 제공하며, 연결 설정 및 관리를 수행합니다. UDP는 연결 없이 빠르게 데이터를 전송하지만, 데이터 손실이나 순서 뒤섞임이 발생할 수 있습니다.




### TCP(Transmission Control Protocol)

네트워크 통신을 위한 프로토콜

1. 연결 지향성 (Connection-Oriented): 데이터 전송 전에 연결 설정 과정을 거친 후, 데이터를 안정적으로 전송합니다.

2. 신뢰성 (Reliable): 데이터를 손실 없이 전달하며, 전송된 데이터의 순서를 보장하여 정확한 재조립을 가능하게 합니다.

3. 흐름 제어 (Flow Control): 데이터의 효율적인 전송을 위해 수신 측이 데이터를 받을 수 있는 속도로 송신 측의 데이터 전송 속도를 조절합니다.

4. 혼잡 제어 (Congestion Control): 네트워크 혼잡을 방지하기 위해 데이터의 전송 속도를 동적으로 조절하여 네트워크 부하를 관리합니다.

5. 핸드셰이크 (Handshake): 연결 설정을 위해 클라이언트와 서버 간에 3단계의 핸드셰이크 과정을 수행하고, 해제할 때는 4단계의 핸드셰이크 과정을 수행합니다.

### UDP (User Datagram Protocol)

1. 연결 없음 (Connectionless): 연결 설정 과정 없이 데이터를 즉시 전송합니다.

2. 비신뢰적 (Unreliable): 데이터 손실이나 순서 뒤섞임이 발생할 수 있으며, 재전송 기능을 제공하지 않습니다.

3. 흐름 제어 및 혼잡 제어 없음: 데이터의 전송 속도를 제어하거나 네트워크 혼잡을 관리하지 않습니다.

4. 경량 (Lightweight): TCP에 비해 오버헤드가 적으며, 실시간 응용 프로그램 및 빠른 데이터 전송에 적합합니다.

5. 단방향 또는 다중 방향 통신: 다수의 클라이언트에 데이터를 동시에 전송할 수 있고, 응답을 기다리지 않고 다음 데이터를 보낼 수 있습니다.

## 꼬리 질문

### 왜 HTTP는 TCP를 사용하나요?

<details>
<summary></summary>
<div markdown="1">

- TCP는 신뢰성 있는 연결 기반 프로토콜이므로, HTTP의 요청과 응답의 신뢰성과 순서를 보장하는데 적합.
- 안정적이고 신뢰성 있는 데이터 전송을 보장(신뢰성, 연결 지향성)

</div>
</details>

### 왜 DNS는 UDP를 사용하나요?

<details>
<summary></summary>
<div markdown="1">

- 작은 패킷 크기: Request의 양이 적어서 충분히 UDP 패킷 안에 담을 수 있음.
- 간단한 요청-응답 모델이기 때문에 굳이 핸드셰이킹을 거칠 필요 없음.

</div>
</details>

### Checksum이 무엇인가요?

<details>
<summary></summary>
<div markdown="1">

- 데이터의 무결성을 검사하기 위해 사용되는 값.
- 데이터의 모든 비트를 더하거나, 비트 연산을 수행하여 생성.
- 오류 탐지만 가능하고 수정은 불가능
- TCP, UDP 모두 헤더에 체크섬 필드 포함됨.

</div>
</details>

### TCP의 흐름 제어가 무엇인지 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- 송신측과 수신측의 데이터 처리 속도 차이 해결 기법
- 수신자가 패킷을 지나치게 많이 받지 않도록 조절하는 것.
- 수신자가 송신자에게 현재 자신의 상태를 알림 -> 이에 따라 데이터 전송량 조절

- 제어 기법으로는 Stop and Wait, Sliding Window 등이 있다.

</div>
</details>

### TCP의 혼잡 제어가 무엇인지 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- 데이터의 전송 속도를 조절하여 네트워크 부하를 관리하는 방법
- 라우터가 처리하지 못한 데이터를 손실 데이터로 간주 -> 계속 재전송하여 네트워크를 혼잡하게 함
- 네트워크 내의 패킷 수를 조절하여 오버플로우를 방지

- 제어 기법으로는 Slow Start, AIMD, Fast Retransmission, Fast Recovery 등이 있다.

</div>
</details>

### 3-way HandShake에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- 클라이언트가 연결 요청 (SYN)
- 서버가 요청 받고 확인 메시지 전송 (ACK, SYN)
- 클라이언트도 서버의 메시지를 받았다는 것을 확인했다는 메시지 전송 (ACK)
- ACK, SYN 같은 값은 TCP 해더에 포함되어 전달

</div>
</details>

### 4-way HandShake에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- 클라이언트의 종료 요청 (FIN)
- 서버의 확인 응답 (ACK)
- 서버의 종료 요청 (FIN)
- 클라인트의 확인 응답 (ACK)

</div>
</details>


### 왜 4-way HandShaking 과정에서 종료 후에 가로 끝나지 않고 TIME_WAIT 상태로 대기하는 것일까요?

<details>
<summary></summary>
<div markdown="1">

1. 데이터 패킷 처리
    - 클라이언트나 서버가 종료된 후에도 재전송된 패킷을 받을 수 있음.
2. 연결 충돌 방지
    - 이전 연결의 잔여 패킷이 네트워크에서 사라질 때까지 대기하는 시간 제공
    - 잔여 패킷이 새로운 연결과 충돌하지 않도록 보장하는 역할
3. 정확한 연결 종료 확인
    - 상대방이 종료 절차를 완료했다는 확인 신호를 받을 수 있음.
    - 신뢰성 있는 연결 종료 보장.

</div>
</details>

### 4-Way Handshake 과정에서 중간에 한쪽 네트워크가 강제로 종료된다면, 반대쪽은 이를 어떻게 인식할 수 있을까요?

<details>
<summary></summary>
<div markdown="1">

1. 타임아웃
    - 클라이언트나 서버는 일정 시간 동안 ACK 패킷을 받지 못하면 타임아웃 발생 -> 이를 통해 상황 감지
2. 비정상적인 연결 해제 감지
    - 서버로부터 FIN 패킷을 받지 못하면 인식 가능.
3. 재전송 시도
    - 한 쪽이 강제로 종료되면, 남아있는 패킷을 재전송하여 상대방이 연결의 비정상적인 종료를 인식하도록 유도할 수 있음.

</div>
</details>

### 빨리 끊어야 할 경우엔, (즉, 4-way Handshake를 할 여유가 없다면) 어떻게 종료할 수 있을까요?

<details>
<summary></summary>
<div markdown="1">

- RTS 패킷을 사용하여 강제로 연결 종료 가능
- 받은 쪽은 즉시 연결 종료
- 데이터의 유실이 발생할 수도 있다.

</div>
</details>

### Half-Close 상태란 무엇인가요?

<details>
<summary></summary>
<div markdown="1">

- TCP 연결에서 한 쪽이 데이터 전송을 완료한 후 연결을 종료하는 상태를 말함
- 일방적인 데이터 전송이 완료되었을 때 유용하게 사용할 수 있다.
- 클라이언트가 서버에게 파일을 요청하여 받은 후, 서버는 파일을 모두 전송한 후에 연결을 종료할 수 있다.

</div>
</details>

### SYN Flooding에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- 네트워크 공격의 한 형태로, 공격자가 대상 서버로 대량의 SYN 패킷을 보낸다.
- 3-way handshaking의 절차를 악용하여 서버의 리소스를 고갈시키거나 서비스 거부 상태를 유발
- SYN 쿠키 사용 또는 패킷 필터링 및 방화벽 설정, 로드 밸런싱 등의 방지 기법 존재

</div>
</details>
