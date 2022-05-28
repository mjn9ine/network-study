# [HTTP] 🌐인터넷 네트워크

## 🤔인터넷에서 컴퓨터는 어떻게 통신할까?

만약 _**클라이언트와 서버가 물리적으로 연결되어 있다면**_ 케이블을 이용해서 서로 통신할 수 있다.  
그렇지 않고 _**인터넷을 이용한다면**_ 수많은 중간 노드(서버)를 거쳐서 통신해야 한다.  
이 때 보내려는 메시지가 어떠한 규칙으로 어떻게 넘어갈 수 있을지 알기 위해서 `IP(인터넷 프로토콜)`을 이해해야 한다.

## 📍IP(인터넷 프로토콜)

복잡한 인터넷망을 통해서 컴퓨터끼리 통신하기 위해서는 최소한의 규칙이 있어야 한다.

먼저, IP 주소를 부여한다. 메시지를 보내는 클라이언트에 IP 주소를 부여하고 받는 서버도 마찬가지로 IP 주소가 있어야 한다.

#### IP의 역할

- 지정한 IP 주소(IP Address)에 데이터를 전달한다.
- 이 때, 패킷(Packet)이라는 통신 단위로 데이터를 전달한다.

#### IP 패킷의 정보(구성)

- 송신자 IP 주소, 수신자 IP 주소, etc...

#### 클라이언트 패킷 전달

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdlRr0f%2FbtrybW5tKXX%2FgsF8dtwJhGVpJqkwki8DdK%2Fimg.png)

1.  클라이언트가 IP 패킷을 인터넷 망에 던진다.
2.  인터넷 상의 서버들은 모두 IP 규약을 따르고 있기 때문에 해당 패킷의 정보를 이해할 수 있다.
3.  노드간에 목적지로 향할 수 있는 노드를 찾아가면서 패킷을 전달하고, 최종적으로 목적지에 도착한다. (라우팅)

#### 서버 패킷 전달

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHBDwk%2Fbtrx9BgYssc%2FE0yjEV2tZMBYrcWAlrQ7U0%2Fimg.png)

1.  클라이언트의 전달 과정과 같다.
2.  여기에서 클라이언트의 전달 경로와 다른 경로로 전달될 수 있다.

#### IP 프로토콜의 한계

- _**비연결성**_  
  : 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송 (잘못된 주소로 보내거나, 해당 컴퓨터가 꺼져 있을 수 있다.)
- _**비신뢰성**_  
  : 중간에 패킷이 사라질 수 있다. (물리적인 이유로 케이블이 소실될 가능성)  
  : 패킷이 순서대로 오지 않을 수 있다. (패킷의 용량이 클 경우 메시지를 끊어서 보내는데, 수신자가 내가 원하는 순서대로 받지 않을 수 있다.)
- _**프로그램 구분**_  
  : 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 하나가 아닐 수 있다.

IP 프로토콜 만으로는 위같은 한계를 해결할 수 없다. 그래서 이러한 문제를 해결해주는 `TCP 프로토콜`을 이용한다.

## 🖇️TCP, UDP

#### 인터넷 프로토콜 스택의 4계층

- 애플리캐이션 계층: `HTTP`, `FTP`
- 전송 계층: `TCP`, `UDP`
- 인터넷 계층: `IP`
- 네트워크 인터페이스 계층

#### 프로토콜 계층

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMyiRb%2FbtryccNI9pL%2FKbWlTXh9KTkO3YDapqV470%2Fimg.png)

#### TCP(전송 제어 프로토콜)의 특징

- **_연결지향 - TCP 3 way handshake(가상 연결)_**  
  위의 연결은 논리적(개념적)인 연결을 뜻한다. (중간에 수많은 서버들은 연결되었는지 아닌지 알 수 없다.)

  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGCr0W%2FbtrybXceU2i%2FJu5hErkrpBhg53MX6M50e0%2Fimg.png)

- **_데이터 전달 보증_**  
  TCP에서는 데이터를 수신하면 잘 수신했다는 확인 응답(ACK)을 해준다.

  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxZywg%2Fbtryaq6UICA%2FF4V4zJ7MtkM23iQQq6jmJ1%2Fimg.png)

- **_순서 보장_**  
  수신된 패킷이 순서대로 오지 않았다면 해당 패킷부터 재전송 요청한다.

  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbzmNig%2FbtrybLCXvxv%2FEmVKWKEUulj1zqLQ6OhdM0%2Fimg.png)

**⇒ 위의 특징이 가능한 이유: TCP 세그먼트 안에 전송 제어, 순서, 검증과 같은 정보가 추가되어 있다.**

- 신뢰할 수 있는 프로토콜
- 현재 대부분 TCP 사용

#### UDP(사용자 데이터그램 프로토콜)의 특징

- 기능이 거의 없다. (하얀 도화지와 같다.)
- 연결지향 - TCP 3 way handshake ❌
- 데이터 전달 보증 ❌
- 순서 보장 ❌
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠르다.
- IP와 거의 동일하다. (IP + PORT + CHECKSUM)  
  : IP로 여러 패킷이 수신될 때, PORT를 이용해서 구분한다. 이 메시지가 제대로 되어 있는지 검증하는 데이터가 체크섬.
- 애플리케이션에서 추가 작업이 필요하다.

###### 🙋 그러면 왜 UDP를 사용하는 걸까?

TCP에서는 3 way handshake을 통한 연결 과정에서 시간과 데이터의 크기가 커질 수 있다. 또한, 이미 인터넷이 TCP 기반으로 대부분 되어 있기 때문에 추가로 최적화 하기가 힘들다.

⇒ UDP는 아무 기능이 없는 도화지 같은 상태이기 때문에, 내가 원하는 대로 최적화가 가능하다. 최근에는, 3 way handshake의 과정까지 줄여보자는 취지로 급부상중이다.

## ⚓PORT

IP 주소만으로는 한 번에 여러개의 서버와 통신할 수 없다. **같은 IP 내에서 프로세스를 구분하기 위해서** `PORT`를 이용한다.  
IP가 _아파트_(목적지의 서버를 찾는 것)라면 PORT는 _동/호수_(서버 안에서 애플리케이션을 구분하는 것)로 비유할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbv4bsV%2FbtryciUzMmC%2FF5Wo9dbnwlLSkOebWYseZK%2Fimg.png)

<center>⇓</center>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLWd2f%2FbtrycPLjxwf%2FK6mnYkwYoMAJoDpOHCgoTk%2Fimg.png)

#### PORT의 특징

- 0 ~ 65535: 할당 가능
- 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋다.
  - FTP: 20, 21
  - TELNET: 23
  - HTTP: 80
  - HTTPS: 443

## DNS(Domain Name System)

IP 주소는 기억하기 어렵고, 바뀔 수 있다.  
⇒ 이를 해결하기 위해서, 도메인 명을 IP 주소로 변환하는 DNS를 사용한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdJKlYr%2FbtrycPExIIT%2F0BekmHYN7DLc3YEDouFJQ1%2Fimg.png)
