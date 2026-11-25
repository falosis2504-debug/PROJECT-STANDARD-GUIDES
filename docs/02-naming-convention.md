# 02. 명명규칙 (Naming Convention)

- 상태: 초안 | 버전: 0.1

## 목표
코드·DB·API·파일·식별자의 이름을 일관되게 짓는 규칙을 정한다. 대상별로 **규칙 / 예시 / 금지** 를 채운다.

## 작성 방법
언어·프레임워크·DBMS는 수시로 바뀌므로 **특정 기술에 종속되지 않는 규칙부터** 확정한다. 기술 종속 항목은 `[기술 확정 후]` 로 보류한다. 현재 확정 대상은 **5. 파일 명명규칙**.

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

## 5. 파일 명명규칙 (확정안, 언어·프레임워크 독립)

### 5.1 기본 형식
```
[시스템코드(2)][기능(2)][계층구분(1)][일련번호(4)] + 역할 접미사
 FR               IS      B            0001           Controller
→ FRISB0001Controller
```
- 접두부 9자(`시스템 2 + 기능 2 + 계층 1 + 일련번호 4`)는 대문자 영문 + 숫자, 그 뒤에 역할 접미사를 붙인다.
- 같은 접두부(`FRISB0001`)를 공유하는 파일은 하나의 기능 단위이다. (예: `FRISB0001Controller`, `FRISB0001Service`, `FRISB0001Mapper`, `FRISB0001Dto`)
- 일련번호는 `시스템+기능+계층` 단위로 0001부터 채번하고, 결번은 재사용하지 않는다.

### 5.2 시스템코드 (2자리)
| 코드 | 시스템 |
|---|---|
| FR | 금융 정보 리서치 시스템 (Financial Information Research System) |
| (추가) | |

### 5.3 기능코드 (2자리)
| 코드 | 기능 | 영문 |
|---|---|---|
| AM | 자산관리 | Asset Management |
| AT | 계좌이체 | Account Transfer |
| ES | 종목스크리너 | Equity Screener |
| IS | 투자전략 | Investment Strategy |
| IO | 투자기회 | Investment Opportunity |
| (추가) | | |

- 신규 기능코드는 이 표에 먼저 등록한 뒤 사용한다. 시스템 내 중복 금지.

### 5.4 계층구분 (1자리)
| 코드 | 계층 | 내용 |
|---|---|---|
| P | Presentation | 프론트엔드, 표현 계층, UI, 사용자 입력 처리 |
| B | Business | 백엔드(로직), 비즈니스 계층, 핵심 로직, API 처리 |
| D | Data | 백엔드(DB), 데이터 계층, DB 연동 및 저장 |
| U | Unified | 통합 계층, 프론트와 백엔드가 하나로 합쳐진 형태 |

### 5.5 역할 접미사
**프론트엔드 (계층 P)**
| 접미사 | 의미 | 예시 |
|---|---|---|
| P | 팝업 | `FRISP0001P` |
| M | 바닥/메인 페이지 | `FRISP0001M` |
| C | 컴포넌트 | `FRISP0001C` |
| (추가) | 필요 시 정의 | |

**백엔드 (계층 B, D)**
| 접미사 | 의미 | 예시 |
|---|---|---|
| Controller | 컨트롤러 | `FRISB0001Controller` |
| Service | 서비스 | `FRISB0001Service` |
| Dto | 데이터 전송 객체 | `FRISB0001Dto` |
| Mapper | DB 매퍼 | `FRISD0001Mapper` |
| (추가) | 필요 시 정의 | |

### 5.6 정리할 사항 [결정 필요]
- 확장자는 언어에 따르며 이 규칙은 확장자 앞 이름(base name)에만 적용한다.
- 계층 `U` 의 역할 접미사 (프론트·백엔드 접미사 중 허용 범위)
- 계층 `D` 의 접미사 범위 (`Mapper` 외 `Repository`, `Entity` 등 추가 여부)
- 다중 구현·테스트 파일: `FRISB0001ServiceTest` 처럼 접미사 뒤에 `Test` 를 붙이는지
- Request/Response 를 `Dto` 로 통일할지, `ReqDto`/`ResDto` 로 구분할지

### 5.7 그 외 파일/디렉터리
| 대상 | 규칙 | 예시 |
|---|---|---|
| 소스 디렉터리 | 기능코드/계층 기준 [결정 필요] | |
| 설정 파일 | [언어·프레임워크 확정 후] | |
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
