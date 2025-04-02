## 왜 속도가 중요할까요?

+ 성능은 사용자 유지를 좌우
+ 성능은 전환율 향상을 좌우
+ 성능은 사용자 경험을 좌우
+ 성능은 사람을 좌우

#### 로딩 (LCP)
+ 화면 다 그려지는데 걸리는 시간
+ 크롬 개발자 도구에 performance insights
  + measure page load

## 성능의 주요 지표
+ 사용자 : 부하를 주는 수
+ 응답시간 : 각 요청에 대한 응답 시간
+ 초당 처리량 : tps
+ 리소스 사용량 : cpu, 메모리, 네트워크 등..

#### Active user
+ 서버에 부하를 주고 있는자
+ 성능 테스트시 Virtual User와 거의 동일

#### Concurrent user
+ 서비스에 접속한 사용자
+ 웹 페이지를 띄워 놓은 사용자나 앱을 실행하고 있는 사용자

#### 응답시간
+ CPU time : CPU 연산을 기다리는데 소용되는 시간
+ Wait time : DB의 결과를 기다리거나 API호출 후 대기하는 시간

#### 처리량
+ TPS
+ 1초에 얼마나 많은 요청을 처리 가능한지 확인
+ 기능별 tps를 측정하는 것도 어느정도 의미가 있음
+ tps가 최대치에 도달한 이후에는 더이상 증가하지 않음

## 주요 성능 병목 지점

#### 병목의 특징
+ 하나의 병목을 없애면 다른 병목이 올 수 있다.
+ 암달의 법칙
 
#### DB 부하가 가장 병목인 경우가 많음

<img width="672" alt="image" src="https://github.com/user-attachments/assets/0572a83b-7afb-477d-b9e7-a67a335f5376" />

#### 네트워크 병목도 발생한다.

#### CPU 병목
+ 사용자가 많아서
+ 계산이 많아서
+ 사용자도 많고 계산도 많아서
+ 사용자가 많은 속도 빠름 -> 수평 확장
+ 사용자가 많은데 응답속도 느림 -> 튜닝 후 수직이나 수평확장
+ 계산이 많고 응답속도느림 -> 튜닝 후 슂ㄱ이나 수평확장 추천
+ 사용자도 많고 계산도 많음 -> 무조건 튜닝 후 수직이나 수평확장

#### 메모리
+ 자바 기반의 애플리케이션은 메모리가 병목일 경우는 많지 않음
+ JVM이 시작되면서 최대 메모리 사용량을 할당하기 때문
+ 메모리를 늘릴수록 GC 시간이 오래걸리기 때문에 무조건 늘린다고 좋은건 아님

#### 디스크
+ 가능한 ssd나 그보다 더 빠른 스토리지를 쓰면 문제는 해결될 수 있음

#### IDC
+ IDC에서는 수많은 네트워크 장비들이 존재

## 성능 확인 방법
+ 모니터링 도구 : grafana, prometheus
+ 성능 분석 도구 : 운영도구가 아닌 개발용 도구
  - CPU 측정
  - Memory 측정
  - Thread 측정 : Thread의 Lock이 발생할 경우 분석하는데 용이함
  - 프로 파일러
    - jProfiler
    - YourKit
+ 성능 테스트 도구 (apm)
  - PinPoint
  - scouter
  - Whatap
  - DataDog
  - newrelic
 
## JVM
+ JVM은 JRE의 일부분에 속함

#### JVM 메모리 영역

<img width="578" alt="image" src="https://github.com/user-attachments/assets/2cc58cfb-7c62-4855-9054-54180bc34424" />

### Execution Engine
+ Interpreter : 바이트 코드를 라인단위로 읽어서 번역하고 실행
+ JIT Compiler : interperter를 효율적으로 활용하기 이해 사용
+ GC : 사용하지 않는 객체 정리

## Visual VM
+ JMX : 자바 프로세스를 모니터링할수 있는 그런 값들

## 서버에 성능에 영향을 주는 것들 (리눅스에서 모니터링 하는법)
+ top
  - load average : cpu의 부하 사항 (1분 5분 15분)
  - zombie 프로세스는 죽여야함
  - us : 유저 cpu (어플리케이션에서 점유)
  - sy : 시스템 cpu
  - wa : wait
  - 
