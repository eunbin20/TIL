# useMemo Hook

- lodash의 memoize와 유사한 기능. 어떤 함수의 연산값을 memoize한다.

```jsx
const result = ueseMemo(() => computeExpensiveValue(a, b), [a, b]);

```
- "create" 함수와 dependency 배열을 인자로 받고 dependency의 값이 바뀔 때만 다시 실행된다. 이를 통해 복잡한 계산이 필요한 함수가 렌더링될 때마다 실행되는 것을 방지해준다.

- useMemo에 전달된 함수는 렌더링 중에 실행되므로, 일반적으로 렌더링하는 동안 실행되지 않는 작업은 수행하지 않아야 한다. 예를 들어 sideEffect의 경우 useEffect에 속해있어야지 useMemo에 속해서는 안된다.

- You rely on useMome as a performance potimization, not as a semantic guarantee.

- 리액트 컴포넌트의 생명주기에 따라 리렌더링될 때 변경사항을 확인하는 과정(shallow comparison)에서 의도치 않게 변화를 감지하는 경우가 존재한다. 이 경우 불필요한 렌더링이 발생할 수 있는데, useMemo를 이용해 이러한 불필요한 렌더링을 방지할 수 있다.

- 성능 최적화

- useMemo vs. React.memo()
  - useMemo : React hook, 함수를 컴포넌트 내부에 감싼다. 해당 함수 내부의 값은 dependency의 값이 변할 때만 recompute된다. 
  - React.memo() : Higher order component, 해당 컴포넌트 내부의 props가 변하지 않는 한 리렌더링되지 않도록 컴포넌트를 감싼다.
