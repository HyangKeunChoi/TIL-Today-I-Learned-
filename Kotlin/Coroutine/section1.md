## 코투린이란?
+ 협력하는 루틴

## 루틴과 코루틴의 차이
+ 루틴에 진입하는 곳이 한 군데이며, 종료되면 해당 루틴의 정보가 초기화된다.

## 코틀린이란?
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

+ runBlocking : 일반루틴 세계와 코투린 세계를 연결함 (중괄호 부터 코루틴 세계)
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

