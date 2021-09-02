# Socket

socket은 커넥션이 성공했을 때 커넥션에 대한 정보를 담고 있는 변수.

- socket객체는 개별 클라이언트와의 interacting을 위한 기본적인 객체이다.
- io객체는 연결된 전체 클라이언트와의 interaction을 위한 객체

io.emit : 접속된 모든 클라이언트에게 메시지를 전송한다.

socket.emit : 메시지를 전송한 클라이언트에게만 메시지를 전송한다.

socket.broadcast.emit : 메시지를 전송한 클라이언트를 제외한 모든 클라이언트에게 메시지를 전송한다.

io.to(id).emit : 특정 클라이언트에게만 메시지를 전송한다.
id는 socket 객체의 id 속성값이다.