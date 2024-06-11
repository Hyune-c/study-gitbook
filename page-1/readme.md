# README

### 뤼튼에서 한 일 (24.01 \~ 24.06)

```
- Kotlin + Spring Boot 3.x.x
- Spring-AI + OpenAI, Azure 
- AWS EKS, MSK, Datadog
- Gitlab, ArgoCD
```

#### 1. AI 모델 서빙 서비스 개발

| 제목                                                                                                         | 요약                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [AI 모델 서비스 서빙 개발, 운영](https://hyune-c.notion.site/AI-0f68cce75c2c4bd9b18e3b7cace4a202?pvs=4)               | <p>- Spring-AI 를 확장하여 개발<br>- 전 세계에 흩어진 27 개의 Azure PTU resource 서빙 서비스 개발<br>- 최전방 노출 서비스에 대해 무중단 교체 및 성능 향상 달성<br>    - RPM 750, API Response Time 20% 감소. 오류건 감소</p> |
| [OpenAi Tiktokenizer 서비스 개발](https://hyune-c.notion.site/Tokenizer-0aacc387412b4773a921ef3ec4f310b1?pvs=4) | <p>- Python + Fast + OpenAI Tiktokenizer 라이브러리 기반 개발<br>- 빠르게 변하는 Token Encoding 방식에 대응하기 위해 Python 으로 개발</p>                                                           |

#### 2. Core Part 업무

| 제목                                     | 요약                                                                                                                          |
| -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| <p>CDS 운영<br>(Common Data Service)</p> | <p>- 여러 서비스에서 공통으로 사용되는 기능을 지원하는 API 서버 운영<br>- 유해 키워드, 한중일 문자열 분석, 이메일 유효성 검증, 이미지 리사이즈, tiktoken 계산</p>                   |
| 전사 기술 수준 향상을 위해                        | <p>- 테크 스펙, 아키텍처, PR 리뷰<br>- 사내 기술 스터디, 테크 피드 운영</p>                                                                        |
| 기술 POC 및 템플릿 코드화하여 사내 배포               | - 모듈 구조, 테스트 코드, 부하 테스트, 모니터링                                                                                               |
| 기타                                     | - Spring-AI 오픈소스 컨트리뷰트 [PR Link](https://github.com/spring-projects/spring-ai/pulls?q=is%3Apr+is%3Aclosed+author%3AHyune-c) |

### 컬리페이에서 한 일 (22.09 \~ 23.12)

```
- Kotlin + Spring Boot 2.x.x/3.x.x
- MySQL, JPA, QueryDSL, Redis 
- AWS EKS, Aurora, MSK, S3, Datadog, Kibana
- Gitlab, ArgoCD
```

#### 1. 상품권 개발, 런칭

| 제목                                                                                                      | 요약                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [컬리페이 상품권 설계, 개발, 운영](https://hyune-c.notion.site/0dab4f6cbb364ad5b09eeae23025dc2a?pvs=4)               | <p>- 계약, 상품, 전시 개발<br>- 상품권 구매 유스케이스 개발<br>    - 외부 제휴사 B2B 구매, 컬리몰 B2C 구매, 법인카드 구매, 개인 대량 구매</p>                                                             |
| [컬리몰 상품권 구매 프로세스 개선](https://hyune-c.notion.site/2535950e7b224b44b3c940b6811f521e?pvs=4)                | <p>- 런칭 후 장애시 불일치가 발생하고, 수동 대응해야되는 as-is 로직을 설계 및 일부 구현<br>- 양사 간의 불일치를 결과적 일관성으로 설계 (kafka)<br>- 기존 로직은 go 로 구현되어 있습니다.</p>                                  |
| 카카오 알림톡 접수성공, 전달실패에 대한 처리                                                                               | <p>- 전달결과를 api polling 스케줄러로 구현 완료<br>- 전달실패에 대한 후속 처리 및 kafka 를 사용하는 개선을 일부 개발</p>                                                                           |
| [B2C, B2B 대량발송 프로세스 설계, 개선](https://hyune-c.notion.site/B2C-B2B-acf2eec8bc294195ac773c386b807dc5?pvs=4) | <p>- 고객센터에서부터 들어오는 구매 흐름 설계<br>- 발주서 설계 및 파트너사로 개발 가이드<br>- 운영 불편함을 줄이기 위해 프로세스 개선</p>                                                                        |
| [통계, 인사이트를 위한 redash 구성](https://hyune-c.notion.site/redash-7f7fa36cbcfe44c1bde64d26f4878027?pvs=4)     | <p>- 비개발자의 접근성을 고려한 솔루션 선택<br>- 더 기술적이고 확장성 있는 설계도 리서치 <a href="https://hyune-c.notion.site/6e12f39a680e4baa9598a72eb2e3acff?pvs=4">확장성 있는 데이터 통계를 위해</a></p> |
| 개발만이 아닌 프로덕트 중심의 태도                                                                                     | <p>- 상품권 판매 독려를 위한 라이브방송에서의 판매 진행<br>- 임직원 복지 포인트를 상품권으로 지급 발의<br>- 컬리앱에서의 상품권 노출 전략에 대한 협의 진행</p>                                                            |

#### 2. 겸직 업무

| 제목                    | 요약                                                            |
| --------------------- | ------------------------------------------------------------- |
| 간편결제 & 일반결제 이관 지원, 운영 | <p>- 컬리 및 파트너 개발사 업무 협의<br>- 유스케이스 흐름, API 및 QA 관리, 이관 전략</p> |
| 선불충전 & 포인트 설계, 개발운영   | <p>- 이벤트 드리븐 기반의 설계, 운영<br>- 복합결제, 우선순위 로직 등</p>              |
| PLCC 컬리카드 운영          | - BC 로부터 전달되는 적립금 시스템 운영                                      |

#### 3. 트러블 슈팅

| 제목                                                                                                                  | 요약                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [배치 작업간 OutOfMemoryError 발생](https://hyune-c.notion.site/1-OutOfMemoryError-b3b513d7f21445b79e70a58310458332?pvs=4) | <p>- 담당자가 퇴사한 상황에서 원인 분석과 단기 해결 방법을 제시<br>- 전사 메모리 최적화까지 진행 완료</p>                                                                                                      |
| [배포 후 인스턴스가 기동되지 않는 오류](https://hyune-c.notion.site/3c0bc9e292c04e3b83a038f3b169e1a0?pvs=4)                         | <p>- 간헐적으로 배포 후 인스턴스가 정상 기동되지 않는 현상 발생<br>- 확인 결과 health check 간격이 1분으로 너무 짧아 간헐적인 실패 발생<br>- 최초 기동에 관련된 startupProbe 는 늘리고, 이후 체크하는 livenessProbe 는 유지하는 것으로 개선 완료</p> |
| [상품권코드 없이 상품권 조회 api 가 호출되는 현상](https://hyune-c.notion.site/2-api-14772169bbec4e249653359d25c4900c?pvs=4)           | <p>- 실제 voc 가 들어오지 않던 부분이기에 놓치기 쉬운 부분 입니다.<br>- 평소에 작업해놓은 모니터링 설정 덕분에 선제 작업을 할 수 있었습니다.</p>                                                                             |
| [ECS 클러스터 안의 서비스간 네트워크 연결 불가](https://hyune-c.tistory.com/52)                                                       | - AWS 권한조차 없던 입사 초기 시점에 인프라 트러블 슈팅을 진행하고 해결                                                                                                                             |

### 마켓보로에서 한 일 (21.08 \~ 22.08)

```
- Java 11 + Spring Boot 2.x.x
- MySQL, Redis, JPA, Jooq, QueryDSL, GraphQL
- AWS ECS, RDS, Lambda, S3, CloudWatch, Datadog
- Bitbucket, Docker
```

| 제목                                    | 요약                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 전사 로깅 강화를 위한 datadog 도입               | <p>- cloudwatch 기반의 관제 환경을 datadog 으로 전환 <a href="https://hyune-c.tistory.com/entry/Datadog-%EC%97%90%EC%84%9C-GraphQL-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81-%EB%A7%9B%EB%B3%B4%EA%B8%B0?category=989703">Datadog 에서 GraphQL 모니터링 맛보기</a><br>- 진입점이 <code>POST /graphql</code> 로 통일되는 문제를 해결하기 위해 커스텀 방법을 연구 (span, tag)<br>- 베스핀글로벌과 비개발 영역 업무 협의 (비용, 도입방법 등), 도커라이징 및 배포 프로세스 개선</p>                                                                                                                                                                                                                                                                                                                                   |
| <p>마켓봄 프로 개발<br>(마켓보로 대표 B2B 플랫폼)</p> | <p>- 이종 플랫폼의 회원 통합 및 운영 방법에 대한 MSA 고민 <a href="https://hyune-c.tistory.com/entry/%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C-%EC%84%9C%EB%B9%84%EC%8A%A4%EB%8F%84-%EB%A6%AC%EC%86%8C%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94%EA%B0%80-%ED%95%84%EC%9A%94%ED%95%A0%EA%B9%8C?category=991435">마이크로 서비스도 리소스 동기화가 필요할까?</a><br>- 높은 트래픽에 대응할 수 있는 아키텍처 설계 <a href="https://hyune-c.tistory.com/entry/%EB%8C%80%EB%9F%89-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A1%B0%ED%9A%8C%EC%9C%A0%EC%A7%80%EB%B3%B4%EC%88%98%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%B4%EC%95%BC%EB%90%A0%EA%B9%8C?category=991435">대량 데이터 조회와 유지보수는 어떻게 해야될까?</a><br>- 카카오 알림톡을 호출하는 레거시 로직 리팩토링 <a href="https://hyune-c.tistory.com/32">느슨한 결합도의 설계를 위해!</a></p> |

### 비즈니스 개발자로서의 태도

> 비즈니스 개발자라면 순수 개발만이 아닌 문제 해결 능력이 중요하다고 생각합니다.\
> 또한 비즈니스의 문제는 혼자서는 해결할 수 없기에 협업을 위한 문제 정의와 실행 가능한 안 선택, 문서화 능력이 필수라고 생각합니다.
>
> 그리고 좋은 개발자라면 자기 개발은 당연하고, 함께 자라기에 대한 생각이 있어야 된다고 생각합니다.

| 제목                                                                                                | 요약                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [명시적인 분석, 기록, 위임](https://hyune-c.notion.site/c1af634858874fd1a71fa67ac78d1e0b?pvs=4)             | <p>- 실무에서 동시에 여러가지의 일을 진행함에 있어 누락과 지연을 방지하기 위해서는<br>명시적인 문서화와 분업화가 필요하다고 생각 합니다.</p>                                                                                      |
| <p><a href="https://hyune-c.notion.site/d9240728504c46dcbe55b7f6d4a76ce9?pvs=4">자기 발전</a><br></p> | <p>- RSS 구독, 블로그 작성, 코드 리뷰어 &#x26; 멘토링 활동<br>- 실무에 적용 가능한 내용들을 사전에 학습하고 실제로 적용함</p>                                                                                       |
| [같이 자라기](https://hyune-c.notion.site/c2bc0343a13340899adac0880f6cb581?pvs=4)                      | - 꾸준한 사내 위키 작성, 기술 공유 & 교육 세션 진행                                                                                                                                          |
| <p>사이드 프로젝트 (종료)<br><a href="https://github.com/Our-Class-Bank/core-backend">repo</a></p>         | <p>- 우리반 은행 - 용돈관리, 신용점수 관리 프로그램<br>- 프론트 2, 백엔드 1<br>- 1명의 교사, 26명의 초등학생이 실 사용</p>                                                                                       |
| 타 언어에 대한 거부감이 적음                                                                                  | <p>- 알바체크: python 레거시를 java spring 으로 전환<br>- 컬리페이: go 레거시를 kotlin spring 으로 일부 전환<br>- 뤼튼: python, fast-api 기반으로 서비스 개발<br>- 대부분의 사이드 프로젝트에서 docker, shell script 사용</p> |