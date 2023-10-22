## 한눈에 들어오는 Test Fixture
+ BeforeEach에 데이터 setup하면 다른 테스트간의 결합도가 생긴다.
+ data.sql에 테스트를 위한 데이터를 setUp하면?
  - 관리포인트가 너무 많이 들어난다. 추천하지 않음
+ builder를 위한 함수 예를들면 createProduct() 같은 함수는 꼭 받을 파라미터만 받자
  - 테스트 클래스마다 필요한 파라미터를 만드는 builder를 이용함
  - 코틀린이면? 롬복 필요없고 생성자내에 파라미터를 지정해서 넣으면 됨, 지정하지 않으면 디폴드 값도 넣을 수 있음
 
## Test Fixture 클렌징
+ deleteAllInBatch를 주로 사용 (지울때도 순서를 고려해야함 외래키 제약조건)
  - deleteAll과의 차이는? deleteAll은 건 단위로 지우고 select 하고 건 단위로 지우고 하는 동작을 반복함
    - 연관 관계를 따지면서 select
  - deleteAllInBatch는 그냥 delete하고 끝 (성능에 좀더 좋음)
+ @Transacational은 지양

## ParameterizedTest

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/a7de8ccb-189d-48e2-baf0-782b5e4b2c3b)

## DynamicTest

+ 일련의 시나리오에 맞게 테스트 수행
  - 형태를 유지하면서!, List.of로 상황을 유지한다.
  
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/08cfe42d-02ad-480b-8d8a-3caa71d1fa63)

## 테스트 수행도 비용이다. 환경 통합하기

+ @Disabled : 테스트 수행하지 않도록 하는 어노테이션 (불필요하게 테스트를 안지워도 된다)

+ 전체 테스트하는데 서버가 6번 떴다. (profile이 다르거나 환경이 다르면 새로 뜬다)

### 서비스 쪽

+ 상위 클래스에 아래와 같은 클래스 상속 받고 
  - extends IntegrationTestSupport
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/6e1a31dd-3e79-4d46-9407-13e11f746e5b)

> 통합을 했는데 OrderStaticServiceTest는 왜 또 스프링부트가 새로 떳지?
> 
> OrderStaticServiceTest 에는 @MockBean이 있어서 새로 환경이 있어야함
>
> IntegrationTestSupport에다가 protected 변수로 옮김

### 레포지토리 쪽

+ Repository 테스트할때도 @DataJpaTest 대신 @SpringBootTest하면 그냥 환경 재활용이 되니까 그냥 @SpringBootTest쓰는걸 선호함

### 컨트롤러 쪽

+ 여기는 통합하기 좀 어렵다.
+ 아래와 같이 {}로 묶어서 통합할 수는 있긴함
  - 이런식으로 해서 레이어 별로 나누면 괜찮다.
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/6dd1e4a1-c6f8-4635-8d45-f8fe729f114a)

> 6번 뜨던 환경이 2번으로 줄었다.

## private 메소드는 어떻게 테스트 하나요?
+ 할 필요가 없다.

## 테스트에서만 필요한 메서드가 생겼는데 프로덕션 코드에서는 필요 없다면?
+ 만들어도 된다. 하지만 보수적으로 접근하기
