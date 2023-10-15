## Test Double : 아래 목록들을이 test double의 종류들
+ Dummy : 아무것도 하지 않는 깡통 객체
+ Fake : 단순한 형태로 동일한 기능은 수행하나, 프로덕션에서 쓰기에는 부족한 객체
+ Stub : 테스트에서 요청한 것에 대해 미리 준비한 결과를 제공하는 객체
+ Spy : Stub이면서 호출된 내용을 기록하여 보여줄 수 있는 객체, 일부는 실제 객체처럼 동작시키고 일부는 stubbing할 수 있다.
+ Mock : 행위에 대한 기대를 명세하고, 그에 따라 동작하도록 만들어진 객체

+ stub vs mock
  - stub : 상태 검증
  - mock : 행위 검증
 
+ service레이어 테스트시 spring을 쓰지않고 순수 mockito만 써서 테스트해보기
  - @ExtendWith(MockitoExtension.class)
+ @Spy : 실제 객체를 사용해야할 때(엄청 많이 사용하진 않는다)
  - 이 경우 when - thenReturn를 사용할 수 없다.
  - doReturn - when을 사용해야한다.

 ## BDD
 + BDDMockito.given().willReturn()
 + mockito와 같은데 이름만 바뀌었다 mockito와 동작이 같다

## Classicist vs mockist
+ mockist : 모든게 mock
+ classicist : 필요한 경우만 mock하자
