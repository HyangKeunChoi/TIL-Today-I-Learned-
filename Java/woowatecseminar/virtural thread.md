## virtual thread 소개
+ 전사 게이트웨이 시스템 개발
  - kotlin coroutine
  - java project loom
 
+ virtual thread : project loom으로 시작된 경량 스레드 모델
+ 스레드생성 및 스케줄링 비용이 기존 스레드보다 저렴
+ 스레드 스케줄링을 통해 nonblocking io 지원
+ 기존 스레드를 상속하여 코드 호환

### virtual thread 장점
+ 자바 스레드는 생성 비용이 크다.
  - 스레드 풀이 존재하는 이유
  - 사용하는 메모리 크기가 크다.
  - os에 의해 스케줄링된다. (시스템 콜 발생)
+ virtual thread는 생성 비용이 작다.
  - 스레드 풀 개념x
  - 사용 메모리 크기가 작다.
  - os가 아닌 jvm내 스케줄링

<img width="334" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/170bcc3e-d48a-4c70-85fd-c9371e7844d2">

+ 기본 스레드 대비 버츄얼 스레드 생성이 매우 빠름.

### non blocking i/o
+ jvm 스레드 스케줄링
+ continuation이라는 개념
 
<img width="359" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/f4608319-4830-4bac-9fa7-740dea4d7ac2">

### 기존 스레드 상속
+ extends BaseVirtualThread

### 일반 스레드
+ 플랫폼 스레드
+ OS에 의해 스케줄링
+ 커널 스레드와 1대1 매칭
+ 작업 단위 Runnable

### virtual 스레드
+ 가상 스레드
+ jvm에 의해 스케줄링
+ 캐리어 스레드와 1:N 매핑
+ 작업 단위 Continuation

### Continuation 작업 단위
+ 실행 가능한 작업 흐름
+ 중단 가능
+ 중단 지점으로부터 재실행 가능

### Continuation 사용 이유
+ Thread는 작업 중단을 위해 커널 스레드를 중단
+ virtual thread는 작업 중단을 위해 continuation yield
+ 작업이 block되어도 실제 스레드는 중단되지 않고 다른 작업 처리
+ 커널 스레드 중단이 없으므로 시스템콜 x -> 컨텍스트 스위칭 비용이 낮음

### 성능 
+ I/O Bound 작업은 더 높은 처리량
+ CPU Bound 작업은 더 낮은 처리량
+ Thread 서버는 특정 vuser수 부터 장애 발생함

## 주의 사항
+ blocking carrier thread(pin)
+ 병목 가능성이 존재
+ 사용 라이브러리 release 점검
+ 변경 가능하다면 java.util의 ReentrantLock을 사용하도록 변경
+ cpu bound인 상황에서 사용하지 않는다.

## 결론
+ virtual thread는 가볍고 빠르고 nonblocking인 경량 스레드
+ virtual thread는 jvm 스케줄링, continuation을 이용 한다.
+ thread per request 사용중이고, i/o blocking time이 주된 병목인 경우 고려
+ 쉽게 적용가능
  - reactive가 러닝커브로 부담되는 경우
  - kotlin coroutine이 러닝 커브로 부담되는 경우

#### ref
+ https://www.youtube.com/watch?v=BZMZIM-n4C0
