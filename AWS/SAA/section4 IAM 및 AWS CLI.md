### IAM 정책

+ IAM 정책 구조
  - 버전
  - 아이디 : identifier
  - statement
    -   sid : identifier
    -   effect : 접근 허용 여부
    -   principal : 특정 정책이 적용될 사용자, 계정 혹은 역할
    -   action : 거부될 API 호출들의 목록
    -   resource : 적용될 action의 항목들
   
### IAM 정책 실습
+ 정책을 새로 생성하거나 기존의 정책을 이용하는 방법
+ 인라인 정책을 추가해 권한을 주는 방법

## MFA
+ Google Authenticator
+ Authy
+ YubiKey
+ Hardward Key Fob MFA Device
+ AWS GovCloud

+ AWS access key
  - console
  - cli
  - sdk : 코딩을 통해 어플리케이션에 심어 놓는다
 
## AWS Cloud Shell

## IAM Role
+ IAM 보안 도구

## 퀴즈
1. 다음 중 IAM 역할의 올바른 정의는 무엇일까요? > AWS 서비스에 요청을 생성하기 위한 일련의 권한을 정의하고, AWS 서비스에 의해 사용될 IAM 개체
2. 다음 중 IAM 보안 도구에 해당되는 것은 무엇인가요? > IAM 자격 증명 보고서
3. IAM 사용자에 대해 잘못 서술된 내용을 고르세요. > IAM 사용자들은 루트 계정 자격 증명을 통해 AWS 서비스에 액세스합니다. (자신만의 자격 증명을 통해)
4. 다음 중 IAM 모범 사례에 해당하는 것은 무엇인가요? > 루트계정 사용하지 않기
5. IAM 정책은 무엇인가요? > AWS 서비스에 요청을 생성하기 위한 일련의 권한을 정의하며, IAM 사용자, 사용자 그룹 및 IAM 역할에서 사용하게 될 JSON 문서
6. (참/거짓) IAM 사용자 그룹은 IAM 사용자 및 기타 사용자 그룹을 포함할 수 있습니다. > 거짓
7. IAM 정책은 하나 이상의 문장으로 구성됩니다. 다음 중 IAM 정책 내 문장의 구성 요소가 아닌 것을 고르세요. > 버전







