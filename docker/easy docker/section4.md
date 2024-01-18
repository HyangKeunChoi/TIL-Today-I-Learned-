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
