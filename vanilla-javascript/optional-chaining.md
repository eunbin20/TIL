# Optional Chaining

중첩된 객체에서 프로퍼티가 없는 경우 undefined를 반환하여 에러 없이 값을 참조할 수 있게 한다.

```jsx
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};

// without optional chaining
const dogName = adventurer.dog.name; // error
```

위 예제에서 `adventurer.dog`의 값은 undefined이다.

즉 `undefined.name`으로 접근하려했기 때문에 에러가 발생하는 것이다.

그러나 때로는 해당 프로퍼티가 있으면 값을 참조하고, 없으면 에러가 발생하는 것이 아닌 undefined를 반환해야하는 경우가 존재한다.

이때 사용할 수 있는 것이 optional chaining이다.

```jsx
const dogName = adventurer.dog?.name; // undefined
```

adventurer객체에 dog가 있으면 그 내부의 name프로퍼티를 참조할 것이고 dog이 없으면 undefined를 반환할 것이다.


나는 이번 Voting Platform 과제에서 세션을 이용한 로그인 기능을 구현하다가 이 `optional chaining`의 필요성을 느꼈다.

```jsx
router.get('/', function(req, res, next) {
  res.render('index', { user: req.user?.nickname });
});
```

index 라우터의 내부 코드이다. req객체 내부에 user프로퍼티가 있으면, 그 내부의 nickname 값을 참조한다.

optional chaining 방식으로 작성하지 않으면 undefined의 nickname프로퍼티에 접근할 수 없다는 에러가 발생할 것이다.
