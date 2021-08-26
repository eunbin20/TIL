# [npm] cookie-session vs express-session

두가지 라이브러리 모두 세션을 생성해주는 라이브러리이다. 


## cookie-session

세션을 생성해주는 미들웨어로 req의 session속성을 통해 접근할 수 있다.
request로부터 session을 받지 않은 경우 새로운 session을 생성하고 또는 request로부터 세션을 불러온다.

이 미들웨어는 req.session의 내용이 변하면 자동으로 response의 header에 set-cookie속성을 추가한다. 

*Note*

세션에 내용이 없는 한 헤더에는 set-cookie가 추가되지 않는다. 그러므로 세션에 저장할 수 있는 식별 가능한 정보를 가지는대로 req.session에 무언가를 추가해야 한다.

**세션 데이터를 쿠키에 담아 client에 저장한다.**

세션 데이터가 비교적 작고 원시값으로 쉽게 인코딩할 수 있는 값일 경우에만 사용해아.

비록 브라우저는 쿠키 하나 당 4096 bytes 이상의 공간을 제공하지만, 한 도메인 당 4093 bytes을 초과하지 않도록 해라. 또한, 쿠키의 데이터는 클라이언트에게 보여지기 때문에, 안전성과 명확성을 유지하기 위해서는 `express-session`이 좀 더 나은 선택이다.


```jsx
const cookieSession = require("cookie-session");
const app = express();

app.use(cookieSession({
  name: "session",
  keys: "secret",

  // cookie options
  maxAge: 24 * 60 * 60 * 1000,
}));

app.get("/", function (req, res, next) {
  req.session.views = (req.session.views || 0) + 1;

  res.end(req.session.views + " view");
});
```

## express-session

주어진 옵션에 따라 세션 미들웨어를 생성한다.

*Note*

세션 데이터는 쿠키 자체에 저장되지 않고, 세션 아이디만 저장된다. **세션 데이터는 서버 측에 저장된다.**

기본적으로 in-memory 저장소를 사용한다.

```jsx
const app = express();
app.set("trust proxy", 1);
app.use(session({
  secret: "secret",
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))
```
