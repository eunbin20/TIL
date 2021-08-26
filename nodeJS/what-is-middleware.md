# What is Middleware

미들웨어란 무엇일까? 다음과 같은 간단한 어플리케이션이 있다고 해보자.

위 예제에서 변수 할당문을 제외한 모든 함수는 미들웨어이다.

미들웨어 함수는 어플이케이션의 요청-응답의 중간(middle)에 위치한다.
request객체(`req`)와 response객체(`res`)와 다음 미들웨어 함수(`next`)로의 접근을 가지고 있는 함수이다.

1. 어떤 코드든지 실행할 수 있다.

2. request나 response객체를 수정할 수 있다.

3. 요청-응답 사이클을 종료시킬 수 있다.

4. 현재 스택의 다음 미들웨어를 호출할 수 있다.


미들웨어의 종류에는 5가지가 있다.

- 어플리케이션 레벨의 미들웨어
  `app.use`
- 라우터 레벨의 미들웨어
  `router.use`
- 내장된 미들웨어
  `express.static, express.json, express.urlencoded`
- 에러 핸들링 미들웨어
  `app.use(err, req, res, next)`
- 외부에서 특정 기능 수행을 위해 추가된 미들웨어
  `bodyParser, cookieParser`

```jsx
const express = require("express");
const router = expressRouter();

const LoggerMiddleware = (req,res,next) =>{
  console.log(`Logged  ${req.url}  ${req.method} -- ${new Date()}`)
  next();
}

const app = express();

// application level middleware
app.use(LoggerMiddleware);
// third party middleware
app.use(cookieParser());
// built-in middleware
app.use(express.static(path.join(__dirname, "public")));

// router level middleware
router.use(function (req, res, next) {
  next();
})

// application level middleware
app.use("/", verifyToken, (req, res, next) => {
  res.status(200).render("index");
});
// application level middleware
app.post("/", verifyToken, (req, res, next) => {
  res.status(201).render("success");
});
// application level middleware
function verifyToken(req, res, next) {
  // ...
  next();
}

// error-handling middleware
app.use(function (err, req, res, next) => {
  res.status(500).render("error");
});
```



