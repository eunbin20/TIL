# React Hook


### Hook의 규칙

- 최상위에서만 Hook을 호출한다.

  - 반복문, 조건문, 중첩된 함수에서는 정의하지 않는다.
  (위와 같은 상황에서는 Hook이 호출되는 순서가 바뀔 수 있는데, Hook은 항상 동일한 순서로 호출되어야하기 때문이다.)

- React함수 내에서만 호출해야 한다.

- React는 Hook이 호출되는 순서에 의존한다.


1. useState : state변수를 React함수 안에서 사용할 수 있게함

```jsx
import React, { useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

1번 코드 : useState Hook을 React에서 가져온다

4번 코드 : useState함수를 호출해 반환값을 구조분해할당으로 변수에 저장한다.

useState함수의 반환값은 길이가 2인 배열로 첫 번째 값은 state변수, 두 번째 값은 state변수를 갱신하는 함수이다.

useState함수에 인자로 지정하는 값은 state변수의 초기값이 된다.

9번 코드 : setCount함수를 호출하여 count변수의 값을 갱신한다.



2. useEffect : side effect 수행
(side effect: 데이터 가져오기, 구독 설정하기, 수동으로 리액트 컴포넌트 DOM 수정,,,)

- class 컴포넌트에서 componentDidMount, componentDidUpdate, componentWillUnmount가 함쳐진 것과 동일한 동작을 한다.

- 컴포넌트가 렌더링 이후 어떤 일을 수행해야하는지 정의

- 리액트는 useEffect내에 정의한 함수를 기억했다가 DOM업데이트를 수행한 이후에 호출한다.

- 첫번째 렌더링을 포함해 이후의 모든 업데이트에서 수행된다.

- 리렌더링 할 때마다 모두 이전과 다른 effect로 교체하여 전달된다.

- (이해안됨)effect는 동기적으로 실행될 필요가 없다. 동기적 수행이 필요하다면 useLayoutEffect사용

- 외부 데이터에 구독(subscription)을 설정해야 하는 경우
  - 메모리 누수가 발생하지 않도록 정리(이벤트요소 삭제, 구독 제거)가 필요하다.
  - 해당 동작을 하는 함수를 반환값으로 넘겨준다.

```jsx
import React, {useState, useEffect} from 'react';

function Example() {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
        setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);

    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  return isOnline ? 'Online' : 'Offline';
}
```

useEffect 내부 함수 : 앱이 렌더링될 때마다 실행되는 함수

useEffect에서 반환하는 함수 : 컴포넌트가 마운트 해제될 때 실행되는 함수.
