## RAID

https://www.youtube.com/watch?v=lP3MlI9aaqY

## RAID 0
+ 속도 위주
+ 두개의 디스크가 있을때 각각의 디스크에 나눠 담는 방식

<img width="588" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/ff488a04-4dbc-4c1f-a7ff-c0bfa4b9f341">

+ 일회성 데이터 저장에 사용되고 사용 후 백업 하는것이 좋다.

## RAID 1
+ 안정성 위주
+ 각각 두개의 디스크에 중복으로 저장
+ 하나가 고장나더라도 데이터가 안정
+ 하드디스크의 용량을 절반밖에 못씀

## RAID 5
+ 3개 이상의 하드디스크 요구
+ 속도,안정성, 용량을 모두 챙기는 방식
+ 데이터를 분할로 저장
+ 패리티라는 복원정보를 같이 저장한다.
  - 하나의 하드디스크 오류만 복원이 가능하므로, 고장나면 하드디스크 복원이 우선시 되어야함

<img width="567" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/894b617a-8358-43fc-95d3-a5b83ad4b161">

<img width="552" alt="image" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/f19fdaee-4c3b-4596-b845-60b8776187fa">
