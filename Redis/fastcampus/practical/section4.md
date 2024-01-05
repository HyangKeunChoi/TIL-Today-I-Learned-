## Section4
## Redis 특수 명령어

### 데이터 만료
+ 데이터 만료 시키는 기능 존재
+ 데이터를 특정 시간 이후에 만료 시키는 기능
+ TTL(Time To Live) : 데이터가 유효한 시간(초 단위)
+ 특징 : 데이터 조회 요청시에 만료된 데이터는 조회되지 않음
+ 데이터가 만료되자마자 삭제하지 않고, 만료로 표시했다가 백그라운드에서 주기적으로 삭제
+ SET greeting hello
+ EXPIRE greeting 10
+ TTL greeting
+ SETEX greeting 10 hello : 데이터 저장 + 만료시간 설정
