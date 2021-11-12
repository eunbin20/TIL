# Web RTC 

[블로그 포스팅](https://euncoding.tistory.com/53)

웹 어플리케이션에서 텍스트 데이터나 영상, 음성 데이터를 클라이언트끼리 실시간으로 주고받을 수 있게 하는 기술이다.
WebRTC는 외부 소프트웨어나 플러그인 없이 클라이언트끼리 Peer-to-Peer 연결을 가능하게 하는 기술이다.

P2P 연결 과정

크게 Signaling, Connection으로 나누어지는데, 

우선 Signaling을 위해서는 클라이언트들이 데이터를 주고받기 위한 Signaling Server가 필요하다.

Signaling이 완료되고 Connection을 위해 P2P 통신을 위한 방법인 ICECandidate들을 주고받는다.

ICE는 Interactive Connectivity Establish의 약자로 P2P통신을 위한 최적의 방법을 찾는 프레임워크이다.
