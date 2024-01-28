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

## 도커파일 지시어
+ Node.js 애플리케이션을 구성하는 과정에 대한 이미지

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/51123ccf-cec2-40f0-a6c7-aa73aece4afb)

+ 이미지 빌드 vs 애플리케이션 빌드
+ 애플리케이션 빌드 : 소스코드를 실행 가능한 프로그램으로 빌드를 말함
+ 도커 이미지를 빌드할때 애플리케이션 빌드를 포함해야 한다.

### 도커파일 지시어

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/6824cdeb-bd95-4169-b989-a3ec9c84f910)

+ docker build -f 도커파일명 -t 이미지명 Dockerfile 경로
+ -f 옵션 : 도커파일명이 Dockerfile이 아닌 경우 별도 지정

### 시스템과 관련된 지시어

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/745edeba-052f-4437-ab58-6d63ab8b557c)

+ WORKDIR : 이 경로에서 부터 모든 명령어를 실행 (보통 FROM다음에 바로 작성)
+ EXPOSE : 사용할 포트 명시

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/9362bdb1-80fc-40e4-928c-d9aac4d14adc)

### 환경 변수와 관련된 지시어

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/f9c2b961-e501-4c13-91e8-0f2b1fccea5e)

### 프로세스 실행과 관련된 지시어
+ entrypoint : 중복된 명령어를 지정하는 명령어
  - 예를들어 npm start, npm install에서 npm이 중복됨

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/8fb2df8d-d3a6-48b7-b612-14cae30c75e1)

## 멀티 스테이지 빌드(Multi-Stage Build)
+ 멀티 스테이지 빌드 : 두개의 base image를 이용하는 방법
  - 이미지를 빌드에 사용하는 이미지, 실행에 사용하는 이미지로 분리
  - 보통 실행하는데 사용하는 이미지의 크기가 생각보다 크기 때문에

+ 백엔드 spring boot application 이미지 구성하기
![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/cebc3dcd-7214-450e-9e6c-127cb8e3bae8)

### Singlestage 방법

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/8ccec53d-23c6-4c1f-9bce-0594686eecf2)

+ 메이븐같은 경우의 도구도 빌드에만 쓰이고 실제 애플리케이션을 실행하는 것과는 무관

### MultiStage 방법

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/d6912c14-bd24-48e7-904f-36187cb4a072)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/4233a97d-882e-4c63-badc-91c4a507cf06)

+ FROM AS build 부분이 COPT --from=build의 이름으로 지정된 것으로 보면 된다.

