# Client side routing and Server side routing

- Server side routing

Server에서 라우팅하기 때문에 해당 페이지에 직접 접근하는 방식이다.

원하는 페이지로 이동하고자할 때 반드시 router를 사용해야 한다.

처음에 URL을 입력했을 때, 또는 페이지를 바꿀 때마다 라우팅이 일어나는데, 라우팅이 일어날 때마다 새로운 전체 페이지가 로드된다.

꽤 큰 용량의 작업이고 인터넷의 속도와 같은 다른 요인들이 필요하다.

- Client side routing

Client 내부에서 라우팅하는 방식으로 해당 페이지를 호출 시 root부터 해당 페이지까지 차례로 로딩된다.

처음 어플리케이션을 불러올 때는 서버로부터 웹 주소로 전체 react app을 로드해야한다.

그리고 하위 페이지를 호출할 경우 해당 컴포넌트의 부모 컴포넌트를 반드시 거쳐야 하므로 호율적인 설계가 필요하다.

하지만 그러고 나서는 페이지를 바꿀 때 HTML5 history API를 이용해 즉각적으로 변화를 탐지하여 처음에 로드되었던 어플리케이션으로부터 페이지를 fetch해온다.

single page application을 만드는 데 사용된다.

이 경우 페이지 변경시 어플리케이션을 swap out할 수 있다.
