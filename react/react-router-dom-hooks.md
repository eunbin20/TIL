# React Rounter Dom Hooks

- useHistory : link to와 같은 역할로 url을 변경시킬 수 있다.
```jsx
import { useHistory, BrowserRouter as Router, Route } from "react-router-dom";

const App = () => {
  return (
    <Router>
      <Switch>
        <Route exact path="/about" component={About} />
        <Route exact path="/skills" component={Skills} />
        <Route exact path="/project" component={Project} />
        <Route parh="/" render={() => <Redirect to="about" />} />
      </Switch>
    </Router>
  );
};
// About, Skills, Project 컴포넌트의 defaultProps에는 history객체가 들어가고 이 history객체를 이용하여 리액트 어플리케이션 내에서 라우팅 가능

// 그 history객체를 대체하는 것이 useHistory

const Buttons = () => {
  const history = useHistory();

  return (
    <div>
      <button onClick={() => history.push("/about")}>About</button>
      <button onClick={() => history.push("/skills")}>Skills</button>
      <button onClick={() => history.push("/projects")}>Projects</button>
    </div>
  )
}
```

- useLocation : 사용자가 현재 머물러있는 페이지에 대한 정보를 알려주는 hooks. defaultProps의 하나인 location객체를 대체하는 react-router-dom hooks

```jsx
import React from 'react';
import { useLocation } from 'react-router-dom';
import queryString from 'query-string';

const Home = (): JSX.Element => {
  const { search } = useLocation();
  // search: ?keyword=리액트

  const { keyword } = queryString.parse(search);
  // keyword 출력결과: "리액트"

  return (
    <></>
  );
}

export default Home;
```

- useParams : path parameter의 정보를 얻을 수 있는 hooks
  동적 라우팅 필요.
  <Route exact path="/home/:id" component={Home} />
  => /home/뒤에 1이 오든, 2가 오든, 문자열이 오든 상관없이 라우팅이 작동

