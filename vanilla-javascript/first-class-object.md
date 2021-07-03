# First Class Object

- 함수의 인자로 전달할 수 있거나
- 함수의 반환값으로 사용될 수 있거나
- 변수에 할당될 수 있고 자료구조에 저장될 수 있어야한다.

함수 또한 위 조건에 모두 해당하므로 일급객체이다. → ***일급 함수***

```jsx
const arr = [];

for (let i = 0; i < 3; i++) {
  arr.push(function foo () { // push라는 함수는 foo라는 함수를 인자로 받고 있다.
	  return function bar () {}; // bar함수는 반환값으로 사용되고 있다.
  });
}

console.log(arr); // arr라는 배열 자료구조 안에 함수를 저장하였다.
```
