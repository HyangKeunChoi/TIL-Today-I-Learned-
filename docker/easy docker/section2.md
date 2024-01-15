## 이미지
+ 이미지 : 특정 시점의 파일 시스템(디렉터리)를 저장한 압축 파일

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/3974fddf-2285-4bd4-8ddd-c2258ecfc7fe)

+ 이미지 자체가 실행할 준비까지 완료된 상태이다.
+ 도커를 사용하는 목적 = 가상화 서버를 빠르고 가볍게 운영하기 위해 사용
+ 이미지 = 특정 서버를 실행할 수 있는 상태를 저장한 압축 파일
  - 다른사람이 만든것을 사용할 수도 있고 직접 만들 수 도 있다.
 
## 이미지와 컨테이너 차이

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/c43c6817-3f37-4c5e-9336-7049ce4beb03)

+ 이미지와 컨테이너 관계는 프로그램과 프로세스의 관계와 같다.

## 이미지 조회
+ docker image ls
+ docker image ls 이미지명

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/e8b5cb5d-7d5b-4df1-a1d4-65588b28dc29)

## 실행중인 컨테이너 삭제
+ 실행중인 컨테이너는 원래 삭제 불가 -> 옵션을 줘야한다.
+ docker rm -f

## 이미지 메타데이터
+ 이미지의 메타데이터란? 이미지에 대한 정보를 기술

## 메타데이터 확인 명령어(inspect)
+ docker image inspect 이미지명 : 이미지의 메타데이터 확인
+ docker container inspect 컨테이너명 : 실행 중인 컨테이너 메타데이터 확인
+ docker run 이미지명 (실행명령) : 컨테이너 실행 시 메타데이터의 cmd 덮어쓰기
+ docker run --env KEY=VALUE 이미지명 : 컨테이너 실행 시 메타데이터의 env 덮어쓰기

cf. docker ps -a : 종료된 컨테이너 까지 출력

## 데몬

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/d1d7be2d-714d-4ec1-b479-c72bc9861296)

## env

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/7965005f-a96c-44dc-a133-3b46b95f2939)

## 컨테이너의 라이프 사이클

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/488ee878-1dda-43b4-bb17-c98e3738a3df)

+ docker create : 생성
+ docker start : 실행
  - docker restart : 재실행
+ docker run = created + running
+ docker pause : 일시정지, docker unpause : 재시작
+ docker stop : 종료
+ docker rm : 삭제

## 실행 중인 컨테이너 로그 확인
+ docker start -i : 실행과 동시에 터미널 연결
+ docker logs 이미지명
  - 지속적으로 로그를 보고 싶으면 -f
