# 수치로 증명하는 백엔드 개발자 유찬영입니다.

> "병목 현상을 찾아 해결하고, 데이터 기반의 아키텍처 최적화에서 가장 큰 성취감을 느낍니다."

단순히 기능 구현에 그치지 않고, **대규모 트래픽 환경에서의 내결함성 확보**와 **응답 속도 개선**을 고민합니다. 시스템의 문제를 논리적으로 분석하고 적합한 기술을 도입하여 성능을 극대화하는 과정을 즐깁니다.

🔍 현재 신입 백엔드 개발자로 새로운 팀을 찾고 있습니다. 측정하고, 그 측정이 맞는지까지 다시 확인하는 것이 강점입니다. 부하 테스트 결과를 로그와 재측정으로 검증해 VUSER 5,000에서 에러율 0%·성공 요청 기준 초당 약 2,000건 처리를 확인했고, 배칭과 캐싱으로 외부 AI API 호출을 98.5% 줄였습니다.

- 📧 **Email:** dev.chanyoung@gmail.com

<br>

## 🛠 Tech Stack
- **Backend:** Java, Spring Boot
- **Database:** PostgreSQL, MySQL, Oracle, Redis
- **Architecture & Infra:** Docker, GitHub Actions, RabbitMQ
- **최근 사용 경험:** TypeScript(Next.js), Python — 채용공고 자동화 파이프라인(job-fit-matcher) 구축 과정에서 사용

<br>

## 🔥 Highlight Projects

### 1. SafeCar 🚗
**대규모 모빌리티 센서 데이터 수집 및 실시간 모니터링 시스템**
> 차량에서 1초 단위로 유입되는 대규모 센서 데이터를 비동기로 수집·처리하는 파이프라인 구축
- **기간:** 2026.02 ~ 2026.03
- **규모:** 개인 프로젝트
- **기술:** Java 17, Spring Boot 3, PostgreSQL, Redis, RabbitMQ, Docker
- **Repository:** [SafeCar GitHub Repository](https://github.com/dev-chanyoung/SensorDetectionSystem) 👈 (상세한 아키텍처 및 트러블슈팅 과정 포함)
- **My Role:** 백엔드 아키텍처 설계 및 개발
- **주요 성과:**
  - **RabbitMQ 기반 비동기 파이프라인** — 이상 탐지·Redis 갱신을 Producer-Consumer 구조로 분리. VUSER 5,000(50,000건) 부하(JMeter CLI 재측정)에서 에러율 0%, 성공 요청 기준 초당 약 2,000건 처리, 성공 응답 수와 DB 저장 행 수 일치 확인
  - **중간 집계(Rolling Aggregation) 배치 파이프라인** — 1시간 단위로 미리 요약해 적재해, 자정 일괄 정산의 부담을 나누도록 설계
  - **벌크 인서트** — IDENTITY 전략에서 JPA 배치 insert가 안 되는 문제를 `JdbcTemplate.batchUpdate` 1,000건 단위 처리로 해결해 쿼리 전송 횟수 감소

<br>

### 2. Clean Eye 👁️
**AI 기반 실시간 텍스트/이미지 유해성 필터링 시스템 (Chrome Extension)**
> 대량의 텍스트를 외부 AI API로 분석하면서도, 배칭·캐싱으로 응답 지연과 호출량을 줄인 텍스트 분석 서버 구축
- **기간:** 2025.03 ~ 2025.06
- **규모:** 4인 팀프로젝트
- **기술:** Java 17, Spring Boot 3, PostgreSQL, Caffeine Cache, Gemini API, AWS
- **Repository:** [Clean Eye GitHub Repository](https://github.com/dev-chanyoung/CleanEye-Backend-Text-Analysis) 👈 (성능 개선 및 아키텍처 상세 과정 포함)
- **🎥 시연 영상:** [Clean Eye 동작 영상 보기](https://youtu.be/Xt6dk59f7CY?si=fuph3n8BtF4rQEa9)
- **My Role:** 텍스트 분석 서버 아키텍처 설계 및 전체 성능 고도화 전담
- **주요 성과:**
  - **4단계 계층형 아키텍처** — 배칭·비동기 병렬 처리·Caffeine 캐시·DB 아카이빙을 결합 (캐시 적중 시 응답 131ms)
  - **배칭 + 비동기 병렬 처리** — 400개 요청을 50개 단위로 묶어 `CompletableFuture`로 병렬 호출 (13.9s → 1.4s 1차 개선)
  - **DB 등록소 + Caffeine 캐시로 API 비용 98.5% 절감** — DB를 1차 등록소로, 캐시를 중복 Gemini 호출 방지용으로 두어 429 에러 해결 및 자가 학습형 아카이빙 구조 구축

<br>

### 3. job-fit-matcher 🎯
**채용공고 자동 발견 & 지원적합도 평가 파이프라인** *(진행 중)*
> 채용 사이트를 매일 자동으로 훑어 신규 공고를 발견하고, 규칙 기반 필터와 근거 기반 정성평가를 결합해 지원적합도를 판정하는 개인용 자동화 시스템
- **기간:** 2026.09 ~ (진행 중)
- **규모:** 개인 프로젝트
- **기술:** TypeScript(Vercel Serverless/Cron), Python, MongoDB, Notion API
- **Repository:** [job-fit-matcher GitHub Repository](https://github.com/dev-chanyoung/job-fit-matcher)
- **My Role:** 전체 아키텍처 설계 및 개발
- **주요 성과:**
  - **결정론적 하드필터와 LLM 평가를 분리해 비용 최소화**
    - 경력 연차·마감일처럼 코드로 명확히 판단 가능한 조건은 규칙 기반으로 먼저 걸러내고, 탈락 공고는 LLM 호출 자체가 발생하지 않도록 파이프라인 분리
  - **자유 서술형 채점을 고정 배점 테이블로 전환**
    - 같은 근거에도 회차마다 다른 점수를 고를 수 있던 채점 방식을 5단계 고정값 기반 가중평균으로 바꾸고, 항목별 계산 근거를 남겨 점수를 되짚어 검토할 수 있게 함
  - **여러 채용 사이트·트래커 간 중복 공고 자동 제거**
    - 회사명 정규화 비교로 소스 간 중복을 걸러내되, 계열사별 개별 채용은 구분해 놓치지 않도록 설계
  - **점수 산정 기준을 4차례에 걸쳐 개선**
    - 외부 검토에서 지적된 문제를 코드로 재현해 확인한 버그 7건(점수 범위 검증, 하드필터 오탈락 등)을 수정
  - **mock 기반 테스트 147개로 전체 파이프라인 회귀 검증**
    - 실제 API 키 없이도 하드필터·평가·Notion 저장 전 구간을 안전하게 검증

<br>

