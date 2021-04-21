# 2021년 4월 셋째주 TIL
오늘 내가 배운 것들(Today I Learned)

---------------------------------------
## 웹 기본과 비동기, 이벤트루프

<details open>
<summary>2021-04-19</summary>
<div markdown="1">

### 웹 기본 개념
서버와 클라이언트는 서로 정보를 주고받는다.

- 서버 : 어떤 정보를 관리하고 제공
- 클라이언트 : 서버에 어떤 정보를 요청. 즉 서버가 관리하는 자료에 접근할 수 있는 프로그램을 뜻함.
ex) 인터넷 브라우저, 휴대폰 어플리케이션
- IP Address(Internet Protocol Address) : 네트워크 상의 컴퓨터마다 할당되는 주소
ex) 192.168.0.3
(실제 주소지 - 서울특별시 00구 00동 ... )
- Domain : ip주소의 별명
ex) www.naver.com
(주소지의 이름 - '이마트 명일점'')

- DNS(Domain Name System) : 우리가 찾고자하는 도메인의 ip주소를 찾아주는 시스템

서버와 클라이언트가 정보를 주고받을 때 지켜야 하는 일련의 규칙이 있다.
- HTTP(Hypertext Transfer Protocol)
HTTP Request / HTTP Response
</div>
</details>
