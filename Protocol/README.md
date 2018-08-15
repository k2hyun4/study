## 프로토콜
* 통신체계
### 대표적 프로토콜 정의 기관
* ISO, IEEE 등

### SSH(Secure Shell)
* 원격 로그인, 파일 전송 등에 사용되는 프로토콜 or 응용프로그램
* 기본 포트 : 22번

### puTTY
* SSH, 텔넷 등을 위한 클라이언트

## TCP 3-way-handshake, 4-way-handshake
### 연결 성립(3-way-handshake)
1. 클라이언트가 서버에 접속을 요청. SYN(a) 패킷 전송
2. 서버가 클라이언트에 요청수락 및 송수신확인. ACK(a+1), SYN(b) 패킷 전송
3. 클라이언트가 서버에 응답. ACK(b+1)

### 연결 해제(4-way-handshake)
1. 클라이언트가 서버에 연결 종료 선언. FIN
2. 서버가 클라이언트에 OKAY 싸인. ACK
* 데이터를 모두 보낼 때까지 대기. TIME_OUT
3. 서버가 클라이언트에 통신 종료 안내. FIN
4. 클라이언트가 서버에 메세지 확인 알림. ACK
* 서버는 소켓 연결 close
* 클라이언트는 못받은 데이터를 대비해 일정 시간 세션 유지. TIME_WAIT

### Reference
* http://asfirstalways.tistory.com/356

***

## TCP/IP
* 데이터의 순서 유지, 유실 방지, 빠른 전송을 위한 네트워크 프로토콜
### 주요 성질
1. Connection oriented
* 로컬-리모트 사이에 연결을 맺고 데이터를 주고 받는다.
2. Bidirectional byte stream
3. In-order delivery
* 송수신 순서가 변경되지 않는다. 순서는 32-bit 정수 자료형을 이용해 표시한다.
4. Reliability through ACK
5. Flow control
* 수신자가 자신이 받을 수 있는 바이트 수(사용하지 않은 버퍼 크기. receive window)를 송신자에게 전달, 
송신자는 그만큼의 데이터를 전달한다.
6. Congestion control
* 송신자가 네트워크 정체를 방지하기 위해 유입되는 데이터양을 제한

### 데이터 전송
1. 레이어 구분
* User(Application)
* Kernel(File, Sockets, TCP, IP, Ethernet, Driver)
* Device(NIC)

2. Host = User + Kernel

### Reference
* https://d2.naver.com/helloworld/47667

## TLS, SSL
* Transport Layer Security
* Secure Sockets Layer
* 통신 과정에서 전송계층 종단간 보안과 데이터 무결성을 확보해줌
