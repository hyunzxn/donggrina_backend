# 동그리나

## 1. 소개
반려동물의 다양한 정보(병원 방문 기록, 미용 등)를 가족/친구/연인과 함께 기록하고 자신의 반려동물의 사진을 공유할 수 있는 게시판 유형의 서비스

## 2. 백엔드 역할 구분
- 문현준: 일정, 성장기록, 마이페이지(가족 관리), 이미지 업로드 및 삭제(스케줄링), 좋아요, 댓글(대댓글), AWS 환경 구성 + CI/CD 구성
- 권민우: OAuth2 인증(카카오, 구글), 마이페이지(반려동물 관리), 다이어리, 스토리

## 3. 담당한 주요 기능 소개
- ThreadPoolTaskExecutor 활용한 S3 작업 비동기 처리하여 메인 스레드 블로킹을 방지하고 동시성을 고려함으로써 애플리케이션 성능 최적화 시도
https://github.com/hyunzxn/donggrina_backend/blob/ccadf71b70da6329e173e1a381e097d7a8f0eb16/src/main/java/com/codeit/donggrina/common/config/AsyncConfig.java#L9-L22
https://github.com/hyunzxn/donggrina_backend/blob/ccadf71b70da6329e173e1a381e097d7a8f0eb16/src/main/java/com/codeit/donggrina/domain/ProfileImage/util/S3Handler.java#L28-L50

- 프로필 이미지를 업로드 하는 기능을 구현할 때 CompletableFuture를 활용하여 S3 이미지 업로드와 DB 저장을 비동기 병렬 처리하여 응답성과 처리량 최적화 시도
https://github.com/hyunzxn/donggrina_backend/blob/ccadf71b70da6329e173e1a381e097d7a8f0eb16/src/main/java/com/codeit/donggrina/domain/ProfileImage/service/ProfileImageService.java#L23-L40

## 3. 사용 기술
- **Backend**
  - Java 17
  - Spring Boot 3.3.0
  - Spring Data JPA
  - Spring Security
  - Spring Validation
  - OAuth2
  - Querydsl
- **Database**
  - MySQL
  - Redis
- **Infra**
  - AWS
    - VPC
    - EC2
    - Load Balancer
    - RDS
    - S3
    - ECR
    - Route53
  - Docker
  - Github Actions

## 4. 클라우드 아키텍처
<img width="1282" alt="백엔드 아키텍처" src="https://github.com/Donggrina/Backend/assets/100478841/71639a78-187c-45ab-bb7d-26e3850d84d0">
<img width="1282" alt="프론트-백엔드 통신 흐름" src="https://github.com/Donggrina/Backend/assets/100478841/cb9af131-2b2b-4747-833a-20c4d03ad2da">

## 5. ERD
<img width="1282" alt="ERD" src="https://github.com/Donggrina/Backend/assets/100478841/ff77b0f3-bcd6-48fd-9fa6-dd5cd39591a0">


