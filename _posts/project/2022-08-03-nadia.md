# 프로젝트(개발 환경) 기본 구조

```
nadia-backend-develop> tree /f
│  .gitattributes
│  .gitignore
│  gradlew
│  gradlew.bat
│  README.MD
│  settings.gradle
│
├─app
│  │  build.gradle
│  │
│  └─src
│      └─main
│          ├─java
│          │  └─com
│          │      └─itnomads
│          │          └─nadia
│          │              └─api
│          │                  │  NadiaApiApplication.java
│          │                  │
│          │                  ├─application
│          │                  │  │  AdminService.java
│          │                  │  │  BusinessService.java
│          │                  │  │  FaqService.java
│          │                  │  │  LoginService.java
│          │                  │  │
│          │                  │  ├─impl
│          │                  │  │      AdminServiceImpl.java
│          │                  │  │      MemberServiceImpl.java
│          │                  │  │
│          │                  │  └─member
│          │                  │          MemberService.java
│          │                  │
│          │                  ├─domain
│          │                  │  ├─model
│          │                  │  │  ├─admin
│          │                  │  │  │      Admin.java
│          │                  │  │  │      AdminCreateDTO.java
│          │                  │  │  │      AdminDTO.java
│          │                  │  │  │      AdminMapper.java
│          │                  │  │  │      AdminPasswordUpdateDTO.java
│          │                  │  │  │      AdminRepository.java
│          │                  │  │  │      AdminSpec.java
│          │                  │  │  │      AdminUpdateDTO.java
│          │                  │  │  │
│          │                  │  │  ├─business
│          │                  │  │  │      Business.java
│          │                  │  │  │      BusinessRepository.java
│          │                  │  │  │      Execution.java
│          │                  │  │  │
│          │                  │  │  ├─donation
│          │                  │  │  │      Donation.java
│          │                  │  │  │      DonationRepository.java
│          │                  │  │  │
│          │                  │  │  ├─faq
│          │                  │  │  │      Faq.java
│          │                  │  │  │      FaqRepository.java
│          │                  │  │  │
│          │                  │  │  ├─fund
│          │                  │  │  │      Fund.java
│          │                  │  │  │      FundRepository.java
│          │                  │  │  │
│          │                  │  │  ├─payment
│          │                  │  │  │      Payment.java
│          │                  │  │  │      PaymentRepository.java
│          │                  │  │  │
│          │                  │  │  ├─user
│          │                  │  │  │      EnterpriseUser.java
│          │                  │  │  │      EnterpriseUserRepository.java
│          │                  │  │  │      PersonalUser.java
│          │                  │  │  │      PersonalUserRepository.java
│          │                  │  │  │      User.java
│          │                  │  │  │      UserRepository.java
│          │                  │  │  │
│          │                  │  │  └─vote
│          │                  │  │          Vote.java
│          │                  │  │          VoteRepository.java
│          │                  │  │          Voting.java
│          │                  │  │
│          │                  │  └─shared
│          │                  │          BaseRepository.java
│          │                  │          PageSpec.java
│          │                  │
│          │                  ├─infrastructure
│          │                  │  ├─jpa
│          │                  │  │  ├─config
│          │                  │  │  │      JpaConfig.java
│          │                  │  │  │
│          │                  │  │  └─repository
│          │                  │  │          JpaAdminRepository.java
│          │                  │  │          JpaBaseRepository.java
│          │                  │  │          JpaBusinessRepository.java
│          │                  │  │          JpaDonationRepository.java
│          │                  │  │          JpaFaqRepository.java
│          │                  │  │          JpaFundRepository.java
│          │                  │  │          JpaMemberRepository.java
│          │                  │  │          JpaPaymentRepository.java
│          │                  │  │          JpaVoteRepository.java
│          │                  │  │
│          │                  │  ├─mvc
│          │                  │  │      WebConfig.java
│          │                  │  │
│          │                  │  └─sqlite
│          │                  │          SqliteDialect.java
│          │                  │
│          │                  └─interfaces
│          │                      └─controller
│          │                              AdminController.java
│          │                              BusinessController.java
│          │
│          └─resources
│                  application.yml
│
├─gradle
│  └─wrapper
│          gradle-wrapper.jar
│          gradle-wrapper.properties
│
└─sql
    └─ddl
            init.sql
```

- admin 패키지가 기본 샘플 형태로 만들어진 상황
- 선행 학습 필요
    - DDD (Domain Driven Development)
    - spring-boot
    - spring-mvc
    - jpa
    - querydsl
    - +gradle?

- API 확인: http://localhost:8080/swagger-ui/ 

- gradle