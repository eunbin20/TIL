# 2021년 4월 넷째주 TIL
오늘 내가 배운 것들(Today I Learned)

---------------------------------------
## 코딩테스트 대비 학습


<details open>
<summary>2021-04-26</summary>

1. fromPairs 메소드
key,value가 있는 배열을 인자로 받아 key-value로 구성된 객체를 반환

2. intersection 메소드
인자로 받은 모든 배열을 포함하는 고유한 배열 생성(unique). 순서와 결과값은 처 번째 배열로 정해진다.

- 간단한 조건문

1) 간단한 if문
조건이 성립했을 때의 결과문장이 간단한 경우 if문 뒤에 {}를 사용하지 않고 바로 작성할 수 있다.

  if (true) alert("true");

2) 삼항연산자
```jsx
(bookean표현식) ? (true일 때 문장) : (false일 때 문장);
```
3) 짧은 조건문
부울값이 아닌 피연산자를 반환하는 자바스크립트의 논리연산자의 특성을 이용하는 방법이다.


&&는 첫 false를 찾고 ||는 첫 true를 찾는다.


즉, &&의 좌항이 true면 우항을 실행하고 ||의 좌항이 false면 우항을 실행한다.



```jsx
// 1. <조건문> <조건문이 거짓일 때 실행될 코드>

tasks.length || finalCallback(results)

// 2. <조건문> && <조건문이 true일 때 실행할 코드>

(참 조건문) && (boolean표현식이 true일 때 실행할 문장)
```
3. sortedIndex(array, value)
array안에서 정렬시에 value가 들어가야 할 가장 작은 인덱스 값을 반환

4. curry

5. bind
앞에서 빼는거 shift()



</details>

<details open>
<summary>2021-04-27</summary>

#### function.length : 함수의 인자로 사용되어야하는 인자의 개수


```jsx
function func1() {}

function func2(a, b) {}

console.log(func1.length); // 0

console.log(func2.length); // 2
```


#### slice.call : 배열을 하나하나로 쪼개기


```jsx
arr = [1, 2, 3, 4, 5]

items = Array.prototype.slice.call(arr);
```

1. bind
2. bindKey

#### valueOf()
특정한 객체의 원시값을 반환한다.
객체를 원시값으로 바꾸기 위해 사용.
valurOf메소드를 스스로 실행할 일은 거의 없다.
js는 원시값이 필요한 객체를 만나면 자동적으로 실행한다.

#### Array.from
새로운 배열의 객체를 만드는 메서드

- Array.from(arrayLike, ([currentValue, [index, [array]]]) => { ... })
- Arrar.from(arrayLike, mapFn, thisArg)
1. arrayLike : 유사배열 또는 배열로 변환 가능한 반복 객체

2. mapFn : 배열의 모든 인자로 실행할 함수

3. thisArg : mapFn에서 this로 사용할 인자.



유사배열객체(문자)를 배열로 바꾸는 데 사용할 수 있는 메서드


```jsx
var str = "apple";
Array.from(str); // ["a", "p", "p", "l", "e"]

Array.from([1, 2, 3], x => x + x); // [2, 4, 6]
```
```jsx
Array.from(
  {length: 10},
  () => Array(5).fill(0)
  )
```
{length: 10}을 배열로 인식한다.

 왜냐면 배열도 원래는 오브젝트이다.

 객체에 length속성을 추가해주면 배열'처럼' 인식하게 되어 Array.from메서드를 통해 새로운 배열을 만들 수 있게 되는 것이다.

 * 객체에 length속성, iterator, Array 메소드 등을 추가해준 것이 배열!!

#### Node.contains()

상위노드.contains(하위노드) // true or false

#### String.includes()

배열.includes(요소) // true or false


#### Array.prototype.flat()

#### Array.prototype.reduce()
배열 각각의 요소에 reduser함수를 실행시켜 나오는 단일 값을 반환한다.
accumulator 존재 여부에 따라 첫 번째 값이 바뀌는데, accumulator가 존재하면 accumulator가 첫 번째 값이 되고 accumulator가 없으면 배열의 첫 번째 값이 첫 번째 값이 된다.

이전의 요소를 실행한 결과값이 다음 요소를 실행하는 함수에 포함되어 단일의 누적값이 반환된다.

#### Array.prototype.splice()

배열의 내용을 새로운 요소로 삭제하거나 대체한다



