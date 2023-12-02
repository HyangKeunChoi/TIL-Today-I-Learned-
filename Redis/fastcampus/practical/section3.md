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
