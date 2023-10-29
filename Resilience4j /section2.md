## CircuitBreaker

### 서킷 상태 3가지
+ close : 정상적인 상태, 트래픽이 들어오고 있는 상태
+ open : 차단된 상태
+ half_open : 차단된 상태에서 정상적인 상태로 갈 수 있는지 점검하는 상태

> 회로 차단기가 내려가야 정상이니까 그 개념으로 생각

<img width="914" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/3ed6bbb8-d9be-4180-8dcc-c7abc5d46bb4">

+ CircuitBreaker설정 관련 yaml파일 보기
  - docs도 보기

+ RecordException : 실패로 간주할 익셉션
+ IgnoreException : 서킷 브레이커가 동작하는데 영향을 주지 않는 예외
  - 주의할 점은 fallback을 타는건 동일하다.
 
