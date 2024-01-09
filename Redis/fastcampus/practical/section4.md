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

## SET NX/XX
+ NX : 해당 Key가 존재하지 않는 경우에만 SET
+ XX : 해당 Key가 이미 존재하는 경우에만 SET

> NX또는 XX의 SET이 동작하지 않는 경우 nil 응답한다.

+ SET greeting hello NX
+ SET greeting hi XX

## Pub/Sub
+ Publisher와 Subscriber가 서로 알지 못해도 통신이 가능하도록 decoupling된 패턴
+ Publisher는 Subscriber에게 직접 메시지를 보내지 않고 Channel에 Publish
+ Subscriber는 관심이 있는 Channel을 필요에 따라 Subscribe하며 메시지 수신
> vs Stream : 메시지가 보관되는 Stream과 달리 Pub/Sub은 Subscribe 하지 않을 때 발행된 메시지 수신 불가

## Pipeline
+ 다수의 commands를 한번에 요청하여 네트워크 성능을 향상 시키는 기술
+ Round-Trip Times 최소화

## Transaction
+ 다수의 명령을 하나의 트랜잭션으로 처리 -> 원자성 보장
+ 중간에 에러가 발생하면 모든 작업 Rollback
+ 하나의 트랜잭션이 처리되는 동안 다른 클라이언트의 요청이 중간에 끼어들 수 없음
+ Pipeline과 Transaction을 동시에 사용 가능
+ MULTI : 트랜 잭션 시작
+ DISCARD : 트랜잭션 롤백
+ EXEC : 트랜잭션 종료

