## 코루틴이란?
+ 협력하는 루틴

## 루틴과 코루틴의 차이
+ 루틴에 진입하는 곳이 한 군데이며, 종료되면 해당 루틴의 정보가 초기화된다.
+ 의존성 추가

```kotlin
fun main(): Unit = runBlocking {
  println("START")
  launch {
    newRoutine()
  }
  yield()
  println("END")
}

suspend fun newRoutine() {
  val num1 = 1
  val num2 = 2
  yield()
  println("${num1 + num2}")
}
```

+ runBlocking : 일반루틴 세계와 코루틴 세계를 연결함 (중괄호 부터 코루틴 세계)
+ launch : 반환값이 없는 코루틴을 만든다.
+ suspend fun : 다른 suspend를 호출
+ yield() : 지금 코루틴을 중단하고 다른 코루틴이 실행되도록 한다. (스레드를 양보한다.)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/f1d02a1e-3f20-4c5d-878a-d3b5f2f6dcd7)

## 루틴과 코루틴
+ 루틴
  - 시작되면 끝날 때 까지 멈추지 않는다.
  - 한번 끝나면 루틴 내의 정보가 사라진다.
+ 코루틴
  - 중단되었다가 재개될 수 있다.
  - 중단되더라도 루틴 내의 정보가 사라지지 않는다.

## 스레드와 코루틴 차이
+ 프로세스가 스레드보다 큰 개념이 듯이
+ 스레드가 코루틴 보다 큰 개념이다.
+ 프로세스가 있어야만 스레드가 있을 수 있다.
+ 스레드가 프로세스를 바꿀 수는 없다.
+ 코루틴의 코드가 실행되려면, 스레드가 있어야만한다.
  - 하지만 중단되었다가 재개될 때 다른 스레드에 배정될 수 있다.

## 프로세스가 Context switching이 일어날 떄 특징
+ 프로세스는 독립된 메모리를 가지고 있어서, context switching이 일어날때 모든 메모리 교체가 교체되므로 비용이 많이 발생한다.
+ 스레드의 경우 Heap 메모리를 공유하고 stack만 교체되므로 프로세스보다는 비용이 적다.
+ 코루틴의 경우 메모리 전체를 공유한다. 따라서 스레드보다 context switching cost가 낮다.
  - 즉 두 코루틴이 동시에 실행되는 것처럼 보인다.
  - 하나의 스레드에서도 동시성을 확보할 수 있다.

## 정리

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/2ecbaa02-ac75-4efe-8a56-d31f06b762c3)

## 3. 코루틴 빌더와 Job

```kotlin
fun main(): Unit = runBlocking {
  printWithThread("START")
  launch {
    delay(2_000L)
    printWithThread("LAUNCH END")
  }
}
```
+ runBlocking이 끝날때 까지 스레드를 blocking시킨다.
  - 따라서 프로그램 진입할때 최초로 작성하거나 테스트코드 시작할때 작성하는게 좋다.
+ delay() : 특정 시간만큼 멈추고 다른 코루틴으로 넘김

## launch
+ 반환값이 없는 코드를 실행하지만
+ Job이라는 반환값을 리턴하기도함?

## join - 두개의 코루틴 다루기
+ 첫번째 코루틴에 join()을 사용하면 join()에 의해 코루틴 1이 끝날때 까지 대기했다가 코루틴2를 실행한다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/cc193cd5-0cf9-4a07-b401-a62ce6ab534d)

## async
+ launch랑 거의 같지만, 다른점은 주어진 함수의 실행 결과를 반환할 수 있다.
  - Deferred를 반환한다.
  - await : async의 결과를 가져오는 함수
  - 여러 API를 동시에 호출하여 소요시간을 최소화할 수 있다.
+ callback을 이용하지 않고 동기 방식으로 코드를 작성할 수 있다.

## async 주의 사항
+ CoroutineStart.LAZY 옵션을 사용하면, await()함수를 호출했을 떄 계산 결과를 계속 기다린다.
+ CoroutineStart.LAZY 옵션을 사용 후 start() 함수를 한번 호출해주면 괜찮다.

## 코루틴 취소
+ 코루틴을 적절히 취소하는 것은 중요하다.
+ 필요하지 않은 코루틴은 적절히 취소해 컴퓨터 자원을 아껴야 한다.
+ cancel() 함수를 활용하면 되지만..
  - 코루틴도 취소에 협조해 주어야 한다.

## 취소에 협조하는 방법 1
+ delay()나 yield()같은 kotlinx.coroutines 패키지의 suspend 함수 사용

## 취소에 협조하는 방법 2
+ 코루틴 스스로 본인의 상태를 확인해 취소 요청을 받았으면, CancellationException을 던지기
  - isActive : 현재 코루틴이 활성화 되어 있는지, 취소 신호를 받았는지
  - Dispatchers.Default : 우리의 코루틴을 다른 스레드에 배정
 
## 코루틴의 예외처리와 Job의 상태 변화

### launch와 async의 예외 발생 차이
+ launch : 예외가 발생하면, 예외를 출력하고 코루틴이 종료
+ async : 예외가 발생해도, 예외를 출력하지 않음. 예외를 확인하려면, await()이 필요하다

### 자식 코루틴의 예외는 부모에게 전파된다.
+ launch건 async건 자식 코루틴의 예외는 부모에게 전파된다.

### 만약 자식 코루틴의 예외를 부모에게 전파하기 싫다면?
+ 루트 코루틴을 만드는거 외에 SupervisorJob()을 이용하는 방법도 있다.

### 예외를 다루는 방법
1. 직관적인 try-catch-finally
2. CoroutineExceptionHandler를 이용

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/37b757d3-d0e8-48b3-8f4a-0b7e246f8db3)

### CoroutinExceptionHandler 주의할 점
1. launch에만 적용 가능하다
2. 부모 코루틴이 있으면 동작하지 않는다.

### 궁금한점
+ 취소도CancellationException이라는 예외였는데 일반적인 예외랑 어떻게 다른걸까?

1. case 1 : 발생한 예외가 CancellationException인 경우 취소로 간주하고 부모 코루틴에게 전파 X
2. case 2 : 그 외 다른 예외가 발생한 경우 실패로 간주하고 부모 코루틴에게 전파 X

+ 다만 내부적으로는 취소나 실패 모두 "취소됨" 상태로 관리한다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/09137a5e-dd72-4129-b757-27e676d8129c)

> 그 이유는 다음시간..
