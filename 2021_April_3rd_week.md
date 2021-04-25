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

<details open>
<summary>2021-04-20</summary>
<div markdown="1">

### 비동기

비동기로 실행되는 프로그래밍은 마치 줄을 서서 주문번호를 받고, 음식이 나오는 순서대로 음식을 받아가는 식당의 알고리즘에 비유할 수 있다.   

(작업이 완료되는 순서대로 일을 처리)   

비동기를 구현하는 방법   

1) callback(콜백 지옥)   

함수의 반환값을 받아서 다음 비동기 처리를 해야하는 경우.   

2) promise(fetch, then, catch)   

3) async/await   


- 이벤트루프   
```
console.log("start");

setTimeout(function foo () {
  console.log("foo!");
}, 0);

console.log("end");
```   

위 실행문의 결과는 start -> end -> foo!   


setTimeout 밑으로 아무리 많고 무겁고 오래걸리는 코드가 있다 하더라도 그 모든 코드가 실행된 이후에 setTimeout의 콜백함수가 실행된다. 그 이유는 이벤트 루프 작동방식 때문이다.   


setTimeout 함수는 web API가 담당하는 함수로 webAPI에서는 0초가 지난 이후 콜백함수를 Callback Queue에 줄세운다.   


이 Callback Queue에 담긴 작업들은 콜스택이 비워진 이후, 즉 모든 코드가 실행된 이후에 순차적으로 실행된다.   


즉 setTimeout은 사실 정확히 00초 뒤에 콜백함수를 실행하는 것이 보장되지 않는다. <i>실행에 걸리는 최소한의 시간<i/>만을 정할 수 있다.   

</div>
</details>

<details open>
<summary>2021-04-21</summary>
<div markdown="1">
### 1) Array.prototype.slice(a, b)메소드   


배열의 인덱스 a부터 인덱스 b전까지(b 포함x) 원본 배열을 복사하여 새로운 배열을 반환   


array.slice(1) : 인덱스 1부터 배열의 마지막까지 반환   
array.slice(-1) : 배열의 마지막부터 1만큼 반환(start값이 배열의 뒤에서 1 앞으로)   

### 2) 데이터타입 판별 유의할 것   
 typeof (객체) : object   
 typeof (배열) : object   
 typeof null : object   
 typeof Nan : number   
 * 객체만 판별할 때 : (객체).toString === "[object Object]"   
 * 배열 판별할 때 : Array.inArray(배열)   

### 3) 객체 요소 순회   
 for (const key in object) -> key 변수는 재할당되지 않는다.   

### 4) rest parameter   
 (arg1, arg2, ...rest)   
 rest = ar1과 arg2를 제외한 인자값의 배열   

### 5) apply   
 인자를 배열 형식으로 받는 경우 함수를 호출하는 방법   
 func.apply(this, rest)

### 6) 동일한 모양의 배열 또는 객체 비교할 때 주의   
배열 또는 객체면 같은 배열 또는 객체여도 동일하지 않다.   
-> JSON.stringfy를 이용   
toString은 그 데이터타입 자체를 string으로 변환   
arr = [1, 2];   
arr.toString() // 1, 2   
JSON.stringfy(arr) // "[1, 2]"   

### 7) 문자열 형식으로 되어있는 메소드를 어떻게 실행할것인가   
메소드는 객체의 속성 중 함수로 되어있는 속성   
객체의 메소드 실행 방법   
1. "dog".toUpperCase();   
2. "dog"\["toUpperCase"\]()   



</div>
</details>

<details open>
<summary>2021-04-22</summary>
<div markdown="1">
### push() pop() shift() unshft() 모두 원본배열을  수정한다.

```jsx
var arr = [1, 2, 3]; // [1, 2, 3] → [1, 2]

function foo(array) {
  array.pop();
}

foo(arr); // 실행시 arr이 바뀐다.
foo(arr); // 이때 arr은 [1, 2]
```
*원본배열을 변경하고싶지 않다면 slice를 사용해라~*
</div>
</details>

<details open>
<summary>2021-04-23</summary>
<div markdown="1">
### Diffrernce between return and break statment


**return** : 함수 실행을 종료하고 실행문에 return값을 할당한다.   

return문 이후의 코드는 실행되지 않는다.   


**break** : 현재 반복문(for, while, switch 등)를 종료하고 다음 문으로 넘어간다.   

함수 밖으로는 나가지 않는다.   


> ☆ break로는 if문을 중단시킬 수 없다.   


break와 continue   

```jsx
for (i = 0; i < 10; i++) {
  if (i === 3) { continue; }
    text += "The number is " + i + "<br>";
  }
}
// 1 2 4 5 6 7 8 9
```   

```jsx
for (i = 0; i < 10; i++) {
  if (i === 3) { break; }
    console.log(i);
  }
}
// 1 2 3
```   

### 반복문   


**for of loop**   

문자열, 배열, 유사배열의 반복문을 만든다.   

```jsx
for (const element of arr) {}
```

**for in loop**   

객체의 열거가능한 속성의 키값으로 으로 반복문을 만든다.    

```jsx
for (const key in obj) {}
```
</div>
</details>


<details open>
<summary>2021-04-24</summary>
<div markdown="1">
### 코드리뷰

> 꼭 변수 선언문이 함수의 제일 상단에 위치해야하는 것은 아니다.   
함수의 코드 흐름상 early return문을 구현할 수 있다면 if문을 상단에 위치시킬수도 있다.    

변수명은 구체적으로

</div>
</details>
