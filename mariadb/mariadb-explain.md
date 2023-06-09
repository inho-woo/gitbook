# MariaDB Explain

쿼리를 작성하여 실행을 시작하니 결과까지 1분이상이 소요가 되었다.\
이러다보니 웹 차트 로딩도 오래걸려 사용하기가 너무 불편해 방법을 찾아보았다.\
찾다보니 **explain** 기능을 알게 되었고, 나중에도 사용할수 있는 기능이기에 정리를 했다.

### explain 이란?

통게 데이터 처리등 복잡한 쿼리의 최적화를 위해\
**explain** 이라는 기능을 통해 쿼리 계획을 분석해 쿼리를 최적화 시켜주는 기능

쿼리의 실행 시간에 가장 큰 영향을 주는 요소들은 **RDBMS** 가 설치된 머신의 스펙과 쿼리의 대상이 되는 레코드의 수, 그리고 인덱스 접근/ 사용 방식과 중첩 쿼리의 실행 순서 등 쿼리 자체의 실행 과정이다. 이 중 머신의 스펙과 대상 레코드의 수는 최적화의 대상으로 보기는 어렵다. 따라서 최적화의 대상은 쿼리 실행 과정인데, 이는 단순히 실행 시간만을 측정해서는 알 수 없기 때문이다.

**explain** 을 이용해 쿼리 게획을 보는 방법은 간단하다.

![explain](https://user-images.githubusercontent.com/58337935/139808616-c1bd2233-dafc-4688-92ed-6a34118bab90.jpg)

**EXPLAIN** 을 실행하면 위와 같은 결과가 출력된다. JOIN이나 서브 쿼리가 포함되어 여러 단계의 처리가 필요한 경우, 각 단계별로 실행 계획을 보여준다.

쿼리 계획에는 다음 항목들이 표시된다.

* id:대상 쿼리문에 JOIN이 포함되어 있을 때, 어떠한 순서로 테이블이 JOIN되는지를 나타내는 값이다.
* select\_type:각 단계를 실행할 때 어떤 종류의 SELECT가 실행되었는지를 나타낸다. 최적화 시에는 크게 중요하지는 않으나, 값이 DEPENDENT SUBQUERY, 혹은 DEPENDENT UNION 인 경우 의존성 등의 문제로 쿼리가 특정 순서로만 실행되어야 함을 뜻하므로 비효율적인 쿼리일 가능성이 있다.
* table:해당 단계에서 접근하는 테이블의 이름이다. 실제 테이블, 혹은 임시 테이블일 수 있다.
* type:테이블 내에서 접근이 필요한 레코드를 어떻게 찾았는지에 대한 정보이다. 인덱스 접근 여부 및 방식 등에 대한 내용도 포함하므로 쿼리 최적화 시 반드시 확인해야 할 값이다. 몇 가지 중요한 값에 대해서만 부연 설명하겠다.
* system:테이블 내에 레코드가 1개 이하인 경우이다. 이 경우에는 레코드를 더 추가한 후 다시 쿼리 계획을 확인하는 것이 좋다.
* const,eq\_ref:해당 단계가 PK 나 유니크 인덱스 검색을 이용해 레코드에 접근함을 뜻한다. 일반적으로 가장 빠른 검색 방법이다.
* ref:인덱스를 이용하여 동등 비교 연산을 통해 레코드에 접근함을 뜻한다. 위의 두 개만은 못하지만, 역시 매우 빠른 검색 방법이다.
* fulltext:전문 인덱스(Fulltext Index) 를 이용하여 레코드에 접근함을 뜻한다. 전문 인덱스는 일반적인 비교 연산으로 접근이 어려운 경우에 주로 사용되므로 최적화하기 어려운 경우가 많다.
* range:인덱스를 이용하여 값 비교 연산 ( , BETWEEN 등 )을 이용하여 레코드에 접근함을 뜻한다.
* index:index 전체를 스캔해야만 필요한 레코드에 접근할 수 있음을 뜻한다. 풀 테이블 스캔보다는 빠르지만, 인덱스가 매우 큰 경우 등에는 비효율적이다.
* ALL:인덱스를 이용하여 필요한 레코드를 검색할 수 없어, 전체 테이블을 스캔해야만 함을 뜻한다. 당연히 테이블 내 레코드 수에 따라 실행 시간이 매우 길어지므로 적절한 인덱스 추가나 HINT 문 사용 등을 통해 최적화하는 것이 좋다.
* possible\_keys:레코드에 접근하기 위해 사용할 수 있는 키, 혹은 인덱스 목록을 보여준다. 실제로 사용된다는 의미가 아니므로 실제로 어떠한 키가 사용되었는지는 key 항목을 확인해야 한다.
* key, key\_len : 레코드에 접근하기 위해 어떠한 index를 참조하는지, 인덱스 중 몇 바이트를 참조했는지에 대한 정보이다. key\_len 은 둘 이상의 컬럼으로 구성된 인덱스를 참조했을 경우에만 의미가 있다.
* ref:인덱스 검색 시 비교 연산 등에 사용되는 기준값을 보여준다. 최적화 시에는 큰 의미는 없다.
* rows:필요한 레코드들을 추려내는 과정에서 몇 개의 레코드에 접근해야 하는지를 예측하여 보여준다.
* extra:이상의 항목 외의 특이 사항들이 있다면 해당 내용을 표시해준다. 예를 들어, 접근해야 하는 컬럼이 모두 인덱스에 포함되어 있어 인덱스 검사만으로 필요한 값을 반환할 수 있다면 Using index 가 표시된다. 때에 따라 성능에 영향을 줄 수 있는 값들이 있으므로, 최적화 시에 이 컬럼이 비어 있지 않다면 확인할 것을 권한다.

실제로 **explain** 을 실행한결과 , 테이블 INNER JOIN을 한 테이블에서 풀스캔을 하고 있어 쿼리가 너무 느렸다.

50만건이상 풀스캔을 하다보니 느릴수밖에 없는 결과였기 때문에 테이블 INDEX를 걸어 해결하려고 했지만,\
고객사 DB이다보니 함부로 변경이 안돼 요청을 하게 되었다.

이렇게 오늘도 하나를 배우게 되었다.
