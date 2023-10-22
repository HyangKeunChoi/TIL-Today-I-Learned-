![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/bdc70be7-374b-4dfb-92ed-caa8d1af5cc9)# 코루틴의 구성 요소와 원리

## Structured Concurrency

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/15f0adb7-e028-4f74-a72d-edfa09442a31)

+ 자식 코루틴을 기다려야 하기 때문!
+ 특정 자식 코루틴에서 예외가 발생하면 예외가 부모로 전파되고 다른 자식 코루틴에게 취소 요청을 보낸다!
+ Structured Concurrency : 부모, 자식 관계의 코루틴이 한 몸 처럼 움직이는 것

## Structured Concurrency 정리
+ 자식 코루틴에서 예외가 발생할 경우, Structured Concurrency에 의해 부모 코루틴이 취소되고, 부모 코루틴의 다른 자식 코루틴들도 취소된다.
+ 다만 CancellationException은 정상적인 취소로 간주하기 때문에 부모 코루틴에게 전파되지 않고, 부모 코루틴의 다른 자식 코루틴을 취소시키지도 않는다.

## CoroutineScope과 CoroutineContext
+ 사실 launch / async는 CoroutineScope의 확장 함수이다.
  - runBlocking이 코루틴과 루틴의 세계를 이어주며 CoroutineScope을 제공해 주었다.
 
 ## CoroutineScope의 주요역할
 + CoroutineContext 라는 데이터를 보관
 + CoroutineContext : 코루틴과 관련된 여러가지 데이터를 갖고 있다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/195a8b9a-3263-48e4-bf36-954cb5c59ead)

+ Dispatcher : 코루틴이 어떤 스레드에 배정될지를 관리하는 역할

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/8de8c3f0-f885-4e44-a48a-860a3e150d8b)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/a4c6508d-0ecf-47d8-a46a-bf0d5df49c89)

## CoroutineContext
+ Map + Set을 합쳐놓은 형태

## CoroutineDispatcher (주요 dispatcher 종류)
+ Dispatchers.Default : 가장 기본적인 디스패처, CPU 자원을 많이 쓸 떄 권장 별다른 설정이 없으면 이 디스패처가 사용된다.
+ Dispatchers.IO : I/O 작업에 최적화된 디스패처
+ Dispatchers.Main : UI 컴포넌트를 조작하기 위한 디스패처, 특정 의존성을 갖고 있어야 정상적으로 활용할 수 있다.

## ExecutorService를 디스패처로 바꿀 수 있다.
+ asCoroutineDispatcher() 확장함수 활용

## Suspending function
+ suspend가 붙은 함수, 다른 suspend가 붙은 함수를 호출할 수 있다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/3c3cb943-c6f6-41ef-b511-b1174b6395ee)

+ suspend function 함수는 코루틴이 중지 되었다가 재개 될 수 잇는 지점
+ 비동기 프로그래밍 할때 callback 지옥에서 벗어 날 수 있는 동기식 프로그래밍 가능
+ 여러 비동기 라이브러리를 사용할 수 있도록 도와준다.

## withContext
+ coroutineScope와 유사하다.
+ context에 변화를 주는 기능이 추가적으로 있다.

## withTimeout / withTimeoutOrNull
+ corutineScope와 기본적으로 유사하다.
+ 주어진 시간 안에 새로 생긴 코루틴이 완료되어야 한다.
  - 주어진 시간 안에 코루틴이 완료되지 못하면 예외를 던지거나 null을 반환하게 된다.

## 코루틴과 Continuation
+ 코루틴은 어떤 원리로 중단과 재개를 반복할까?
+ 핵심은 Continuation을 전달하며 callback으로 활용한다

## 마무리 - 코루틴의 특징
+ callback hell을 해결
+ kotlin 언어 키워드가 아닌 라이브러리
+ 비동기 non-blocking 혹은 동시성이 필요한 곳에서 사용
  - client : Async UI
  - server : 여러 API를 동시에 호출
  - 동시성 테스트
  - webflux
 
  
