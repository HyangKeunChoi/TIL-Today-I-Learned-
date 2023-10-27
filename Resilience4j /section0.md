## Resilience4j
+ Resilience : 회복 탄력성, 장애 내성
+ Hystrix : 더이상 개발 되지 않음, Resilience4j 사용권장

### Resilience4j의 핵심 기능
1. CircuitBreaker - 다룰 예정
2. Bulkhead
3. RateLimiter
4. Retry - 다룰 예정
5. TimeLimiter
6. Cache

### CircuitBreaker
+ 서버가 너무 트래픽을 많이 받아서 회복을 위해 잠시 트래픽을 차단시켜야 한다면?
  - 원래 기능을 대체 할 수 있는 기능(fallback) 실행
 
### Retry 고려해야 하는 것들
1. 몇번까지 재시도 할 것인가?
2. 재시도 간격은 얼마나 길게 줄 것인가?
3. 어떤 상황을 호출 실패로 간주할 것인가?

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/1a9cb3c9-b33b-44ca-b533-3c9153910c46)

> 기능중 일부를 포기한다
> 
> 상품 자체를 못보여주는 것보다 리뷰 정보 같은 부수 정보는 안보여줘도 된다.
