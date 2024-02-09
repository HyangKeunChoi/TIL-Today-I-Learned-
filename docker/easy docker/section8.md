## Topic1 레이어 관리
### 이미지 크게 작게 만드는 방법

+ Dockerfile에 작성된 지시어 하나 당 레이어가 한 개 추가됩니다.
+ 불필요한 레이어가 많이지면 이미지의 크기가 늘어나고 빌드 속도가 느려질 수 있습니다.

1. RUN 지시어는 &&을 활용해 최대한 하나로 처리합니다.
  -> 불필요한 명령을 추가해서 레이어의 개수를 늘리지 않습니다.
2. 애플리케이션의 크기를 가능한 작게 관리합니다.
3. 베이스 이미지는 가능한 작은 이미지를 사용합니다. alpine OS를 사용하는 것이 좋습니다.
4. .dockerignore 파일을 사용해서 불필요한 파일을 제거합니다.
 -> copy 지시어는 그대로 사용하면서 .dockerignore파일로 빌드 컨텍스트에 전달하지 않는 방법 이용


## Topic2 캐싱을 활용한 빌드
+ Dockerfile에 작성된 순서대로 결과 이미지의 레이어가 쌓입니다.
+ Docker는 각 단계의 결과 레이어를 캐시처리합니다. 지시어가 변경되지 않으면 다음 빌드에서 레이어를 재사용합니다.
+ COPY,ADD 명령의 경우 빌드 컨텍스트의 파일 내용이 변경되어도 캐시를 사용하지 않습니다.
+ 레이어가 변경되면 그 레이어와 이후의 모든 레이어는 캐시를 사용하지 않고 새로운 레이어가 만들어 집니다.

+ ![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/ba0710b5-3296-44b7-b4f9-f6223350b2d2)

+ ![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/5c661af0-8e38-47ac-9769-e5392a5e8743)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/3f974ef2-4a0f-4064-aed4-359570f7d158)

+ 잘 변경되지 않는 파일들을 아래 레이어에 배치하면, 캐시를 활용하는 빈도를 높힐 수 있습니다.
+ package.json, package-lock.json 파일은 소스 코드가 의존하는 외부 라이브러리 정보가 있습니다. 개발 시 자주 변경 되지 않습니다.
+ package.json, package-lock.josn 파일이 변경되지 않을 경우 npm ci단계(의존 라이브러리 설치)까지 캐시를 활용할 수 있습니다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/d7e55ac3-db08-4e5c-98a0-c190d32a3d74)

## TOPIC 3 Tier 아키텍처 구성
+ 3 Tier : 프론트, 백엔드, db 서버가 유기적으로 구성되어 관리되는 어플리케이션 아키텍쳐
+ 백엔드 애플리케이션이 외부에 노출되어 있을 경우 개발자가 의도하지 않은 API를 호출할 위험이 있습니다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/a8494110-e937-4763-82ea-ee77008b4fe3)

+ Nginx의 프록시 기술을 활용해 보안에 뛰어난 3Tier 아키텍처를 구성할 수 있습니다.
+ Nginx는 특정 경로로 온 요청(/api로 시작하는 경로)를 지정한 서버로 전달합니다.
+ Nginx를 프록시 서버로 활용하여 보안 향상, 부하 관리 및 API 응답을 캐싱을 활용할 수 있습니다.

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/c749a159-b278-4b27-ae4a-8ea31ad9d392)

## 이중화 DB 구성

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/cc604de8-5c91-457f-8f26-0862b02421a3)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/4d1d5d71-c9de-4107-a8bd-ad4542d4c832)

## TOPIC 6 컨테이너 애플리케이션 최적화

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/37fc08f9-7191-4818-82fc-f8bba6ff1981)

### 도커 사용량 조회 명령어
+ docker stats (컨테이너명/ ID)
+ docker events : HOST OS에서 발생하는 이벤트 로그 조회

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/804450e1-1750-4a46-8a22-9e24808f60e9)

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/5131bf0c-a86c-475d-a508-f110f52a5f2e)

### 자바 JVM 튜닝

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/3bc5977f-ce33-48a0-972c-f5bdc431a051)

## JVM 자동으로 힙메모리 설정

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/dd44de1d-ed1e-42b1-8a77-4c68e6a2a456)

## TOPIC 7 컨테이너 내부에서 개발하기

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/6663fd66-33e3-4d45-846a-c3483b07b255)

## java, intellij 컨테이너 활용 및 원격 디버깅
