# 수치로 증명하는 백엔드 개발자 유찬영입니다.

> "병목 현상을 찾아 해결하고, 데이터 기반의 아키텍처 최적화에서 가장 큰 성취감을 느낍니다."

단순히 기능 구현에 그치지 않고, **대규모 트래픽 환경에서의 내결함성 확보**와 **응답 속도 개선**을 고민합니다. 시스템의 문제를 논리적으로 분석하고 적합한 기술을 도입하여 성능을 극대화하는 과정을 즐깁니다.

- 📧 **Email:** dev.chanyoung@gmail.com

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

<br>

## 🛠 Tech Stack
- **Backend:** Java, Spring Boot
- **Database:** PostgreSQL, MySQL, Redis
- **Architecture & Infra:** Docker, GitHub Actions, RabbitMQ
- **최근 사용 경험:** TypeScript(Next.js), Python — 채용공고 자동화 파이프라인(job-fit-matcher) 구축 과정에서 사용

<br>

<p align="center">
  <img height="165em" src="https://github-readme-stats.vercel.app/api?username=dev-chanyoung&show_icons=true&theme=default&hide_border=true&count_private=true" />
  <img height="165em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=dev-chanyoung&layout=compact&hide_border=true&langs_count=8" />
</p>

<br>

## 🔥 Highlight Projects

### 1. SafeCar 🚗
**대규모 모빌리티 센서 데이터 수집 및 실시간 모니터링 시스템**
> 차량에서 1초 단위로 유입되는 대규모 데이터를 유실 없이 처리하는 파이프라인 구축
- **기간:** 2026.02 ~ 2026.03
- **규모:** 개인 프로젝트
- **기술:** Java 17, Spring Boot 3, PostgreSQL, Redis, RabbitMQ, Docker
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
- **기술:** Java 17, Spring Boot 3, PostgreSQL, Caffeine Cache, Gemini API, AWS
- **Repository:** [Clean Eye GitHub Repository](https://github.com/dev-chanyoung/CleanEye-Backend-Text-Analysis) 👈 (131ms 성능 개선 및 아키텍처 상세 과정 포함)
- **My Role:** 텍스트 분석 서버 아키텍처 설계 및 전체 성능 고도화 전담
- **주요 성과:**
  - **4단계 계층형 아키텍처 설계로 응답 속도 100배 단축**
    - 대량 텍스트 분석 시 발생하던 13.9초의 응답 지연을 배칭, 비동기, 캐싱을 결합하여 **최저 131ms로 단축**
  - **배칭(Batching) 및 비동기 병렬 처리 도입**
    - 400개의 개별 요청을 50개 단위 Chunk로 통합하고 `CompletableFuture`로 병렬 처리하여 통신 오버헤드 최소화 (초기 응답속도 13.9s → 1.4s 1차 개선)
  - **로컬 캐싱 및 데이터 아카이빙으로 API 비용 98.5% 절감**
    - DB를 1차 등록소로, Caffeine Cache를 그 다음 계층(중복 Gemini 호출 방지)으로 구성해 429(Too Many Requests) 에러 완벽 해결
    - AI 분석 결과를 실시간 DB에 영속화하는 자가 학습 구조를 설계하여 외부 API 의존도를 대폭 축소

<br>

### 3. job-fit-matcher 🎯
**채용공고 자동 발견 & 지원적합도 평가 파이프라인** *(진행 중 · 비공개 저장소)*
> 채용 사이트를 매일 자동으로 훑어 신규 공고를 발견하고, 규칙 기반 필터와 근거 기반 정성평가를 결합해 지원적합도를 판정하는 개인용 자동화 시스템
- **기간:** 2026.09 ~ (진행 중)
- **규모:** 개인 프로젝트
- **기술:** TypeScript(Vercel Serverless/Cron), Python, MongoDB, Notion API
- **My Role:** 전체 아키텍처 설계 및 개발
- **주요 성과:**
  - **결정론적 하드필터와 LLM 평가를 분리해 비용 최소화**
    - 경력 연차·마감일처럼 코드로 명확히 판단 가능한 조건은 규칙 기반으로 먼저 걸러내고, 탈락 공고는 LLM 호출 자체가 발생하지 않도록 파이프라인 분리
  - **자유 서술형 채점을 고정 배점 테이블로 전환해 재현성 확보**
    - 같은 근거를 봐도 회차마다 점수가 달라지던 문제를, 5단계 고정값 기반 가중평균 방식으로 바꿔 해결
  - **여러 채용 사이트·트래커 간 중복 공고 자동 제거**
    - 회사명 정규화 비교로 소스 간 중복을 걸러내되, 계열사별 개별 채용은 구분해 놓치지 않도록 설계
  - **점수 산정 기준을 4차례에 걸쳐 개선하며 재현성 문제를 실측 검증**
    - 같은 근거에도 회차마다 다른 점수가 나오는 문제를 코드로 재현해 실제 버그 7건 이상을 발견·수정
  - **mock 기반 테스트 147개로 전체 파이프라인 회귀 검증**
    - 실제 API 키 없이도 하드필터·평가·Notion 저장 전 구간을 안전하게 검증

<br>

