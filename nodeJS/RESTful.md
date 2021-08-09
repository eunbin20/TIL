# RESTful

[블로그 포스팅](https://euncoding.tistory.com/52)

## REST(REpresentational State Transfer)

HTTP 창시자 중 한 사람인 Roy T. Fielding은 개발자들이 웹을 사용할 때 본래 설계의 우수성을 잘 사용하지 못하고 있다고 판단했고, 웹의 점을 최대한 활용할 수 있는 네트워크 기반의 아키텍쳐인 REST를 처음 소개한다.

- REST의 정의

> **a way of providing interoperability between computer systems on the Internet.**
컴퓨터 시스템과 인터넷 간의 상호 운용성을 제공하는 방법(위키피디아)

> **REST는 웹과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처 스타일을 말한다.**

* 하이퍼 미디어 시스템 = 다른 문서로 이동할 수 있는 하이퍼링크를 가지면서 그 내부에 텍스트와 음성, 영상을 비롯한 다양한 멀티미디어 데이터를 가지는 시스템

* 아키텍처 스타일 = 자원을 정의하고 자원에 대한 주소를 지정하는 방법 등을 포함하는 제약조건의 집합

즉, REST는 분산 하이퍼 미디어 시스템에서 데이터를 정의하고 하이퍼링크를 통해 해당 데이터의 주소를 지정하는 방법 또는 제약 조건의 한 종류이다. REST는 HTTP URI(Uniform Resource Identifier)을 통해 자원을 명시하고, HTTP METHOD(POST, GET, PUT, DELETE)를 통해 해당 자원을 처리하도록 설계되었다.


### REST API란, REST에서 정의한 제약조건을 모두 지키는 API를 말한다.

제약 조건은 다음과 같다.

1. Client-Server
client와 server에 대한 분명해야 한다. 
UI와 요청 수집은 **client의 영역**이고 비즈니스 로직을 처리, 저장하고 보안과 관련된 영역은 **server의 영역**이다. 
이러한 역할의 분리를 통해 이 두 영역은 서로 독립적으로 개발되고 향상된다. 
2. Stateless(무상태성)
무상태성의 의미는 사용자나 클라이언트의 세션과 쿠키와 같은 context를 서버쪽과 별개로 관리한다는 의미로 서버측에서는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
이를 통해 서버의 처리 방식이 일관적이고 구현이 단순해진다.
3. Cacheable
HTTP프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다. 즉, HTTP의 특징 중 하나인 캐싱 기능을 적용할 수 있다.
캐시 사용을 통해 응답 시간이 빨라지고 REST 서버 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
4. Uniform Interface
- Identification of resource : URI로 리소스가 식별되어야 한다.
- Manipulation of resources through representations : 표현(representation)전송을 통해 리소스를 조작해야 한다.  
즉, 리소스를 만들거나 삭제, 수정할 때 http 메시지에 그 표현을 전송해야 한다.
- **self-descriptive messages** 
- **hypermedia as the engine of application state(HATEOAS)**
5. Layered System(계층화)
REST 서버는 요청된 정보를 검색하는 서버(보안, 로드 밸런싱 등)의 각 유형을 클라이언트가 볼 수 없는 다중 계층으로 구성될 수 있다.
6. Code-on-Demand(optional)
서버에서 코드를 클라이언트로 보내서 실행할 수 있어야 한다는 것을 의미한다. 즉, 자바스크립트를 의미한다.

대부분의 조건은 http프로토콜을 따르면 자동으로 지켜지는 조건들이다. 그러나 self-descriptive message와 HATEOAS는 REST api로 알려져 있는 대부분의 api들이 만족하지 못하는 조건들이다. 이 두 가지 조건에 대해 자세히 알아보자.

- Self-descriptive message

메시지는 스스로를 설명해야 한다.

다음과 같은 요청을 보자.

```html
GET / HTTP/1.1 
```

이 메세지에는 목적지가 빠져있다. 

```html
GET / HTTP/1.1
Host: www.example.org
```

이 요청이 www.example.org라는 도메인으로 이동한다는 목적지가 추가되었다. 이제 self-descriptive하다.

```html
HTTP/1.1 200 OK
[ { "op": "remove", "path": "a/b/c" } ]
```

위 메시지는 self-descriptive하지 않다. 그 이유는 이 메시지는 클라이언트가 해석하려고 하면, 어떤 문법으로 작성된 것인지 모르기 때문에 해석에 실패한다. 그렇기 때문에 요청 body가 어떤 문법으로 쓰인것인지에 대해 헤더의 Content-type속성이 반드시 추가되어야 한다.

```html
HTTP/1.1 200 OK
Content-Type: application/json

[ { "op": "remove", "path": "/a/b/c" } ]
```

이제 클라이언트측에서는 reponse의 body가 json 문법으로 사용되었다는 것을 알게 되었고 대괄호, 중괄호, 큰따옴표의 의미가 무엇인지 알게 되었다. 

이제 self-descriptive하다고 볼 수 있는가? 아니다.

클라이언트는 아직 "op"가 무슨 뜻이고, "path"가 무엇을 의미하는지 알 수 없다. 즉 self-descriptive하지 않다.

이 메시지를 self-descriptive하게 만들려면 각각의 키와 값이 어떤 것을 의미하는지도 해석할 수 있는 명세가 헤더에서 제공되어야 한다.

```html
HTTP/1.1 200 OK
Content-Type: application/json-patch+json

[ {"op": "remove", "path": "/a/b/c" } ]
```

json-patch+json에는 위 메시지에 포함되어있는 키와 값이 각각 무엇을 의미하는지에 대한 명세가 담겨있다. 즉 위 http메시지는 self-descriptive하다.

이처럼 self-descriptive하다는 것은 http메시지만 봤을 때 해당 메시지에 담긴 정보를 이용해 메시지의 의미를 온전하게 해석할 수 있어야 한다는 것이다.

그러나 오늘날의 REST API라고 부르는 많은 API들은 대부분 이 조건을 만족하고있지 않다. 대부분 json형태의 메시지를 보내면 Content-Type의 속성으로 json/application이 정의되어있다.

- HATEOAS(Hypermedia as the engine of application state)

애플리케이션의 상태는 Hyperlink를 이용해 전이되어야 한다.

html의 경우에는 이 조건을 만족한다.

```html
HTTP/1.1 200 OK
Content-Type: text/html

<html>
  <head></head>
	<body> <a href = "/test"> test</a> </body>
</html>
```

a 태그를 통해 하이퍼링크가 정의되어있고, 이 링크를 통해 그 다음 상태로 전이가 가능하다.

json의 경우는 어떨까?

```html
HTTP/1.1 200 OK
Content-Type: application/json
Link: </articles/1>; rel="previous", 
			</articles/3>; rel="next";
{
	title: "The second article",
	content: "hi"
}
```

header의 Link라는 속성은 이 리소스와 하이퍼링크로 연결되어있는 다른 리소스를 가르킬 수 있는 기능을 제공해준다.

위의 특징들을 잘 충족하면 Uniform Interface조건을 만족할수 있다. 그렇다면 이 Uniform Interface를 왜 충족시켜야하는가?

</br>

### 독립적 진화

REST라는 아키텍처를 도입하게 된 배경에는 웹(클라이언트)을 망가뜨리지 않고 HTTP(서버)를 업데이트할 수 있나?라는 의문이 있었다. 서버와 클라이언트가 각각 독립적으로 진화한다면 서버에 새로운 기능이 추가되거나 기능이 바뀌어도 클라이언트는 문제없이 실행될 것이다.

그렇기 때문에 REST의 가장 큰 목적은 서버와 클라이언트의 독립적 진화이다.

self-descriptive를 만족하는 api에서는 서버나 클라이언트가 변경되더라도 오고가는 메시지는 언제나 그 자체만으로 해석이 가능하다.

어플리케이션에서 하이퍼링크를 통해 어느 곳으로 전이가 가능한지는 미리 결정되는 것이 아니다. 어떤 상태로 전이가 완료되어야 그 다음 전이될 수 있는 상태가 결정된다. 즉 링크는 동적으로 변경될 수 있다. 따라서 HATEOAS를 만족하면 어플리케이션의 상태가 전이될 때마다 응답 메시지에 하이퍼링크의 주소가 지정되므로 클라이언트 측에서는 서버와는 독립적으로 자유롭게 리소스를 요청할 수 있게 된다.

**독립적 진화**는 self-description와 HATEOAS를 반드시 만족해야 구현될 수 있는 특징이기 때문에 이를 만족하지 못하면 RESTful하다고 볼 수 없는 것이다.

</br>

## REST API를 구현하기 어려운 이유

웹과 HTTP API를 비교해보자. 웹은 사람이 서버에 요청을 하면 서버에서 html파일을 응답함으로써 동작한다. 그러나 HTTP API는 HTTP를 사용해서 서로 정해둔 스펙으로 데이터를 교환하는 방식으로 동작하고 주고받는 데이터의 형식은 주로 JSON형태이다.

HTML과 JSON을 비교해보자.

먼저 http가 어떻게 self-descriptive와 HATEOAS를 만족하고있는지 살펴보자.

```html
GET /todos HTTP/1.1
Host: example.org
```

클라이언트측에서 위와 같이 GET요청을 서버로 보냈다.

```html
HTTP/1.1 200 OK
Content-Type: text/html

<html>
  <head></head>
  <body>
    <a href="http://todos/1"> 회사 가기</a>
    <a href="http://todos/2"> 집에 가기</a>
  </body>
</html> 
```

서버로부터 위와 같은 응답 메시지를 받았다.

- self-descriptive 
Content-Type을 보고 미디어타입을 확인→ text/html에 대한 명세를 보고 이를 해석하여 사용자에게 보여줌
- HATEOAS
a태그를 이용해 표현된 하이퍼링크가 다음으로 전이될 상태에 대한 정보를 담고 있으므로 만족

이제 JSON의 경우를 살펴보자.

```html
GET /todos HTTP/1.1
Host: example.org
```

클라이언트로부터 다음과 같은 요청을 받았다.

```html
HTTP/1.1 200 OK
Content-Type: application/json

[
  {"id": 1, "title": "회사가기"}
  {"id": 2, "title": "집에 가기"}
]
```

서버로부터 다음과 같은 응답 메시지를 받았다.

- self-descriptive
  Content-Type을 보고 미디어 타입이 application/json임을 확인 → 명세를 보고 해석
  그러나 "id"가 무엇을 뜻하는 값인지, "title"이 무엇을 뜻하는 값인지는 모름.
  ⇒ 실패
- HATEOAS
  다음 상태로 전이할 링크에 대해 정의되어있지 않음
  ⇒ 실패

## REST API로 바꾸는 방법

- self-descriptive
- custom media type 정의하기: json문서를 작성하고 해당 문서의 각 키와 값이 어떤 값을 뜻하는지에 대한 명세를 담은 문서를 등록.

  그러나 이 방법은 매 문서마다 media type문서를 정의해야하므로 시간이 오래 걸리고 비효율적임.

- Profile 이용하기: 헤더에 Link속성으로 profile relation으로 명세를 연결하면 응답 메시지만으로 json파일을 해석할 수 있음

  이 방법은 client측에서 Link헤더와 profile을 이해해야하고 Content negotiation이 불가능하다.
- HATEOAS
- data내에서 다양한 방법으로 하이퍼링크를 표현한다. → 링크를 표현하는 방법을 직접 정의해야한다.
- json으로 하이퍼링크를 표현하는 방법을 정의한 명세를 활용한다. → 기존 API를 많이 고쳐야 한다.
- HTTP 헤더로 Link나 Location 활용

# 결론

### 오늘날의 대부분의 "REST API"는 사실 REST조건을 만족하지 않는다.

특히 self-descriptive와 HATEOAS를 만족하지 못하는데 이것은 미디어 타입의 차이(html/json)로 인해 발생한다. html은 별다른 로직 없이도 두 조건을 만족하지만 json은 두 조건을 만족하기 위해서는 부가적인 설정을 해줘야 한다. 

REST는 긴 시간에 걸쳐 진화하는 웹 어플리케이션을 위한 제약이며 REST를 따를 것인지는 API를 설계하는 이들이 스스로 결정할 수 있다.

다만, REST의 제약 조건을 모두 만족하는 API가 아니라면 "REST 를 만족하지 않는 API"를 뭐라고 부를지 결정해야한다.

</br>

### 그렇다면, RESTful하지 않은 API를 REST API라고 이름 붙이는 것이 타당한가?

REST라는 용어를 쓰기 위해선 해당 개념이 어떤 목적으로 만들어졌는지를 생각해봐야한다. Roy F. Fielding은 웹을 망가뜨리지 않고 HTTP를 발전시키기 위해 서버와 클라이언트간에 독립적으로 진화할 수 있도록 REST를 만들었다. 즉, 웹만큼 규모가 크고 수많은 서버가 존재해 긴 시간(수십년)동안 진화해야하는 시스템이 아니라면 REST라는 규약을 지키면서까지 상호 운용성을 유지하지 않아도 된다는 것이다.

 사실 서버 API를 제대로 만들어 본 적이 없는 나로서는 RESTful한 API를 만든다는 것이 어떤 것인지 잘 모른다. 다만 최근 REST에 대한 여러가지 정보를 접하면서 API를 RESTful하게 만드는 방법이 분명 존재하는데도 많은 자칭 "RESTful"한 API들이 실제로 RESTful하지 않다는 것을 보면 API를 RESTful하게 만드는 것은 매우 비효율적이고 불필요한 작업이 될 것 같다는 추측이 들 뿐이다.

 또한 어딘가에는 실제로 RESTful한 REST API도 존재할 것이기 때문에 그런 API와 그렇지 않은 API 사이에 혼동이 발생할 것 같기도 하다.

 나는 로이 필딩 편이다! RESTful하지 않은 API를 REST API라고 칭하는 것은 해당 개념의 목적과 다르게 사용하는 것이고 또 왠만한 API는 RESTful하게까지 만들 필요성은 없다고 생각한다. 따라서 이러한 API에 대해서는 HTTP API라고 칭하거나 다른 새로운 이름을 붙여야 한다. 또는 REST라는 개념에 대한 재정의가 되어야 한다.(그러나 이렇게 되지는 않을 것같다..!)
