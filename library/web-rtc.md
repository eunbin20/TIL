# Web RTC with simple peer

### WebRTC(Web Real-Time Communications)란?

웹 어플리케이션에서 음성, 영상, 또는 텍스트 파일과 같은 데이터를 브라우저끼리 실시간으로 주고 받을 수 있게 만든 기술이다.

WebRTC를 이용하면 외부 소프트웨어나 플러그인을 설치할 필요 없이 데이터를 공유할 수 있고 peer-to-peer 화상회의가 가능하다.

### WebRTC 핵심 개념들: NAT, STUN, TURN, ICE

**NAT(Network Address Translation)**

![https://blog.kakaocdn.net/dn/pH5eM/btrj7RCFYD2/DVpcYxIg4wkfzDwWAv4bzK/img.jpg](https://blog.kakaocdn.net/dn/pH5eM/btrj7RCFYD2/DVpcYxIg4wkfzDwWAv4bzK/img.jpg)

NAT은 **PrivateIP와 PublicIP를 1대1 대응시켜 변환**하는 장치를 말한다.예를 들어 wifi환경과 같이 publicIP가 존재하고 공유기 내부에서는 privateIP를 이용하여 구분할 때, 공유기에서 publicIP를 privateIP로 매핑시켜주는 환경을 의미한다. 그러나 P2P로 연결되어야하는 WebRTC에서는 직접적으로 IP를 연결해야하기 때문에 방화벽이 존재하거나 라우터를 사용하는 NAT환경에서는 연결이 불가능하다. 이 연결을 가능하게하기위해 **STUN서버** 또는 **TURN서버**가 필요하다.

**STUN(Session Tracersal Utilities for NAT)**

![https://blog.kakaocdn.net/dn/4bZa4/btrkobu54Se/wCrY9E31ek8a3WSXSD0AK1/img.jpg](https://blog.kakaocdn.net/dn/4bZa4/btrkobu54Se/wCrY9E31ek8a3WSXSD0AK1/img.jpg)

보통 PublicIP인 공유기에는 여러 PrivateIP주소가 내부적으로 라우팅되어있다. 공유기에 연결된 디바이스들은 자신의 PublicIP주소를 모른다. STUN Server는 기기의 Public IP 주소를 알려주는 역할을 한다. 클라이언트는 자신이 받은 Public IP를 이용하여 시그널링을 할 수 있다.

하지만 STUN은 항상 효과적이지 않다. 두 단말이 같은 NAT환경에 있는 경우 또는 NAT의 보안 정책이 엄격한 경우에는 STUN Server를 이용하여 연결할 수 없다.

**TURN(Tranersal Using Relays around NAT)**

![https://blog.kakaocdn.net/dn/dmxiSx/btrkkXdo44h/H8h6WDmqVImfwviWEJ5FZ1/img.jpg](https://blog.kakaocdn.net/dn/dmxiSx/btrkkXdo44h/H8h6WDmqVImfwviWEJ5FZ1/img.jpg)

STUN 서버의 확장으로 NAT환경에서 릴레이하여 통신하게 된다. 이 방법은 다른 방법이 모두 실패했을 때 실행되는 대안적인 방법으로, 오버헤드가 발생하므로 권장되지 않는 방법이다.

**ICE(Interactive Connectivity Establishment)** 

ICE는 Client가 통신 가능한 모든 주소들을 찾는 프레임워크

> ICE는 먼저 장치의 OS와 네트워크 카드에서 얻은 호스트 주소를 사용하여 연결을 시도합니다.(UDP > TCP)
이 작업이 실패할 경우(NAT 뒤에 있는 장치의 경우), ICE는 STUN 서버를 사용하여 외부 주소를 가져옵니다.
이 작업이 실패하면 트래픽이 TURN 릴레이 서버를 통해 라우팅됩니다.
> 

이 각각의 주소들이 ICECandidate이다. 이 주소들 중 가장 최적의 경로를 찾아서 연결시켜준다.

### WebRTC를 이용한 P2P연결 과정

연결 과정을 간략하게 살펴보면 다음과 같다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9bcd975-4f93-4469-9716-400642411be1/Untitled.png)

<Signaling>

1. PeerA는 createOffer()를 통해 먼저 자신의 SessionDescription을 생성하고 Signaling Server를 통해 PeerB에게 전달한다.

2. PeerB가 PeerA의 SessionDescription을 전달받고 이에 대한 답으로 createAnswer()을 통해 자신의 SessionDescription을 생성하고 Signaling Server를 통해 PeerA에 전달한다.

<Connection>

3. PeerA와 PeerB 모두 자신의 ICECandidate 정보를 생성하기 시작하고 이를 Signaling Server를 통해 각각 서로에게 전달한다.

4. 서로의 MediaStream을 peer 간 통신으로 주고받는다. (만약 PeerA과 PeerB 둘 중 Symmetric NAT을 가진 Peer가 있는 경우 TURN 서버를 사용해 data relay로 연결을 진행해야 한다.)

### **1. Signaling(hand shaking)**

Signaling은 Peer to Peer 통신을 위해 각각의 peer가 서로 메타데이터를 주고받음으로써 멀티미디어 스트림을 주고받을 수 있게 연결된 것을 의미한다. 메타데이터에는 코덱, 대역폭 등 데이터의 포맷과 네트워크 데이터(IP주소, 포트 번호 등)등의 정보가 들어있다. 즉 **Signaling은 두 peer가 통신을 진행하기 위해 협의하는 단계**라고 볼 수 있다.

![https://blog.kakaocdn.net/dn/WxmzW/btrj3MPS5Ee/MNVHZZFsCcNUYPB2BWvcm0/img.png](https://blog.kakaocdn.net/dn/WxmzW/btrj3MPS5Ee/MNVHZZFsCcNUYPB2BWvcm0/img.png)

쉽게 설명하자면, 예를 들어 PeerA와 PeerB가 있다고 해보자.

먼저 PeerA는 PeerB에게 본인의 멀티미디어 컨텐츠와 ip주소 대한 메타데이터가 적혀있는 메시지를 보낸다. 이 메시지는 우리 Signaling하자는 **'제안(offer)'**이다.

PeerA의 메시지를 받은 PeerB는 PeerA에게 본인의 멀티미디어 컨텐츠와 ip주소에 대한 메타데이터가 적혀있는 메시지를 보낸다. 이 메시지는 Signaling 제안을 받아들이겠다는 **'답장(answer)'**이다. 이렇게 **두 Peer가 'offer'와 'answer'을 주고받으면 Signaling**이 완료된다.

두 peer가 서로 주고받는 메타데이터는 **SDP방식**으로 통신한다. 또한 메타 데이터들(offer, answer)을 주고받기위해서는 **Signaling Server**가 필요하다.

- **SDP(Session Description Protocol)** peer연결을 위해 주고받는 멀티미디어 컨텐츠의 규격(해상도, 포맷, 코덱 등)의 표준을 말한다. 멀티미디어 컨텐츠 데이터가 아닌 **컨텐츠의 메타데이터**이다.
- **Signaling Server** WebRTC에서는 이 signaling을 위한 메커니즘은 제공하지 않기 때문에 signaling을 위한 서버가 필요하다. Signaling Server가 해야하는 일은 각각의 Peer가 SDP방식으로 서로 메타데이터를 주고받게해주는 것이다. 그 방법은 개발자가 필요에 따라 자유롭게 선택할 수 있다. 예를 들어 [appr.tc](http://appr.tc/) 에서는 XHR과 Channel API를 사용해 Signaling을 구현했고, 구글 코드랩에서는 Node 서버 위에 [socket.io](http://socket.io/) 를 사용해서 만들었다.

나는 socket.io를 이용한 웹소켓을 통해 Signaling Server을 구현하였다.

### **2. Connection**

Signaling을 통해 SDP를 결정한 후에 ICE Candidate들을 교환한다. ICE Candidate는 어떻게 통신하는지에 대한 방법이며 통신 방법들은 검색되는 순서대로 상대 Peer로 보내진다. 그 중 최적의 방법(UDP > TCP > STUN > TURN(relay)순으로 시도)으로 통신이 진행되면 최종적으로 두 Peer간의 연결이 완료된다.

이후에는 서로의 음성/영상 스트림과 같은 데이터들을 실시간으로 주고받을 수 있게 된다.

여기까지 WebRTC api를 이용해 P2P연결을 구현하는 과정을 알아보았다. 매우 복잡하다...