## One Time Password (OTP)
+ 인증을 위해 사용되는 임시 비밀번호 (6자리 랜덤 숫자)
+ 유효시간만큼만 TTL

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/4bff3626-071e-4455-bb0c-4a994db834a5)

## Distributed Lock (분산락)
+ 분산 환경의 다수의 프로세스에서 동일한 자원에 접근할 때, 동시성 문제 해결
+ NX를 통해 해당키가 존재하지 않는 경우에만 락 획득, 존재하여 획득할 수 없는 경우 nil을 리턴해 프로세스 대기 시킴
+ 작업 종료 후 lock 삭제
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/b446d08c-2fab-43ad-91b4-d7848cf02aef)

## Rate Limiter
+ 시스템 안정성/보안을 위해 요청의 수를 제한하는 기술
+ 특정 IP에 대한 요청 수 제한(IP-Based)
+ 유저 제한(User-Based)
+ 어플리케이션 제한(Application-Based)
+ Fixed-window Rate Limiting : 고정된 시간 안에 요청 수를 제한하는 방법

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/87d50bac-a79c-4c75-b232-9f4715e55dc4)

+ 0시 10분에 대한 요청을 ip와 분을 가진 키로 매핑 : 10분 부터 11분사이 요청 횟수 저장
+ 요청 제한이 20번이면 해당 키로 조회한 value가 20일 경우 Too Many Request를 발생한다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/8c8385cd-eaa4-4ba8-bad7-2739aaf93c75)

## List - SNS Activity Feed
+ Activity Feed : 사용자 또는 시스템과 관련된 활동이나 업데이트를 시간순으로 정렬하여 보여주는 기능
+ Fan-Out : 단일 데이터를 한소스에서 여러 목적지로 동시에 전달하는 메시징 패턴

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/b3a7f7f3-614c-4ceb-a4ad-eb097b89e251)

## Shopping Cart
+ 수시로 변경이 발생할 수 있고, 실제 구매로 이어지지 않을 수도 있다.
+ 장바구니 담을 경우 SADD, 조회할 경우 SMEMBERS
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/23944c4e-9cb0-4e84-968e-cdd8aa0db0e1)

## Login Session
+ 사용자 로그인 상태를 유지하기 위한 기술
+ 동시 로그인 제한 : 로그인시 세션의 개수를 제한하여, 동시에 로그인 가능한 디바이스 개수 제한

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/347306b4-9002-4977-8173-2fbfff9609ce)

## Sliding Window Rate Limiter
+ 시간에 따라 Window를 이동시켜 동적으로 요청수를 조절하는 기술
+ vs : Fixed Window : 시간마다 허용량이 초기화 됨
+ Sliding Window는 시간이 경과함에 따라 window가 같이 움직인다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/203ce77f-e746-44ca-85f1-c97b09bc5950)

+ sorted set을 이용한다.
+ 유닉스 타임
+ ZREMRANGEBYSCORE로 빨간 부분은 삭제
+ ![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/116781fe-f9cf-412b-8ba1-265b2b4706a3)

## Geofencing
+ 위치를 활용하여 지동 상의 가상의 경계 또는 지리적 영역을 정의하는 기술

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/563c0390-f631-4c74-af87-a9c56d4af197)

## 사용자 Online Status
+ Bitmap이용
+ 사용자의 현재 상태를 표시하는 기능
+ 실시간성을 완벽히 보장하지는 않는다. 수시로 변경되는 값이다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/e7be1ca3-784f-41fd-9e51-b45a473cc9dc)

## 데이터 타입 활용 (Visitor Count)
+ Visitor Count Approximation : 방문자 수를 대략적으로 추정하는 경우, 정확한 횟수를 셀 필요 없이 대략적인 어림치만 알고자 하는 경우
+ HyperLogLog를 이용

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/5e57c069-4a80-4bb6-8d75-da6fdc2f594a)

## Unique Events
+ BloomFilter 이용
+ Unique Events : 동일 요청이 중복으로 처리되지 않기 위해 빠르게 해당 item이 중복인지 확인하는 방법

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/5ced99af-9f55-4a97-af15-80523c6f96f9)
