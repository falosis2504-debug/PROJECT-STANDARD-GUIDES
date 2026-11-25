# 02. 명명규칙 (Naming Convention)

- 상태: 초안 | 버전: 0.1

## 목표
코드·DB·API·파일·식별자의 이름을 일관되게 짓는 규칙을 정한다. 대상별로 **규칙 / 예시 / 금지** 를 채운다.

## 작성 방법
각 절의 `[결정 필요]` 항목을 채운다. 케이스 표기 약어:
`camelCase`, `PascalCase`, `snake_case`, `UPPER_SNAKE_CASE`, `kebab-case`

## 1. 공통 원칙
- 영문 사용, 의미 있는 이름, 약어는 표준 약어 사전에 등록된 것만 사용
- 한글 발음 영문 표기(예: `sunsu`) 금지 [결정 필요]
- 불필요한 접두/접미(`my`, `tmp`, `data`, `info` 남용) 지양
- 길이 상한: [결정 필요]

## 2. 소스 코드
| 대상 | 케이스 | 규칙 | 예시 | 금지 예시 |
|---|---|---|---|---|
| 패키지/네임스페이스 | | | `com.회사.프로젝트.모듈` | |
| 클래스/타입 | PascalCase | 명사형 | `OrderService` | |
| 인터페이스 | | 접두 `I` 사용 여부 [결정 필요] | | |
| 메서드/함수 | camelCase | 동사로 시작 | `findOrderById` | |
| 변수 | camelCase | | | |
| 상수 | UPPER_SNAKE_CASE | | `MAX_RETRY_COUNT` | |
| Boolean | | `is/has/can` 접두 | `isActive` | |
| enum | | | | |

### 계층별 접미사 [결정 필요]
| 계층 | 접미사 | 예시 |
|---|---|---|
| Controller | `Controller` | `OrderController` |
| Service | `Service` / `ServiceImpl` | |
| Repository/DAO | `Repository` / `Dao` | |
| DTO | `Request` / `Response` / `Dto` | |
| Entity/VO | `Entity` / `Vo` | |

### 메서드 동사 표준
| 동작 | 동사 | 비고 |
|---|---|---|
| 단건 조회 | `get` / `find` | 차이 정의 [결정 필요] |
| 목록 조회 | `list` / `search` | |
| 등록 | `create` / `insert` | |
| 수정 | `update` | |
| 삭제 | `delete` | |
| 존재 확인 | `exists` | |

## 3. 데이터베이스
| 대상 | 규칙 | 예시 |
|---|---|---|
| 테이블 | `snake_case`, 접두(업무구분) [결정 필요], 단수/복수 [결정 필요] | `ord_order` |
| 컬럼 | `snake_case` | `order_dt` |
| PK | `pk_테이블` | |
| FK | `fk_자식_부모_컬럼` | |
| 인덱스 | `ix_테이블_컬럼` / 유니크 `ux_` | |
| 시퀀스 | `sq_테이블` | |
| 뷰 | `v_` | |
| 공통 컬럼 | `created_at`, `created_by`, `updated_at`, `updated_by`, `use_yn`/`del_yn` | |

### 표준 도메인/용어 사전 [결정 필요]
| 한글명 | 영문명 | 약어 | 타입/길이 |
|---|---|---|---|
| 일자 | date | dt | |
| 코드 | code | cd | |
| 명 | name | nm | |
| 여부 | yn | yn | CHAR(1) |

## 4. API / URL
| 대상 | 규칙 | 예시 |
|---|---|---|
| URL 경로 | kebab-case, 소문자, 복수 명사 | `/api/v1/orders/{orderId}` |
| 쿼리 파라미터 | camelCase / snake_case [결정 필요] | |
| JSON 필드 | camelCase [결정 필요] | |
| HTTP 메서드 | GET 조회, POST 등록, PUT/PATCH 수정, DELETE 삭제 | |
| 버전 | 경로 `/v1` | |

## 5. 파일/디렉터리
| 대상 | 규칙 | 예시 |
|---|---|---|
| 소스 디렉터리 | | |
| 설정 파일 | `application-{env}.yml` | |
| SQL/마이그레이션 | `V{버전}__{설명}.sql` | |
| 문서 | `NN-kebab-case.md` | |
| 리소스(이미지 등) | kebab-case | |

## 6. 업무 식별자 (SI 공통)
| 대상 | 규칙 | 예시 |
|---|---|---|
| 업무(모듈) 코드 | 영문 2~3자 [결정 필요] | `ORD`, `CUS` |
| 화면 ID | `업무코드 + 화면유형 + 일련번호` | `ORD-S-0001` |
| 프로그램 ID | | |
| 인터페이스 ID | `IF-송신-수신-일련번호` | |
| 공통코드 그룹ID | | |
| 에러/메시지 코드 | `업무코드 + 구분 + 번호` | `ORD-E-1001` |

## 7. 기타
- 환경변수: `UPPER_SNAKE_CASE`, 접두 `APP_`
- 로그 카테고리 / 설정 키: [결정 필요]
- 테스트: `대상Test`, 메서드 `메서드_상황_기대결과`

## 변경이력
| 버전 | 일자 | 작성자 | 내용 |
|---|---|---|---|
| 0.1 | | | 최초 작성 |
