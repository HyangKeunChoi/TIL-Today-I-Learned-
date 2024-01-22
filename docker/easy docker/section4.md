## 이미지 빌드

+ 레이어드 파일 시스템
  - nginx를 다운받는데 pull을 여러번 받는 것을 볼 수 있다.
  - 저 레이어들이 모여서 하나의 이미지를 만든다고 보면 된다.
  - 레이어드 구조가 재사용하기 좋기 때문에 이 구조를 사용한다.
    - 레이어드 구조가 데이터 전송에도 좋음, 다른 레이어만 보내면 되기 때문에
    - 설계도를 예시로 설명
 
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/4b276bb8-c6d6-4ef3-829d-1b684006026c)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/fab24986-1a2a-4e8f-997e-aae736426a47)

## NGINX 이미지 설계 예시
+ OS 준비 -> NGINX 설치 -> NGINX 설정 -> Index.html 파일 수정

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/c16cfec7-49bd-4e94-861b-487b991098eb)

## 이미지 레이어와 컨테이너 레이어

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/dbb964e6-cae6-4f5f-ad82-36a1c0d7abbe)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/93d0007e-3f6d-49d0-8aaf-ad691cb3ff19)


## 이미지 레이어 실습
+ docker image history 이미지명
  - 이미지 레이어 구성 확인

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/4e1e0f62-c7dc-45af-b39f-e29fc1342387)

## 이미지 레이어 정리

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/9141b6be-6dc4-460b-9575-7be4f189245d)

## 이미지 커밋
+ 이미지 커밋 : 현재 컨테이너의 상태를 이미지로 저장
+ 빌드 : Dockerfile을 통해 이미지를 저장 (대부분 이방식을 이용하지만 빌드방식은 커밋 방식을 이용함)

## 이미지 커밋 순서
1. Nginx 이미지를 컨테이너로 실행
2. 컨테이너 내부 파일 변경
3. commit으로 새로운 이미지로 저장

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/d019d979-fc71-41de-9d4f-c442635d26d6)

+ docker run -it --name 컨테이너명 이미지명 bin/bash
  - 컨테이너 실행과 동시에 터미널 접속
 
+ docker commit -m 커밋명 실행중인컨테이너명 생성할이미지명
  - 실행 중인 컨테이너를 이미지로 생성

+ docker push 레지스트리 계정명/commitnginx

## 이미지 빌드
+ IaC : 인프라 상태를 코드로 관리
  - 도커에서 코드로 이미지를 빌드를 통해 관리하는 방식이 IaC방식임
 
+ Dockerfile : 이미지를 만드는 단계를 기재한 명세서

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/bbdd6db6-a3c7-48a5-b507-996aa56a0bd3)

+ docker build -t 이미지명 도커파일 경로

## 도커 파일 문법
+ FROM 이미지명 : 베이스 이미지를 지정 (시작점 역할을 하는 이미지)
+ COPY 파일경로(=변경한 파일) 복사할 경로 : 파일을 레이어에 복사
+ CMD["명령어"] : 컨테이너 실행 시 명령어 지정

## 도커파일 실행
+ 도커파일이 있는 경로로 이동
+ docker build -t 레지스트리계정명/buildnginx .

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/8fdd08c2-454e-4427-b438-1eba87e0d928)

## 빌드 컨텍스트
+ 빌드 컨텍스트란 ? 이미지를 빌드할때 사용하는 폴더

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/302c135f-8fff-40a9-b648-09c9d3a93eb3)

