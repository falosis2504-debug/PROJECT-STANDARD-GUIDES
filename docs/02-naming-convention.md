# 02. 명명규칙 (Naming Convention)

- 상태: 초안 | 버전: 0.1

## 목표
코드·DB·API·파일·식별자의 이름을 일관되게 짓는 규칙을 정한다. 대상별로 **규칙 / 예시 / 금지** 를 채운다.

## 작성 방법
언어·프레임워크·DBMS는 수시로 바뀌므로 **특정 기술에 종속되지 않는 규칙부터** 확정한다. 기술 종속 항목은 `[기술 확정 후]` 로 보류한다. 현재 확정 대상은 **5. 파일 명명규칙**.

> **이 문서는 템플릿이다.** 구성 규칙(형식·자릿수·폴더 구조·접미사)은 모든 프로젝트 공통의 **고정 규칙**이고,
> 시스템코드·기능코드·중분류·공통코드 그룹 ID 같은 **값**은 프로젝트 생성 시 업무 특성을 모두 파악한 뒤 프로젝트별로 정의한다.
> 문서 안의 `FR`, `AM`, `IS` 등은 모두 **예시(샘플 프로젝트: 금융 정보 리서치)** 이며, 신규 프로젝트에서는 5.2·5.3·5.1.1 표를 해당 프로젝트 값으로 교체한다.
> - 🔒 고정: 모든 프로젝트에 동일 적용 / ✏️ 가변: 프로젝트별 정의

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
언어·프레임워크와 무관한 규칙이다. 🔒 고정 / ✏️ 가변 / [제안]은 확정 전 안.
파일 명명규칙(5장)과 추적 가능해야 하므로 **URL ↔ API ID(접두부 9자) ↔ 기능코드 폴더**를 대장으로 연결한다.

### 4.1 URL 구조
```
/api/{버전}/{기능코드}/{리소스}[/{식별자}][/{하위리소스}]
 예) /api/v1/is/indicator-combos/{comboId}/diagnoses
```
| 구성 | 규칙 | 구분 | 예시 |
|---|---|---|---|
| 접두 | `/api` 고정 | 🔒 | `/api` |
| 버전 | `v{정수}`, 호환 불가 변경 시에만 증가 | 🔒 | `v1` |
| 기능코드 | 5.3 기능코드를 **소문자**로 사용 | 🔒 | `is`, `am` |
| 리소스 | 소문자 kebab-case, 복수 명사, 영문 | 🔒 | `indicator-combos` |
| 식별자 | path 변수, 중괄호 표기 | 🔒 | `{comboId}` |
| 리소스 이름 값 | 업무 분석 후 프로젝트별 정의 | ✏️ | |

- 첫 세그먼트 이후 계층은 **3단계 이내** 권장 [제안].
- URL에 동사 금지. 동작은 HTTP 메서드로 표현한다. (예외: 4.3 액션)
- URL에 확장자(`.json` 등), 대문자, 언더스코어, 한글, 파일명 규칙의 ID(`FRISB0001`) 사용 금지.
- 마지막 `/` 는 붙이지 않는다.

### 4.2 HTTP 메서드
| 메서드 | 용도 | 예시 |
|---|---|---|
| GET | 조회 (목록/단건), 본문 없음, 부작용 없음 | `GET /api/v1/is/indicator-combos` |
| POST | 등록 | `POST /api/v1/is/indicator-combos` |
| PUT | 전체 수정 | `PUT /api/v1/is/indicator-combos/{comboId}` |
| PATCH | 부분 수정 | `PATCH /api/v1/is/indicator-combos/{comboId}` |
| DELETE | 삭제 | `DELETE /api/v1/is/indicator-combos/{comboId}` |

### 4.3 액션(동사) 예외 [제안]
CRUD로 표현하기 어려운 처리는 마지막 세그먼트에 **kebab-case 동사**를 쓰고 `POST` 를 사용한다.
- 예) `POST /api/v1/at/transfers/{transferId}/cancel`, `POST /api/v1/es/screenings/execute`
- 조회성 복합 조건 검색은 `GET` + 쿼리, 조건이 길면 `POST /{리소스}/search` 허용 [제안].

### 4.4 쿼리 파라미터 / 본문
| 대상 | 규칙 | 구분 |
|---|---|---|
| 쿼리 파라미터 | camelCase | [제안] |
| JSON 필드 | camelCase | [제안] |
| 날짜/시간 | 날짜 `yyyy-MM-dd`, 일시 ISO-8601 | [제안] |
| 불리언 | `true`/`false` (문자 `Y/N` 금지) | [제안] |
| 목록 조회 공통 | `page`, `size`, `sort` (`sort=field,asc`) | [제안] |

