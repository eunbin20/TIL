# What's difference between connect() vs createConnection()

`mongoose.connect()`를 호출하면 몽구스는 기본(default) connection을 생성한다. 이후에 `mongoose.connection`명령을 이용하면 이 기본 connection에 접근할 수 있다.

몇 가지의 이유로 여러 개의 connection이 필요할 수 있다. 한 가지의 이유는 여러 개의 데이터베이스나 여러 개의 mongoDB cluster가 필요할 때이다.

`mongoose.createConnection()`함수는 `mongoose.connection()과 동일한 인자를 받아 새로운 connection을 만든다.

https://mongoosejs.com/docs/connections.html#multiple_connections

https://stackoverflow.com/questions/40818016/connect-vs-createconnection

