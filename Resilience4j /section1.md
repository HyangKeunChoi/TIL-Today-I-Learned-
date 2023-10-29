# Resilience4j 시작하기

+ 깃헙에서 resilience4j-spring-boot2 들어가기
  - 너무 복잡하게 되어있음, 모든 기능을 다 쓸 필요는 없다

+ AOP 의존성 추가 : 왠만하면 거의 다 AOP를 이용 해서 사용할 수 있음
+ actuator : 서킷브레이크를 더 잘 쓰기 위해 의존성 추가

## Retry를 통해 Resilience4j 맛보기

## Resilience4j의 instance
+ 자바의 instance 와 같다고 보면된다.
+ 크게 신경쓸 필요는 없다.

<img width="965" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/86f2be59-a044-4651-89a4-85cc8933891f">

+ 특정 예외가 터질때만 retry 시도(yaml파일)

### RegistryEventConsumer
+ 이 빈을 등록해서 이벤트 핸들러를 등록함
+ 이벤트 발생시 동작 정의

## Retry하는 코드 직접 만들어보기