- 요청/응답 객체명은 5장 `Dto`(`ReqDto`/`ResDto`) 규칙을 따른다. JSON 필드명과 DTO 필드명은 같은 이름을 사용한다.
- 공통 응답 포맷·에러 응답은 04-design-standard.md 에서 정의하며, 에러 코드는 인터페이스 ID 기준(6장)이다.

### 4.5 API 대장 (URL ↔ ID 매핑) ✏️
프로젝트별로 대장을 작성하여 URL 과 파일명 규칙의 ID 를 연결한다.

| API ID(접두부) | 메서드 | URL | 한글명 | Controller | 상태 |
|---|---|---|---|---|---|
| FRISB0100 | GET | `/api/v1/is/indicator-combos` | 지표조합 목록 | `IS/Controller/FRISB0100Controller` | |
| FRISB0101 | POST | `/api/v1/is/indicator-combos/{comboId}/diagnoses` | 지표조합 진단 | `IS/Controller/FRISB0101Controller` | |

- 일련번호의 상위 2자리(중분류)는 하나의 **리소스**에 대응시키는 것을 원칙으로 한다. (예: `IS01xx` = `indicator-combos`) [제안]
- 대장 위치는 프로젝트별 [결정 필요].

## 5. 파일 명명규칙 (확정안, 언어·프레임워크 독립)

### 5.1 기본 형식
```
[시스템코드(2)][기능(2)][계층구분(1)][일련번호(4)] + 역할 접미사
 FR               IS      B            0001           Controller
→ FRISB0001Controller
```
- 접두부 9자(`시스템 2 + 기능 2 + 계층 1 + 일련번호 4`)는 대문자 영문 + 숫자, 그 뒤에 역할 접미사를 붙인다.
- 같은 접두부(`FRISB0001`)를 공유하는 파일은 하나의 기능 단위이다. (예: `FRISB0001Controller`, `FRISB0001Service`, `FRISB0001Mapper`, `FRISB0001Dto`)
- 일련번호(4자리)는 `시스템+기능+계층` 단위로 부여하며 연속일 필요는 없다. (예: `0001`, `0100`, `5000`) 번호 구성은 5.1.1을 따른다. 부여된 번호는 재사용하지 않는다.

### 5.1.1 일련번호 구성 🔒 고정 (표의 업무 내용은 ✏️ 예시)
일련번호 4자리 = **상위 2자리(중분류) + 하위 2자리(소분류/최소업무단위)**.
- 하위가 `00` 이면 해당 중분류의 메인(대표) 화면/기능이다.
- 같은 중분류는 같은 상위 2자리를 공유한다.

| 번호 | 의미 (예시: `IS` 투자전략) |
|---|---|
| `0000` | 투자전략 / 홈 / 메인 |
| `0100` | 투자전략 / 지표조합 / 메인 |
| `0101` | 투자전략 / 지표조합 / 진단 step1 |
| `0102` | 투자전략 / 지표조합 / 진단 step2 |
| `0200` | 투자전략 / 거시예측 / 메인 |

- 중분류(상위 2자리)는 기능코드별로 대장에 등록한 뒤 사용한다. 중분류당 소분류는 최대 100개(`00`~`99`).

### 5.2 시스템코드 (2자리) ✏️ 가변 — 프로젝트별 정의
아래는 예시이다.

| 코드 | 시스템 |
|---|---|
| FR | 금융 정보 리서치 시스템 (Financial Information Research System) |
| (추가) | |

### 5.3 기능코드 (2자리) ✏️ 가변 — 프로젝트별 정의
아래는 예시이다. 업무 분석 후 기능(업무) 단위를 확정하여 등록한다.

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
| Dto | 데이터 전송 객체 (원칙) | `FRISB0001Dto` |
| ReqDto / ResDto | 요청/응답 구분이 필요한 경우 (`Dto` 폴더에 둠) | `FRISB0000ReqDto`, `FRISB0000ResDto` |
| Mapper | DB 매퍼 | `FRISD0001Mapper` |
| Repository | 저장소 | `FRISD0001Repository` |
| Entity | 엔티티 | `FRISD0001Entity` |
| (추가) | 필요 시 정의 | |

