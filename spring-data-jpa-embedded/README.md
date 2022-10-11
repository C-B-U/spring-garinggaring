## Spring Data JPA 사용법 (일반 JPA 와 차이점도)

[[Spring Data Jpa] JPA..그래 알겠어.. 그래서 스프링 데이터 JPA는 어떻게 쓰는데..](https://c11.kr/16dls)

## N+1 문제 및 해결법

[JPA 모든 N+1 발생 케이스과 해결책](https://url.kr/i9el7d)

## Embedded Database 설정 

[스프링부트 h2 설정](https://bgpark.tistory.com/78)

```docker
spring:
  jpa:
    hibernate:
      ddl-auto: create
    properties:
      hibernate:
    # show_sql: true
        format_sql: true
  h2:
    console:
      enabled: true
logging:
  level:
    org.hibernate.SQL: debug
    org.hibernate.type: trace
```
