# 수치로 증명하는 백엔드 개발자 유찬영입니다.

> "병목 현상을 찾아 해결하고, 데이터 기반의 아키텍처 최적화에서 가장 큰 성취감을 느낍니다."

단순히 기능 구현에 그치지 않고, **대규모 트래픽 환경에서의 내결함성 확보**와 **응답 속도 개선**을 고민합니다. 시스템의 문제를 논리적으로 분석하고 적합한 기술을 도입하여 성능을 극대화하는 과정을 즐깁니다.

- 📧 **Email:** dev.chanyoung@gmail.com

<br>

## 🛠 Tech Stack
- **Backend:** Java, Spring Boot
- **Database:** PostgreSQL, MySQL, Redis
- **Architecture & Infra:** Docker, GitHub Actions, RabbitMQ

<br>

## 🔥 Highlight Projects

### 1. SafeCar 🚗
**대규모 모빌리티 센서 데이터 수집 및 실시간 모니터링 시스템**
> 차량에서 1초 단위로 유입되는 대규모 데이터를 유실 없이 처리하는 파이프라인 구축
- **기간:** 2026.02 ~ 2026.03
- **규모:** 개인 프로젝트
- **기술:** Java 17, Spring Boot 3, PostgreSQL, Redis, RabbitMQ
- **Repository:** [SafeCar GitHub Repository](https://github.com/dev-chanyoung/SensorDetectionSystem) 👈 (상세한 아키텍처 및 트러블슈팅 과정 포함)
- **My Role:** 백엔드 아키텍처 설계 및 개발
- **주요 성과:**
  - **비동기 메시지 큐(RabbitMQ) 도입으로 시스템 장애 완벽 해결**
    - VUSER 5,000명 부하 테스트 시 동기 처리로 인해 발생하던 스레드 대기열 폭주 및 DB 커넥션 고갈 문제 발견
    - RabbitMQ를 활용한 Producer-Consumer 구조로 분리하고 커넥션 풀을 튜닝하여 **에러율 52.1% → 0% 개선** 및 Fail-Fast 아키텍처 구축
  - **중간 집계(Rolling Aggregation) 배치 파이프라인 구축**
    - 수천 건의 데이터를 자정에 한 번에 정산할 때 발생하는 RDBMS Lock 현상 방지
    - Spring Scheduler를 활용해 1시간 단위 사전 요약 적재를 구현하여 최종 배치 처리 속도 최적화
  - **벌크 인서트(Bulk Insert) 최적화**
    - `JdbcTemplate.batchUpdate`를 도입해 1,000건 단위로 묶어 처리함으로써 단건 쿼리 반복에 따른 네트워크 I/O 병목 제거

<br>

### 2. Clean Eye 👁️
**AI 기반 실시간 텍스트/이미지 유해성 필터링 시스템 (Chrome Extension)**
> 대량의 텍스트를 실시간으로 분석하여 0.1초대에 필터링하는 고성능 AI 엔진 서버 구축
- **기간:** 2025.03 ~ 2025.06
- **규모:** 4인 팀프로젝트
- **기술:** Java 17, Spring Boot 3, PostgreSQL, Caffeine Cache, Gemini API
- **Repository:** [Clean Eye GitHub Repository](https://github.com/dev-chanyoung/CleanEye-Backend-Text-Analysis) 👈 (131ms 성능 개선 및 아키텍처 상세 과정 포함)
- **My Role:** 텍스트 분석 서버 아키텍처 설계 및 전체 성능 고도화 전담
- **주요 성과:**
  - **4단계 계층형 아키텍처 설계로 응답 속도 100배 단축**
    - 대량 텍스트 분석 시 발생하던 13.9초의 응답 지연을 배칭, 비동기, 캐싱을 결합하여 **최저 131ms로 단축**
  - **배칭(Batching) 및 비동기 병렬 처리 도입**
    - 400개의 개별 요청을 50개 단위 Chunk로 통합하고 `CompletableFuture`로 병렬 처리하여 통신 오버헤드 최소화 (초기 응답속도 13.9s → 1.4s 1차 개선)
  - **로컬 캐싱 및 데이터 아카이빙으로 API 비용 98.5% 절감**
    - Caffeine Cache를 1차 방어선으로 구축하여 429(Too Many Requests) 에러 완벽 해결
    - AI 분석 결과를 실시간 DB에 영속화하는 자가 학습 구조를 설계하여 외부 API 의존도를 대폭 축소

<br>

