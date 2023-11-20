+ https://www.youtube.com/watch?v=kRUVjFu5twM

## Fetch Join

+ 일반적인 SQL에서 이야기하는 조인의 종류가 아닌 JPQL에서 성능 최적화를 위해 제공하는 기능
  - Fetch join을 사용하면 연관된 엔티티나 컬렉션을 한 번에 같이 조회할 수 있다.
 
## 엔티티 Fetch Join

<img width="700" height="550" alt="스크린샷 2023-11-20 오후 6 25 22" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/5ba3a0b7-879c-4931-bd90-68f54dd0c16b">

+ ```join fetch를 이용```
+ 다대일 관계는 결과가 뻥튀기가 되지 않음

## 컬렉션 Fetch Join

<img width="966" alt="스크린샷 2023-11-20 오후 6 25 53" src="https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/8784d7de-fc1e-4996-ac0e-69ec30ed59af">

+ 일대다 관계에서의 fetch join은 결과가 뻥튀기가 됨
  - JPQL의 distinct 명령어는 SQL에 Distinct는 물론이고 애플리케이션에서 한번 더 중복을 제거

![image](https://github.com/HyangKeunChoi/TIL-Today-I-Learned-/assets/49984996/1a2c11e6-f44f-4d94-b924-34c74d6b0893)

  ## 한계
  + 페치 조인 대상에는 별칭을 줄 수 없다.
  + 따라서 Select, Where절, 서브 쿼리에 페치 조인 대상을 사용할 수 없다.
  + 둘 이상의 컬렉션을 페치할 수 없다.
  + 컬렉션을 페치 조인하면 페이징 API를 사용할 수 없다.
