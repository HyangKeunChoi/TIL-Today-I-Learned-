## section3

## Strings
+ 문자열, 숫자, serialized object 등 저장
+ SET lecture redis
+ MSET : 다수의 스트링 저장
  - MSET price 100 language ko
+ MGET : 다수의 키의 값을 한번에 반환
  - MGET price language
+ INCR : increase명령어
  - INCR price
+ INCRBY price 10 : 특정값을 더할떄 사용
  - INCRBY price 9
+ 키를 만들때 일반적으로 콜론을 만든다.

## Lists
+ string을 linked list로 저장 -> push /pop에 최적화 O(1)
  - queueF(FIFO) / stack(FILO) 구현에 사용
+ LPUSH queue job1 job2 job3 : 3
+ RPOP queue : job1 출력

+ LPUSH stack job1 job2 job3 : 3
+ LPOP stack : job3 출력
+ LPUSH queue job4 job5
+ LRANGE queue 0 -1 : 가장 첫번째 item부터 마지막 아이템까지 출력
+ LRANGE queue -2 -1 : job3 job2 출력
+ LRANGE queue 2 3 : job3 job2 출력
+ LTRIM queue 0 1 : OK
+ LRANGE queue 0 -1 : job5 job4만 남는다

## Sets
+ Sets : Unique string을 저장하는 정렬되지 않은 집합

## 명령어
+ SADD : 값 추가
+ SMEMBERS : 모든 멤버 조회
+ SCARD : set의 카디널리티 출력 (고유한 아이템의 갯수)
+ SISMEMBER : 값이 있는지 확인
+ SINTER : 공통을 출력 (교집합)
+ SDIFF : 차이를 출력 (차집합)
+ SUNION : 합집합 출력

## hashes
+ field-value 구조를 갖는 데이터 타입
  - 다양한 속성을 갖는 객체의 데이터를 저장할 때 유용
+ HSET lecture name inflearn-reids price 100 language ko : lecture라는 키로 3개의 필드 저장
+ HGET lecture name : 하나의 필드 조회
+ HMGET lecture price language invalid : 다수의 필드 조회
+ HINCRBY lecture price 10 : 숫자형으로 저장된 string value를 특정 값만큼 더하는 명령어

## Sorted Sets = ZSets
+ ZSets : 중복없는 Unique한 String을 저장하지만 score라는 추가적인 속성이 있어서 socre를 통해 정렬된 집합 (Set의 기능 + 추가로 score 속성 저장)
+ 내부적으로 Skip List + Hash Table로 이루어져 있고, score 값에 따라 정렬 유지
+ score가 동일하면 lexicographically(사전 편찬 순) 정렬
+ ZADD points 10 TeamA 10 TeamB 50 TeamC

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/87df7ea7-bab5-43d5-8e15-3d67115f1790)

+ ZSets은 순서를 갖기때문에 Range로 범위 조회 가능
+ ZRANGE points 0 -1
+ ZRANGE points 0 -1 REV WITHSCORES
+ ZRANK points TeamA

## Streams
+ append-only log에 consumer groups과 같은 기능을 더한 자료 구조
  - append-only 란? 데이터 저장 알고리즘에서 데이터가 수정되거나 삭제되지 않고 항상 추가만 되는 구조
+ 추가 기능 1 : unique id를 통해 하나의 entry를 읽을 때, O(1) 시간 복잡도
+ 추가 기능 2 : Consumer Group을 통해 분산 시스템에서 다수의 consumer가 event 처리

<img width="697" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/a9ef489d-9f58-4522-bfca-e2452d642fb3">

### 명령어
+ XADD events * action like user_id 1 product_id 1
+ XRANGE events - +
  - 가장 처음에 들어갔던 이벤트 부터 마지막 이벤트까지 출력
+ XDEL events ID
  - events 삭제

## Geospatials
+ Geospatial Indexes : 좌표를 저장하고, 검색하는 데이터 타입, 거리 계산, 범위 탐색 등 지원
+ GEOADD seoul:station
+ GEODIST seoul:station hong-dae gang-nam KM(단위: 키로미터)
  - 거리 차이

## Bitmaps
+ 실제 데이터 타입은 아니고, String에 binary operation을 쉽게 사용할 수 있게 만들어 놓은 인터페이스라 생각
+ 최대 42억개 binary 데이터 표현 = 2의 32승
+ SETBIT user:log-in:23-01-01 123 1
+ SETBIT user:log-in:23-01-01 456 1
+ BITCOUNT user:log-in:23-01-01
+ BITOP AND result user:log-in:23-01-01 user:log-in:23-01-02
+ GETBIT result 123

## HyperLogLog
+ 집합의 cardinality를 추정할 수 있는 확률형 자료구조
+ 정확성을 일부 포기하는 대신 저장공간을 효율적으로 사용(평균에러 0.81%)
  - 근사치만 알아도 되는 경우에 사용
+ 원리 : 멤버의 값을 해싱하여 버킷이라는 단위로 준비해서 해시값에 맞게 표시
  - 해시 충돌이 일어나는 경우 정확하지 않은 값 반환
  - 실제 값을 저장하지 않기 때문에 매우 적은 메모리 사용, 모든 아이템을 출력하는 경우에는 활용할 수 없다.
+ PFADD fruits apple orange grape kiwi
+ PFCOUNT fruits

## BloomFilter
+ element가 집합 안에 포함되어 있는지 확인할 수 있는 확률형 자료 구조 (=membership test라는 기능 구현할때 사용)
+ 정확성을 일부 포기하는 대신 저장공간을 효율적으로 사용
+ false positive 문제 : element가 집합에 실제로 포함되지 않는데 포함 되었다고 잘못 예측하는 경우
+ vs set : 실제 값을 저장하지 않기 때문에 Set에 비해 매우 적은 메모리 사용
+ BF.MADD fruits apple orange
+ BF.EXISTS fruits apple