### 5.6 세부 규칙 (확정)
- 확장자는 언어에 따르며 이 규칙은 확장자 앞 이름(base name)에만 적용한다.
- **계층 `U`**: 프론트·백엔드 역할 접미사를 모두 사용할 수 있다.
- **계층 `D`**: `Mapper`, `Repository`, `Entity` 등 DB와 연관된 접미사를 사용할 수 있다.
- **테스트 파일**: 대상 파일명 뒤에 `Test` 를 붙인다. (`FRISB0001Service` → `FRISB0001ServiceTest`)
- **요청/응답 객체**: `Dto` 로 통일하는 것이 원칙이며, 필요한 경우에 한해 `ReqDto`, `ResDto` 로 구분할 수 있다. (`FRISB0000Dto`, 구분 시 `FRISB0000ReqDto` / `FRISB0000ResDto`) 구분하더라도 `Dto` 폴더에 함께 둔다.

| 계층 | 허용 접미사 |
|---|---|
| P | `P`, `M`, `C` (필요 시 추가) |
| B | `Controller`, `Service`, `Dto`, `ReqDto`, `ResDto` |
| D | `Mapper`, `Repository`, `Entity` 등 DB 연관 접미사 |
| U | P·B·D 의 접미사 전부 |

### 5.7 디렉터리 구조 (확정)
**원칙**
- 최상위(루트 패키지) 아래에 `common`, `config`, 그리고 **기능코드(2자리, 대문자) 폴더**를 둔다.
- 기능코드 폴더 아래에는 **역할 접미사와 동일한 이름의 폴더**를 둔다. (`Controller`, `Service`, `Dto`, `Mapper` …) 폴더명은 접미사를 그대로 쓰고, 해당 접미사의 파일만 그 폴더에 둔다.
- `common`, `config` 는 업무 공통/설정 영역으로 5.1의 파일 명명규칙 적용 대상이 아니다. (자유 명명, 예: `BsUtils`, `MiniConfig`)
- 시스템코드는 파일명(접두부)에 포함되므로 폴더에는 별도로 두지 않는다.

**예시** (`com.falosis.finresearch`)
```
com.falosis.finresearch
├─ common
│   └─ BsUtils.java
├─ config
│   └─ MiniConfig.java
├─ IS                              # 기능코드: 투자전략
│   ├─ Controller
│   │   ├─ FRISB0001Controller.java
│   │   └─ FRISB0100Controller.java
│   ├─ Service
│   │   ├─ FRISB0001Service.java
│   │   └─ FRISB0100Service.java
│   ├─ Dto
│   │   ├─ FRISB0000Dto.java
│   │   ├─ FRISB0000ReqDto.java
│   │   └─ FRISB0000ResDto.java
│   └─ Mapper
│       └─ FRISB0000Mapper.java
└─ AM                              # 기능코드: 자산관리
    ├─ Controller
    │   └─ FRAMB5000Controller.java
    └─ Service
        └─ FRAMB5000Service.java
```

**규칙 요약**
| 항목 | 규칙 |
|---|---|
| 기능 폴더 | 기능코드 2자리 대문자 (`IS`, `AM` …) |
| 역할 폴더 | 역할 접미사와 동일 (`Controller`, `Service`, `Dto`, `Mapper`, `Repository`, `Entity`). `ReqDto`/`ResDto` 는 별도 폴더 없이 `Dto` 폴더 사용 |
| 파일 위치 | `{기능코드}/{역할접미사}/{파일명}` |
| 폴더-파일 일치 | 파일의 기능코드·접미사가 소속 폴더와 반드시 일치 (`FRISB0001Service` → `IS/Service`) |
| 일련번호 | 폴더가 달라도 같은 기능 단위는 동일 접두부 사용 (`IS/Controller/FRISB0001Controller`, `IS/Service/FRISB0001Service`) |

**프론트엔드 (계층 P) 폴더 (확정)**
- 파일명 **앞 4자리(시스템+기능, 예: `FRAM`)** 기준으로 기능코드 폴더(`AM`)에 둔다.
- 역할 접미사(`P`, `M`, `C`)별 하위 폴더는 만들지 않고, 기능코드 폴더 바로 아래에 파일을 둔다. (백엔드와 달리 flat)
- 기능코드 폴더 외에 `common`, `stores`, `routes` 등 공통 폴더를 같은 레벨에 둔다.

