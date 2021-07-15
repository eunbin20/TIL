# Controlled component vs Uncontrolled component

- 사용자의 입력을 제어하는 방식에는 두 가지가 있다.

## 제어 컴포넌트

리액트 컴포넌트 내부 로직에 의해 화면에 표시되는 값이 제어됨
 → 화면에 표기하는 과정에서 변환하거나 다른 처리를 적용하기 쉽다.

```jsx
function controlledConponent() {
  const [username, setUsername] = useState("");

  function handleSubmit(event) {
    event.prevent.default();
    alert(`이름: ${username}`);
  }
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="username">이름</label>
        <input
          value={username}
          onChange={ev => setUsername(ev.current.value)}
					id="username"
				/>
			</div>
		</form>
	);
}
```

- input의 값은 항상 신뢰 가능한 단일 출처(single source of truth)로 결정된다.

- 비제어에 비해 코드를 좀 더 작성해야 하지만, 다른 UI엘리먼트에 input 값을 전달하거나 다른 이벤트 핸들러에서 값을 재설정할 수 있다.
x
- 여러 input 값을 조정해야하는 경우

```jsx
function Reservation() {
  const [isGoing, setIsGoing] = useState(true);
  const [numberOfGuests, setNumberOfGuests] = useState(2);

  handleInputChange(event) {
    const target = event.target;

    if (target.type === 'checkout') {
      setIsGoing(target.checked);
    } else {
      setNumberOfGuests(target.valu);
    }

	render(
    <form>
      <label>
        IsGoing:
        <input
          name="isGoing"
          type="checkbox"
          checked={isGoing}
          onChange={ev => setIsGoing(ev.current.value)}
        />
      </label>
      <br />
      <label>
        Number of guests:
        <input
        name="numberOfGuests"
        type="number"
        value={numberOfGuests}
        onChange={ev => setNumberOfGuests(ev.current.value)}
        />
      </label>
    </form>
	);
}
```

## 비제어 컴포넌트

사용자의 입력값이 DOM에 의해 화면에 표시되는 방식
(DOM자체에서 폼데이터가 다루어짐)

* 사용자의 입력값을 제어하는 로직이 없으므로 접근하려면 ref키워드를 이용해야한다.

```jsx
function UncotrooledComponent() {
	const inputEl = useRef(null);

  function handleSubmit(event) {
    event.prevent.default();
    alert(`이름: ${inputEl.current.value}`);
	}

	return (
    <form onSubmit={handleSubmit}>
      <div>
      <label htmlFor="username">이름</label>
        <input
          ref={inputEl}
          id="username"
          type="text"
        />
      </div>
    </form>
	);
}
```

- DOM에 신뢰가능한 출처를 제공한다.

- React - non React 코드 통합에 용이하다.

- 기본값 설정 → defaultValue

- `<input type="file">`은 프로그래밍적으로(리액트 컴포넌트 내에서) 값을 설정할 수 없고 사용자만 설정할 수 있으므로 항상 비제어컴포넌트로 다루어진다.
