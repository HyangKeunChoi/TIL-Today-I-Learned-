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