```
finresearch-pro
├─ AM
│   ├─ FRAMP0001P.js
│   ├─ FRAMP0000M.js
│   ├─ FRAMP0100M.js
│   ├─ FRAMP0200M.js
│   ├─ FRAMP0201C.js
│   └─ FRAMP0210M.js
├─ IS
│   ├─ FRISP1000M.js
│   └─ FRISP1010C.js
├─ common
├─ stores
└─ routes            # 등
```
- 공통 폴더(`common`, `stores`, `routes` 등)는 5.1 파일 명명규칙 대상이 아니다. 허용 공통 폴더 목록은 프론트 기술 확정 후 [결정 필요].

### 5.8 그 외 파일/디렉터리
| 대상 | 규칙 | 예시 |
|---|---|---|
| 설정 파일 | [언어·프레임워크 확정 후] | |
| SQL/마이그레이션 | `V{버전}__{설명}.sql` | |
| 문서 | `NN-kebab-case.md` | |
| 리소스(이미지 등) | kebab-case | |

## 6. 업무 식별자 (파일 명명규칙과 정합)
업무 식별자는 5.1의 **접두부 9자** `[시스템][기능][계층][일련번호]` 를 기준으로 파생한다. 파일명 ↔ 식별자 ↔ 폴더가 서로 추적 가능해야 한다.

| 대상 | 규칙 | 예시 |
|---|---|---|
| 시스템 코드 | 5.2 | `FR` |
| 업무(기능) 코드 | 5.3 | `IS`, `AM` |
| 프로그램 ID | 접두부 9자 (파일명에서 역할 접미사 제외) | `FRISB0001` |
| 화면 ID | 접두부 9자, 계층 `P` 또는 `U` | `FRISP0001` |
| API/서비스 ID | 접두부 9자, 계층 `B` 또는 `U` | `FRISB0001` |
| 데이터(DB) 접근 ID | 접두부 9자, 계층 `D` | `FRISD0001` |
| 인터페이스 ID [제안] | `[시스템][기능]` + `I` + 일련번호 4 → 9자 형식 유지 (일련번호는 5.1.1) | `FRISI0100` |
| 에러/메시지 코드 (**인터페이스 ID 기준**) | `인터페이스 ID + "-" + 구분(E/W/I) + 번호 3` | `FRISI0100-E001` |
| 공통코드 그룹 ID ✏️ 가변 | 프로젝트별로 정의 (아래 6.1) | 프로젝트 생성 시 확정 |

- 같은 접두부를 쓰는 파일·화면·API·에러코드는 하나의 기능 단위로 본다.
- 프로그램 ID 목록(대장)을 별도 관리한다: 접두부 / 한글명 / 기능코드 / 계층 / 담당자 / 상태. [결정 필요: 대장 위치]
- 에러/메시지 코드는 인터페이스 ID를 기준으로 부여한다. (확정) 구분은 `E` 오류 / `W` 경고 / `I` 안내, 번호 3자리는 [제안].
- `[제안]` 항목은 확정 전 안이며, 인터페이스용 계층 문자 `I` 도입 여부는 5.4 계층구분과 충돌하므로 결정이 필요하다.

### 6.1 공통코드 그룹 ID — 프로젝트별 가변
공통코드 그룹 ID는 고정 형식을 두지 않는다. 프로젝트 생성 시 **각 업무 특성을 모두 파악한 뒤** 프로젝트별로 체계를 정하고 생성한다.

**정의 절차**
1. 업무(기능) 분석 결과에서 공통으로 쓰이는 코드성 데이터(상태, 구분, 유형 등)를 수집한다.
2. 업무 간 공유되는 코드와 특정 업무 전용 코드를 구분한다.
3. 그룹 ID 체계(형식·자릿수·접두 규칙)를 프로젝트 표준으로 확정하여 이 절에 기록한다.
4. 그룹 ID 대장을 만들어 등록 후 사용한다. (그룹 ID / 그룹명 / 사용 업무 / 코드 값 목록 / 담당자)

**프로젝트별 확정 기록** (신규 프로젝트에서 작성)
| 항목 | 내용 |
|---|---|
| 그룹 ID 형식 | |
| 업무 공유 코드 / 업무 전용 코드 구분 방식 | |
| 대장 위치 | |

## 7. 기타
- 환경변수: `UPPER_SNAKE_CASE`, 접두 `APP_`
- 로그 카테고리 / 설정 키: [결정 필요]
- 테스트: `대상Test`, 메서드 `메서드_상황_기대결과`

## 변경이력
| 버전 | 일자 | 작성자 | 내용 |
|---|---|---|---|
| 0.1 | | | 최초 작성 |
