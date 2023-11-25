
<img width="525" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/b8a549c7-f6c4-4a4d-9309-b66dbc541062">

## 소개

+ 분산환경에서의 서버들이 공통으로 사용할 수 있는 해시 테이블로 생각
+ 오픈 소스 인메모리 저장소 - 램에 저장

## 특징
1. in-memory : 모든 데이터를 RAM에 저장 (백업/ 스냅샷 제외)
2. single threaded : 단일 thread에서 모든 task 처리
3. cluster mode : 다중 노드에 데이터를 분산 저장하여 안정성, 고가용성 제공
4. persistence : RDB(Redis Database) + AOF(Append only file) 통해 영속성 옵션 제공
5. pub/sub : pub/sub 패턴을 지원하여 손쉬운 어플리케이션 개발 (채팅, 알림 등)

## 장점
+ 높은 성능 : 모든 데이터를 메모리에 저장하기 때문에 빠른 읽기/쓰기
+ Data Type 지원 : Redis에서 지원하는 Data type을 잘 활용하여 다양한 기능 구현
+ 클라이언트 라이브러리 지원 : python, java, javascript 등 다양한 언어로 작성된 클라이언트 라이브러리 지원
+ 다양한 사례 / 강한 커뮤니티 : Redis를 활용하여 비슷한 문제를 해결한 사례가 많고, 커뮤니티 도움 받기 쉽다.


## 사용사례
+ Caching : 임시 비밀번호, 로그인 세션 등등
+ Rate Limiter : Fixed-Window / Sliding-Window Rate Limiter (비율 계산기)
+ Message Broker : 메시지 큐 (Message Queue)
+ 실시간 분석 / 계산 : 순위 표(Rank), 반경 탐색(Geofencing), 방문자 수 계산(Visitors Count)
+ 실시간 채팅 : Pub/Sub 패턴

## 영속성에 대해
+ Persistence : Redis는 주로 캐시로 사용되지만 데이터 영속성을 위한 옵션 제공
  - SSD와 같은 영구 적인 저장 장치에 데이터 저장

## 영속성 적용 방식들
+ RDB(Redis Database) : Point-in-time snapshot -> 재난 복구 또는 복제에 주로 사용
  - 일부 데이터 유실 위험이 있고, 스냅샷 생성 중 클라이언트 요청 지연 발생

+ AOF(Append Only File)
  - Redis에 적용되는 Write작업을 모두 log로 저장
  - 데이터 유실의 위험이 적지만, 재난 복구시 Write 작업을 다시 적용하기 때문에 RDB보다 느림
 
+ RDB + AOF : 함께 사용
