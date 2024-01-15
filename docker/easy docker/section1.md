## 엔터프라이즈 서버 운영
1. 베어메탈
2. 하이퍼바이저
3. 컨테이너 - 도커

## 가상화 기술
+ 하나의 컴퓨터에서 여러개의 컴퓨터를 실행하는 기술
+ 물리적인 컴퓨터환경에서 논리적인 컴퓨터환경
+ 높은 성능의 컴퓨터 한대쓰는게 더 이득 ( 낮은 성능의 컴퓨터 여러대 쓰는것 보다)
+ 하이퍼바이저, 컨테이너 방식이 가상화 기술

## 하이퍼 바이저
+ 호스트 OS 위에 게스트 OS 여러개 설치

## 동작 원리
+ 하이퍼 바이저가 게스트 OS와 호스트 OS의 중간 다리(마치 통역)역할을 한다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/2d51bdb2-c9a6-4451-b8fa-74503611570e)

## 컨테이너 가상화 (도커)
+ 하이퍼 바이저 가상화보다 선호됨
  - 이유 1 : 가볍다
  - 이유 2 : 빠르다
 
+ LXC 기술을 이용
+ 컨테이너 가상화는 하이퍼바이저가 필요없이 커널 자체의 기술로 가상화
+ 모든 컨테이너가 하나의 커널을 공유

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/9e1b8038-93a7-417c-a5c6-ac50350a577b)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/a04629c9-8003-4d2a-a7b5-1fb52950aa95)

+ 적은 오버헤드, 빠른 부팅 (하이퍼바이저 가상화 보다)

## 도커

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/11171acb-2924-423d-898f-b1aedb0f9edf)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/f0f0ab30-6368-4af6-9079-d3d8226d7ee7)

+ docker version
+ docker info
+ docker --help

## 도커 명령어 형태
+ docker (management command - 생략 가능) command 형태이다.
  - docker container run
  - docker run 과 같다.
 
+ docker run  이미지명 : 컨테이너 실행
+ docker rm 컨테이명/ID : 컨테이너 삭제
+ docker run -p 80:80 --name hellonginx nginx
