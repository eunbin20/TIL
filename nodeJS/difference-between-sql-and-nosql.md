# Difference between SQL and NoSQL

## SQL(Structured Query Language; 구조화된 쿼리언어)

특정 유형의 DB(RDBS, 관계형 데이터베이스)와 상호작용하는 데 사용하는 언어이다.

- 데이터는 **정해진(엄격한) 스키마**를 따라 데이터베이스 테이블에 저장한다.

  데이터는 테이블 내의 레코드로 저장되며, 각 테이블에는 명확하게 정의된 구조가 있다.

  *스키마를 준수하지 않는 레코드는 추가할 수 없다.

- 데이터는 **관계**를 통해서 연결된 여러 개의 테이블에 분산된다.

  데이터들을 여러 개의 테이블에 나누어서 데이터의 중복을 피할 수 있다.

  각각의 테이블은 다른 테이블에 저장되지 않은 데이터만을 가지고 있다.(->중복된 데이터가 없다.)

- 관계를 맺고있는 데이터가 자주 변경되는 애플리케이션일 경우
- 변경되지 않고 명확한 스키마가 필요한 데이터인 경우

- 장점

  스키마가 명확하게 정의되어있어 데이터 무결성이 보장된다.

  각 테이블의 데이터가 중복되지 않는다.

- 단점

  스키마의 수정이 불가능하다.

  데이터가 여러 테이블에 분산되어있기 때문에 join을 이용해야 함

  수평적 확장이 어렵다.

  ## NoSQL(Non-SQL, Not only SQL, non-relational database)

  RDBS에서의 레코드를 document라고 부른다.

  SQL에서는 정해진 스키마를 따르지 않으면 데이터를 추사할 수 없지만 NoSQL에서는 다른 구조의 데이터를 같은 컬렉션에 추가할 수 있다.

  문서는 JSON과 비슷한 형태를 가지고 있다 (js를 이용한 개발시 많이 이용된다.)

  일반적으로 관련 데이터를 도일한 컬렉션에 넣는다.

  -> Orders컬렉션에 일반적인 정보를 포함한 모든 데이터가 저장된다.(Users나 Products도 포함)

  따라서 여러 테이블/콜렉션에 조인할 필요 없이 이미 필요한 모든 정보를 갖춘 문서를 작성하게 된다.

- 데이터의 구조가 확정되지 않고 자주 변경, 또는 확장될 수 있는 경우
- 읽기 처리를 자주 하지만 데이터가 자주 변경되지 않는 경우
- 데이터베이스를 수평적으로 확장해야 하는 경우

- 장점

    스키마가 없기 때문에 훨씬 유연하다. 언제든지 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.

    데이터는 애플리케이션이 필요로 하는 형식으로 지정되어 데이터를 읽어오는 속도가 빠르다.

    수직 및 수평 확장이 가능하므로 방대한 양의 데이터를 관리할 수 있다.

- 단점

  데이터 구조의 유연성으로 인해 데이터의 구조가 불안정할 수 있다. 일관성이 약하다.

  데이터의 중복이 발생하므로 업데이트할 때 여러 컬렉셔의 문서들을 업데이트 해야 한다.


</br>

### - 수평적(horizontal) 확장과 수직적(verticle) 확장(scale)
  - 수평적 확장 = Add more server(and merge data into DB)

    **scaling out**

    더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨

    -> 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동

    데이터가 저장되는 방식때문에 SQL 데이터베이스는 일반적으로 수직적 확장만을 지원한다.

    샤딩(Shading)의 개념을 적용하는 데 제한이 있으며 대체로 구현하기가 어렵다.


  - 수직적 확장 = Improve server capacity / hardware

    **scaling up**

    단순히 데이터베이스 서버의 기능을 향상시키는 것(CPU업그레이드)

    NoSQL데이터베이스에서만 가능하다.

    샤딩을 기본적으로 지원하고, 여서 서버에서 DB를 쉽게 분리할 수 있다.

> 샤딩이란?<br/>
  데이터베이스나 웹 검색엔진의 데이터를 물리적으로 수평분할하는 패턴 <br/>
  DB트래픽을 분산할 목적으로 사용되며 다수의 데이터베이스에 데이터를 분산하여 저장한다.<br/>  
  데이터를 수평적으로 분할하기 위한 용이한 기준을 잡고 데이터를 분산하거나 row의 행수를 기준으로 분산저장한다.<br/>
  레인지 샤딩/모듈러 샤딩</br>
  \- 장점: 1.쿼리 시간이 단축된다. 2.shared DB가 아니면 모든 row를 검사해야 한다.
  3.db의 신뢰도를 높인다. <br/>
  \- 단점: 1. 샤딩되어있는 데이터베이스를 적절하게 구현하기가 복잡하다. 2. 결국은 불균형해진다. 3.한 번 분배를 하면 다시 돌아가기가 힘들다.






