# Prop types

[블로그 포스팅](https://euncoding.tistory.com/50)

## React props

리액트에서는 자바스크립트의 함수를 호출할 때 매개변수를 전달하는 것 처럼 데이터(숫자, 문자열, 함수, 객체, 배열 등등)를 전달할 수 있다. 

그러나 컴포넌트가 잘못된 타입의 props를 받으면 bug가 발생하게 되고 에러가 발생해 애플리케이션이 중단된다.

자바스크립트에는 내장되어있는 타입 체크 솔루션이 없기 때문에, 많은 개발자들은 TypeScript와 Flow와 같은 extention들을 사용하지만, 리액트에는 props의 유효성을 검사하기 위한 내부적인 매커니즘인 PropTypes가 있다.

## TypeProps

리액트 애플리케이션을 개발할 때, 어떤 prop이 정의되지 않으면 적절하게 렌더링되지 않기 때문에 필수적으로 prop을 정의해야하는 경우가 있다. 

props가 리액트의 컴포넌트로 전달되면, propTypes의 속성으로 설정된 타입의 정의와 맞는지 확인하고, 적절하지 않은 값이 prop으로 전달되면, console에 경고메세지가 나온다.


컴포넌트 내에 default props가 정의되어있다면, 해당 값은 적용되기 전에 propTypes를 통해 타입을 확인한다.

즉, default props 또한 propTypes가 적용된다.

다음은 간단한 proptype에 대한 예시이다.

```jsx
// basic types

Component.propTypes = {
  anyProp: PropTypes.any, // 모든 값
  booleanProp: PropTypes.bool,
  numberProp: PropTypes.number,
  stringProp: PropTypes.string,
  functionProp: PRopTypes.func
}

// renderable types

Component.propTypes = {
  nodeProp: PropTypes.node, // 리액트로 렌더링될 수 있는 모든 값이 될 수 있다.
  elementProp: PropTypes.element // prop으로 리액트 엘레멘트가 올 수도 있다.
}
```
 

*  PropType.node에는 리액트로 렌더링될 수 있는 모든 값이 될 수 있다.

 '렌더링될 수 있는 값'이란 무엇일까?

 - 렌더링될 수 있는 값이란 `<div>{ value }<div>` 코드를 렌더링했을 때 화면에 출력되는 value을 말한다.  
`<div>{ true }</div>`, `<div>{ object }</div>`, `<div>{ function }</div>` 등의 값은 화면에 렌더링되지 않는다.

## 결론

애플리케이션이 커지고, 복잡해질수록 여러 컴포넌트들 간 props의 연결구조 또한 복잡해진다.

특히 개발의 규모가 커지고 다른 개발자들과 함께 작업을 하게되는 경우, 다른 개발자들이 나의 컴포넌트만을 봐서는 props로 전달받은 값 어떤 값인지 추정하기 어렵게 된다.

그러면 그 개발자는 이 컴포넌트가 어떤 다른 컴포넌트로부터 호출되었는지 다른 코드들을 모두 찾아봐야하는 일이 발생한다.


그래서 해당 컴포넌트 안에서 props로 받은 값이 어떤 값인지, 꼭 필요한 값인지 아닌지에 대해 명확히 정의할 필요성이 생기게 된다.

props는 해당 컴포넌트가 다른 컴포넌트에 의존해있는 부분이라고 볼 수 있다. 이러한 부분을 명확히 정의함으로써 해당 컴포넌트 내에서의 작업에 더 집중할 수 있게 되는 것 같다. 

