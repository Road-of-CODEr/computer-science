## 데이터베이스 설계와 ER모델

### 데이터베이스 설계를 하는 목적과 절차
- 데이터베이스 설계는 한 조직체의 운영과 목적을 지원하기 위해 필요한 과정이다. 
- 좋은 데이터베이스 설계란 시간의 흐름에 따른 데이터의 모든 측면을 나타내고, 중복이 최소화되며 무결성을 제공한다. 
- 절차
  
  (1) 요구사항 수집과 분석
    - 실세계에서 관심 있는 부분의 정보 구조 요구를 파악하는 단계


  (2) 개념적 설계
    - 높은 추상화 수준의 데이터 모델을 기반으로 정형적인 언어로 데이터 구조를 명시한다
    - 주로 많이 사용되는 데이터 모델이 ER 모델이다. 
    - [참고하면 좋은 자료](http://contents2.kocw.or.kr/KOCW/document/2016/catholic/hwangbyungyeon/11.pdf)
    - 개념적 스키마(ER스키마)는 ER다이어그램으로 표현한다. 
    - 데이터베이스 설계자가 요구사항 수집과 분석 후에 개념적 설계단계를 생략하고 바로 논리적 설계단계로 가는 경우가 있는데, 이런 경우 흔히 좋은 관계 데이터베이스가 생성되지 않는다

  (3) DBMS 선정
    - 여러 요인을 검토하여 DBMS를 선정한다


  (4) 논리적 설계
    - 개념적 스키마에 알고리즘을 적용하여 논리적 스키마를 생성하는 단계이다
    - 논리적 스키마를 나타내기 위해 관계 데이터 모델을 사용하는 경우 ER모델로 표현된 개념적 스키마를 관계 데이터베이스 스키마로 사상한다. 


  (5) 정규화
    - ER스키마를 변환해서 얻은 관계스키마를 더 정제하는 과정이다
    - 이를 위해 관계 스키마에 중복과 갱신이상이 없는지 검사한다


  (6) 물리적 설계
    - 처리 요구사항들을 만족시키기위해 저장 구조와 인덱스 등을 결정한다. 
    - 물리적 설계에는 트랜잭션들의 예상 수행 빈도, 트랜잭션들의 시간 제약조건 등이 있는데, 초기에는 개략적으로 인덱스를 선정하고, DBMS를 사용하면서 요구사항이 만족되는지 테스트한다. 
    - 성능향상을 위해 튜닝이 필요한 단계이다


  (7) 트랜잭션 설계
    - 트랜잭션은 완성될 데이터베이스에서 동작할 응용 프로그램이다. 
    - 데이터베이스 스키마는 트랜잭션에서 요구하는 모든 정보를 포함해야한다. 




### ER 모델
- ER모델의 사용 이유
  - ER모델은 물리적인 데이터베이스 설계의 효율성에 관심을 두지 않으면서 한 조직의 개념적 스키마를 설명하기 위해 사용된다.
  - ER 모델을 기반으로 만들어진 CASE 도구(ex: ERWIN)들은 데이터베이스 설계 시간과 비용을 감소시키고, 데이터 베이스 설계 방법론을 표준화하고, CASE도구를 사용하여 개발된 응용 시스템의 유지보수를 용이하게 한다. 
  - CASE도구들은 ER설계를 자동적으로 오라클등 사용자가 원하는 데이터 정의어로 변환해준다. 이러한 도구들에서 사용하는 표기법은 ER다이어그램을 그래픽하게 나타내기에 더 적합한다. 
  - ER 모델은 구형의 그래픽 표기법이나, 개념적으로 익히기 쉽다. 현재는 UML을 사용해서 데이터베이스를 설계한다. 

- [ER모델 표기법 예제 및 설명 자료](https://mangkyu.tistory.com/27)


### 논리적 설계(ER스키마를 관계 모델의 릴레이션으로 사상)
- ER데이터모델을 기반으로 한 사용 DBMS가 없고, 대부분은 관계 데이터베이스 모델을 기반으로 하기때문에 ER스키마를 관계 데이터모델로 변환하는 작업이 필요하다
- ER스키마에는 엔티티타입과 관계가 존재하지만 관계 데이터베이스에는 엔티티타입과 관계타입이 없고 릴레이션만 있다. 
- ER스키마를 릴레이션들의 집합으로 사상한 후에도 릴레이션들이 정보의 중복과 갱신 이상을 가질 수 있기때문에 정규화 과정이 필요하다

- ER 릴레이션 사상 알고리즘
  
  (1) 정규 엔티티 타입과 단일 값 애트리뷰트
    - 정규 엔티티 타입을 하나의 릴레이션으로 만든다. 
    - 단순 애트리뷰트들은 모두 포함시키고, 복합 애트리뷰트의 경우 이를 구성하는 단순 애트리뷰트만 릴레이션에 포함시킨다. 

  (2) 약한 엔티티 타입과 단일 값 애트리뷰트
    - 모든 애트리뷰트들을 릴레이션에 포함시킨다. 
    - 소유 엔티티 타입에 해당하는 릴레이션의 기본키를 해당하는 릴레이션의 외래키로 포함한다. 
    - 이때 약한 엔티티타입에 해당하는 릴레이션의 기본키는 약한 엔티티타입의 부분키와 소유 엔티티를 참조하는 외래키의 조합이다.

  (3) 2진 1:1 관계 타입
    - 두 릴레이션 중 하나를 선택하여 하나의 기본키를 다른 릴레이션의 외래키로 포함한다. 
    - 두 릴레이션이 모두 관계에 완전참여하는 경우 하나의 릴레이션으로 합칠 수 있다. 

  (4) 정규 2진 1:N 관계 타입
    - N측의 참여 엔티티 타입에 1측의 참여 엔티티의 기본키를 외래키로 포함시킨다. 
  
  (5) 2진 M:N 관계 타입
    - M:N을 직접 관계 데이터베이스에 나타낼 수 없으므로 별도의 릴레이션으로 표현해야한다. 
    - 해당하는 관계에 대해 릴레이션을 하나 생성하고 참여하는 엔티티타입에 해당하는 릴레이션의 기본키를 모두 외래키로 포함하고, 이들의 조합이 이 릴레이션의 기본키가 된다

  (6) 3진 이상의 관계 타입
    - 관계 타입에 대해 릴레이션을 생성하고, 참여하는 모든 엔티티의 기본키를 외래키로 가져온 다음, 이 릴레이션의 기본키로 사용한다. 
    - 1:N:N의 경우 N:N를 참조하는 외래키만 기본키를 구성한다. 
  
  (7) 다치 애트리뷰트
    - 다치 애트리뷰트에 대해서 릴레이션을 생성하고, 해당 애트리뷰트를 릴레이션에 포함시킨다. 
    - 다치 애트리뷰트를 애트리뷰트로 갖는 엔티티 타입이나, 관계 타입의 기본키를 이 릴레이션의 외래키로 포함시킨다. 
    - 이 릴레이션의 기본키는 다치 애트리뷰트와 외래키의 조합이다.

### 참고자료
[데이터베이스 배움터(oracle)](http://www.yes24.com/Product/Goods/4154340)



  