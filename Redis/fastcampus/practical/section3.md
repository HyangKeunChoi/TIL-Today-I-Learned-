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
