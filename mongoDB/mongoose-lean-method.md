# Why use mongoose lean method

"Faster Mongoose Queries With Lean"

lean 메소드는 쿼리 작업을 더욱 빠르고 메모리를 덜 소모하도록 해준다.

하지만 이 메소드가 반환하는 document는 몽구스의 document가 아닌 plain old Javascript objects(POJOs)이다.

기본적으로 몽구스에서 쿼리를 실행하면 Mongoose document class를 반환한다.

이 document는 더 많은 내부적인 state를 가지고 있기 때문에 바닐라 자바스크립트의 객체보다 더 무겁다.

```jsx
const schema = new mongoose.Schema({ name: String });
const MyModel = mongoose.model('Test', schema);

await MyModel.create({ name: 'test' });

// 객체의 크기를 측정하는 모듈
const sizeof = require('object-sizeof');

const normalDoc = await MyModel.findOne();
const leanDoc = await MyModel.findOne().lean();

sizeof(normalDoc); // >= 1000
sizeof(leanDoc); // 86, 10배 이상 작다!
```

쿼리작업을 수행하고나서, 몽구스는 비밀리에 쿼리 실행 결과를 POJOs로 바꾸는 작업을 수행한다.

lean 옵션은 이 작업을 건너뛰게 해준다.
