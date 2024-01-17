## 이미지 레지스트리

+ 대표적인 이미지 레지스트리 : 도커허브

## 이미지 레지스트리 기능
+ 이미지 공유
+ 이미지 검색
+ 이미지 버전 관리
+ 이미지 보안
+ DevOps 파이프라인과 연계

## 이미지가 저장되는 곳
+ 퍼블릭 레지스트리
+ 프라이빗 레지스트리
+ 호스트 머신의 로컬 스토리지

+ docker run nignx를 실행하면 로컬 스토리지를 찾고 여기에 없으면 퍼블릭에서 다운 받아서 사용

## 이미지 네이밍 규칙
+ 레지스트리주소/프로젝트명/이미지명(:이미지태그)
  - docker.io/myProject/myNginx:2.1.0-alpine
  - docker.io/library/nginx:latest

 ## 도커 허브
+ hub.docker.com

## 도커 레지스트리 실습
+ docker pull 이미지 명 : 로컬 스토리지로 이미지 다운로드
+ docker tage 기존이미지명 추가할 이미지명 : 로컬 스토리지의 이미지명 추가
+ docker push 이미지명 : 이미지 레지스트리에 이미지 업로드

## 실습 

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/feaeae24-55c2-4183-8972-d3d33b8c698a)

+ docker pull devwikirepo/simple-web:1.0
+ docker tag devwikirepo/simple-web:1.0 easydocker12345/my-simple-web:0.1
+ docker image ls
+ docker push easydocker12345/my-simple-web:
  - denied 뜨면 로그인 해야한다.
  - docker login : 도커 로그인
  - docker logout
  - docker image rm 이미지명
 
