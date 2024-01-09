# Redis 사용시 주의사항

## O(N)

+ O(N) 명령어 : 대부분의 명령어는 O(1) 시간복잡도를 갖지만, 일부 명령어의 경우 O(N)
+ 주의사항 : Redis는 Single Thread로 명령어를 순차적으로 수행하기 때문에, 오래 걸리는 O(N) 명령어 수행시 전체적인 어플리케이션 성능 저하
+ 예시 : KEYS : 지정된 패턴과 일치하는 모든 키 조회
  - production 환경에서 절대 사용 금지 -> Scan명령어로 대체
+ SMEMBERS : SET의 모든 member 반환 (N = Set Cardinality)
+ HGETALL : HASH의 모든 field 반환 (N = Size of Hash)
+ SORT : List, Set, ZSet의 item 정렬하여 반환

## Thundering Herd Problem
+ 병렬 요청이 공유 자원에 대해서 접근할 때, 급격한 과부하가 발생하는 문제

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/bf78244e-17f3-472a-bfee-dd4cd1e3b230)

+ 순간적인 캐시 미스로 인해, 순간 요청이 application에 여러번 발생하게 된다.
+ cron job을 통해 통계 캐시를 주기적으로 최신화 하여 예방하기도 한다.

## Stale Cache Invalidation
+ Cache Invalidation : 캐시의 유효성의 손실되었거나 변경되었을 때, 캐시를 변경하거나 삭제하는 기술
+ 캐시와 실제 값이 다른 경우를 말한다.
