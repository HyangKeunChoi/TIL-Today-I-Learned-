# Service Discovery

+ dependency : spring cloud discovery > eureka server
+ @EnableEurekaServer
+ register-with-eureka : false
+ fetch-registry: false

## 클라이언트 서버 
+ dependency : spring cloud discovery > eureka discovery client
+ @EnableDiscoveryClient, @EnableEurekaClient 둘중 하나 사용
+ eureka.clinet.fetch-registry=true : eureka 서버로 부터 인스터스들의 정보를 주기적으로 가져올 건인지 설정, true로 설정하면 갱신된 정보를 받겠다는 설정

## 매번 인스턴스 새로 구축할때마다 포트번호 지정해 줘야하는 번거로움
+ server.port : 0 으로 설정시 랜덤 포트 지정