splice(start, [deleteCount], item,,,)
- start : 배열을 변경하기 시작할 인덱스
- deleteCount : start인덱스부터 시작해서 삭제할 요소의 개수
- item : start인덱스부터 시작해서 채워나갈 요소들

* for문은 배열의 순서를 제어할 수 있고 순회를 중단할 수 있다는 장점이 있지만 모든 배열을 순회할거라면 forEash를 사용하는 것이 좋다.

#### Array.prototype.forEach
forEach(function callback(currentValue, index, array) {

  }, thisArg)
  콜백함수로 화살표함수를 사용하는 경우 thisArgs는 생략된다.


#### Object.getOwnPropertyNames

오브젝트의 키값을 배열로 만들어 반환하는 메소드


#### value.Object.hasOwnProperty(key)


</details>

<details open>
<summary>2021-04-28</summary>

재귀 9 문제 풀었다 재귀의 신이 되었    ...
- array.forEach(function(item, index, array) {})
- for ... of (문자열, 유사배열, 배열)
- for ... in (객체)
for (const item of collection)    
for (let i = 0; i < 6; i++)    
위 두 코드에서 변수 선언 키워드의 차이가 생기는 이유는 i는 반복이 실행되면서 재할당되기 때문이다.


</details>


<details open>
<summary>2021-04-29</summary>

- Array.prototype.split
- Array.prototype.slice

#### 자꾸만~~ 헷갈리는~~ 함수 띄어쓰기
`space-before-function-paren`,  `space-before-blocks`


1) 기명함수 선언문
`function foo() {}`

2) 무명함수 선언문(무명함수를 써야하는 경우 화살표함수를 써라!)
`function () {}`

- 갑자기 찾아본 에어비앤비 코드스타일

*화살표함수를 사용할 수 있는 부분에서는 적극 사용해라*

*arguments 쓰지마라. arguments는 배열도 아니고 객체도 아닌 유사배열*

*인자에 대한 기본값은 함수 안에서 지정하기보단 default parameter를 사용해라*
*단, 기본값에 변형을 주는 건 지양*
*default parameter는 항상 마지막에 위치*
```jsx
// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

var b = 1;
// bad
function count(a = b++) {
  console.log(a);
}
// good
function handleThings(opts = {}) {
  // ...
}
```
*인자를 직접 변형하지마라. 사용할 땐 변수에 담아 그 변수를 사용 - 원본 호출에 대해 원치 않는 결과 초래*

### b = a || 1;
**||는 첫 번째 true를 찾는 연산자**
#### : a가 존재하면 b = a;
#### : a가 없으면 b = 1;

#### 배열 내부 순회 함수 map, forEach 차이점

- `arr.map(callback, thisArg)` : 배열 각각 엘리먼트를 순회하며 함수를 실행하고 그 결과값을 새로운 배열에 담아 반환한다.   
thisArg는 콜백함수를 실행할 this값.

- `arr.forEach(callback, thisArg)` : 배열 각각의 엘리먼트를 순회하며 함수를 실행한다. 특정한 반환값은 없다.(undefined)


*콜백함수가 화살표함수면..?*
-> thisArg는 무시하고 this값을 찾으러 스코프 밖으로 나간다.

`function callback(curentValue, index, array) {}`


</details>

<details open>
<summary>2021-04-30</summary>


#### Object.prototype.assign() vs Object.prototype.merge()
- 공통점: 모두 객체에서만 작동하는 객체 메소드   둘 다 대상 객체가 변경   뒤에 있는 동일한 속성을 가진 다른 객체에 의해 overwrite

- assign - 자식객체까지 깊은 병합. own 속성, enumerable 속성만 가능   
- merge - 1 depth까지만 병합

```jsx
function merge(object, source) {
  if (source.toString() === "[object Object]") {
    for (var key in source) {
      if (typeof source[key] === "object") {
        merge(object[key], source[key]);
      } else {
        object[key] = source[key];
      }
    }
  } else if (Array.isArray(source)) {
    for (let i = 0; i < source.length; i++) {
      if (typeof source[i] === "object") {
        merge(object[i], source[i]);
      } else {
        object[i] = source[i];
      }
    }
  }

  return object;
}

var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};

var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};

merge(object, other);
```
_.merge 구현 완성했다 아 행복해~~

</details>

<details open>
어드미션 코딩 테스트...
<summary>2021-05-01</summary>



</details>

<details open>
<summary>2021-05-02</summary>



</details>
