# section3

### 상태 변화 관련 주요 설정들
+ slidingWindowType : 최근을 기준으로 몇개씩만 상태를 본다.
+ slidingWindowSize
  - COUNT_BASED : 값을 기준으로 (100개가 디폴트)
  - TIME_BASED : 시간을 기준으로 (몇초를 기준으로)
+ failureRateThreshold : 몇번 실패해야 서킷이 열리는지
  - Threshold : 임계치, 기준치
+ minimunNumberOfCalls : 해당 설정을 넘어간 순간부터 실패로 계산
  - Sliding Window보다 큰 값으로 지정하면 의미 없음
+ waitDurationInOpenState : 오픈으로 바뀐 다음에 얼마나 동안 지속할지
+ permittedNumberOfCallsInHalfOpenState : halfOpen에서 정상적인 상태로 갈 수 있는 지에 대한 상태 점검하는 횟수를 지정
+ automaticTransitionFromOpenToHalfOpenEnabled : 자동으로 halfOpen 으로 갈지 말지
+ slowCallDurationThreshold : 슬로우 call을 몇초로 간주할 건지
+ slowCallRateThreshold : 느린 호출의 비율이 몇 이상으로 간주할 건지

### 주요 설정 알아보기

+ onEvent
+ onSuccess
+ onCallNotPermitted : 서킷프레이커가 오픈되어 요청이 차단될때 실행되는 이벤트 핸들러
+ onError
+ onIgnoredError : ignore exception이 발생했을때 실행되는 이벤트 핸들러
+ onStateTransition
+ onSlowCallRateExceeded
+ onFailureRateExceeded

## 이벤트 핸들러를 어떻게 활용할 것인가?
1. 로그로 남겨서 모니터링할때 사용한다.
2. 특정 서버에서 state transition이 발생해서 open상태가 되었을때 이벤트 핸들러를 통해 다른 서버들도 상태를 전파 받을 수 있다.

## 서킷의 상태를 어떻게 강제로 바꾸나요?
+ actuator

## 어떤 예외를 recordException으로 지정할까?

### 주의할 예외
+ 유효성 검사나 NullPointerException처럼 서킷이 열리는 것과 무관한 예외는 recordExceptions로 등록X
+ Exception이나 RuntimeException처럼 너무 높은 수준의 예외 역시 recordExceptions로 등록 X
+ slow call에만 의존하지 말기
  - 타임아웃 걸어서 예외 던져주기

## fallback 활용하기

#### fallback 메서드가 실행되는 경우
1. Record Exception이 발생했을 떄
2. Ignore Exception이 발생했을 때
3. 서킷이 OPEN되어 요청이 실행되지 않을 때

#### fallback으로 할 수 있는 일
+ 로깅 or DB에 저장
+ 실패 했던 요청을 모아서 재시도
+ 클라이언트에 반환
  - 저장소에 있는 데이터를 조회하지 못하면 캐시 데이터 라도 조회해서 반환
 
