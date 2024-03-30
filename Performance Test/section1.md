## 지연시간과 처리량
+ 지연시간(latency) : 클라이언트가 요청을 보낸 후 응답을 받기까지 걸린 시간
+ 처리량(throughput) : 단위 시간동안 몇건의 요청을 처리할 수 있는가? 주로 tps 단위
+ 대역폭(Bandwidth) : 단위시간동안 네트워크 전송량

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/b2640deb-d2e5-4fbb-b78c-83e05b04d13b)

## 운영체제 지식

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/5d65a919-d284-4d5c-8fcb-762a1087e61c)

> 페이징 : 메모리중 일부를 디스크에(가상 메모리) 저장했다가 다시 불러오는 것

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/76ab45dc-08a7-436e-8313-6ce7cc661d44)

### 지연시간, 처리량과의 관계

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/4b91f8af-623c-4608-9efe-f6f959793cd6)

## 네트워크 지식

### 네트워크 통신 발생
+ DB 호출
+ 또 다른 API 호출
+ 개발자 도구에서 실제 웹 페이지 로딩시간이 측정된다
+ 지리적 위치에 따라 네트워크 시간 차이가 많이 난다.

### 네트워크 대역폭과 지연시간의 관계
+ 대역폭보다 큰 데이터는 전송되지 못하고 쌓인다.
  - 대용량의 파일을 다운로드 하고 있을 때 웹 서핑을 했더니 웹 페이지가 느리게 뜸
  - 고행상도의 이미지가 많이 포함된 페이지에 접속했을때 이미지들이 느리게 로딩됨
+ 대역폭은 경로상 가장 낮은 대역폭에 맞춰진다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/723d8bf0-2844-4261-9bfe-53ca2f3d5a66)

## 데이터 베이스
+ 지연시간이 길어지는 상황 : 많은 요청이 들어올때
+ 많은 데이터 중 특정 데이터를 찾아야 할때
+ 락이 너무 자주 걸리는 경우
+ SSD가 HDD보다 빠르고, 용량 작고 비싸다

