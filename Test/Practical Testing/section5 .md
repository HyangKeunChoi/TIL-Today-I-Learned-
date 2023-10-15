## library vs framework

+ library는 내 코드가 주체이고 필요한것만 외부에서 끌어다 씀
+ framework는 이미 틀이 있어서 내 코드가 수동적으로 돌아감
+ 뷰는 프레임워크, 리액트는 라이브러리
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/7134ea50-19c7-4fc6-a3f7-5704d3a77fc1)

### Persistence Layer 테스트 (2) - DATA ACCESS 테스트
+ data access의 역할 + 비즈니스 가공 로직이 포함되어서는 안된다.
  - data에 대한 crud에만 집중한 레이어

+ DataJpaTest : SpringBootTest보다 가벼움
  - 하지만 springBootTest를 좀더 선호함 ( 그 이유는 다다음시간에 )
 
+ assertThat.extracting() : 원하는 필드만 추출
  - containsExactlyInAnyOrder : 순서에 상관없이 필요한 데이터가 있는지
 
### Business Layer 테스트 (1)
+ 비즈니스 로직을 구현하는 역할
+ persistence layer와의 상호작용을 통해 비즈니스 로직을 전개시킨다.
+ ***트랜잭션***을 보장해야 한다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/ad568728-6650-4dc4-81f5-ae8c43f6357b)

+ business layer + persistence layer합쳐서 테스트하는 느낌으로 작성할 예정

+ AfterEach를 통해 다른 테스트에 영향 주지 않기 - 데이터 클랜징
  - orderServiceTest에서 (서비스 테스트)
  - productRepository.deleteAllInBatch();
  - orderProductRepository.deleteAllInBatch();
  - orderRepository.deleteAllInBatch();
 
+ 리포지토리 테스트는 클랜징을 안했는데도 테스트가 통과 했다.?
  - 알아서 rollback이 됨
  - @DataJpaTest에 @Transactional이 걸려있다.
  - @SpringBootTest에는 @Transactional이 안걸려있다.
 
+ 그러면 서비스 레이어에 @Transactional 달면 되지 않나? 굳이 AfterEach하지 않고
  - 다음 강의에서 설명
 
+ Post요청의 경우 브라우저에서 테스트하기 어려움
  - order.http파일 생성
 
## Business  Layer 테스트3

+ @Transactional vs deleteAllInBatch() 데이터 클랜징 차이
  - @Transacional을 테스트 클래스에 달면 서비스 레이어에 @Transcational이 설정된 것 처럼 보이게 됨
  - 쓰지 않자가 아니고 잘 써야한다!

- readOnly= true // CURD에서 CUD 동작 X / only Read
  - jpa에서 CUD 스냅샷 저장, 변경감지 X
  - CQRS - Command / Read 분리

## Presentation Layer 테스트1
+ presentation  layer를 테스트할때는 business, persistence layer는 mocking 처리한다.

## Presentation Later 테스트2
+ @WebMvcTest : controller의 mock객체를 쓰기위한 테스트
  - @WebMvcTest(controllers = ProductController.class)
+ @MockBean : 컨테이너에 mock객체를 넣어줌
  - @MockBean ProductService productservice;
+ @Mock
  