+ vmstat
+ sar
+ /proc

## 4. 성능 테스트
+ Ramp-up load : 점진적으로 부하
+ Cruising load : 지속적으로 부하
+ Spike load : 순간적으로 높은 부하

#### 성능 테스트 주요 용어
+ VUser
+ TPS
+ 응답시간
+ 대기시간 (think time)
+ Load generator : 부하 에이전트, 부하 발생기 라고함
+ 리틀의 법칙
+ 표준 편차는 낮을 수록 좋다. (거의 유저간의 차이가 없는 상황)

#### JMH
+ Java Microbenchmark harness
+ @BenchmarkMode
  - Throughput
  - Average Time
  - ..
+ @State 
+ DB연동 / 타 서비스 연계된 기능 비교는 성능 테스트 도구 활용

#### Gatling

## GC
+ 더이상 사용하지 않는 객체를 청소
+ Miner GC(Young GC) : eden, survior
  - 생긴지 얼마 안된 객체는 보통 eden으로 간다.
  - 보통 eden에서 survivor로 계속 이동한다.
  - 그 다음 survivor로 계속 이동
+ Major GC(Full GC) : old, metaspace

#### 왜 영역을 나누어 놓은것인가
+ 대부분은 minor에서 사라짐
+ 계속 살아있는것들만 old에서 체크
+ jstat을 활용하면 jvm을 쉽게 모니터링할 수 있다.

#### GC 종류
+ Serial GC : 옛날 GC
+ Parallel Collector : 컴팩션 작업이 필요
+ G1 GC : 일반적인 GC
+ Shenandoah GC
+ ZGC
+ GC는 하나만 쓸 수 있다.

### FAQ
+ GC옵션은 모든 서비스에서 동일하게 설정했는데 그래도 되나요?
  - 모르겠으면 useG1Gc만 쓰는거 추천
  - 프로그램마다 메모리 차지하는 게 다르니까 각 특징에 맞는 GC쓰는게 좋다.

+ Old 영역 메모리 사용량이 늘어나기만 해요
  - Full Gc해서 30프로 만 계속 남는다면 그건 일반적인 현상
  - 힙 덤프 떠서 확인 해야함 (힙덤프 뜨면 멈추니까 주의)

+ Concurrent Mark and Sweap이라는것도 있던데요?
  - 이를 보완한게 G1GC이므로 이걸 쓰는걸 추천
 
+ GC시간 때문에 고려해야할 것은?
  - 타임아웃시간이 GC시간보다 많은지 확인 > 많으면 괜찮, 적으면 문제

+ G1GC 이후의 가비지 컬렉터를 사용할 경우에는 웬만하면 튜닝하려고 하지말것

#### jstats 모니터링 방법

## 자바 개발하면서 성능상 유의할 점
1. String - StringBuilder, StringBuffer, StringJoiner

2. stream vs parallelStream - parallelStream에서 스레드 풀이 코어 갯수만큼 씀
- 웹 개발하면서는 parallelStream 쓰지말자
- 배치에서 사용하고 싶으면 parallel stream support를 쓰자
   
3. Date format이 문제가 되는 이유
- 서버와 서버간의 통신할때는 json이나 xml을 쓰지 말아야 한다.
- 메모리를 너무 많이 잡아 먹는다.
- 대안 : protobuf, gRPC

4. Log는 반드시 필요한 곳에서만 사용한다.

#### 개발보다 더 중요한 성능에 영향을 주는 설정
+ Thread pool
+ DB connection pool

#### Thread pool 개수를 너무 작게 잡으면
+ 요청을 처리하지 못하고 대기하게 됨
+ 요청이 많을수록 CPU 사용량이 더 이상 증가하지 않음

#### DB connection pool

## Troubleshooting 개요

#### thread 문제가 있는지 확인하는 법
+ Thread dump : 어떤 스레드가 어떤 작업을 하고 있는지, 현재 시점의 상태를 덤프
+ jstack [pid] : 일반적인 스레드 덤프 뜨는법
+ kill -3 [pid]
  - -9옵션은 사용하면 안된다!
