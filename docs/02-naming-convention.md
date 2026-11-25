# 02. 명명규칙 (Naming Convention)

- 상태: **확정** | 버전: 1.4

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

## 1. 공통 원칙 🔒
- 식별자는 **영문**을 사용하고, 약어는 표준 용어/약어 사전(02-2)에 등록된 것만 사용한다.
- 한글 발음 영문 표기(예: `sunsu`) 금지.
- 의미 없는 접두/접미(`my`, `tmp`, `data`, `info` 남용) 지양.
- 식별자 길이는 **40자 이내** 권장.
- 단일 문자 변수는 반복문 인덱스(`i`, `j`)에만 허용한다. 타입을 이름에 넣는 표기(헝가리안)는 사용하지 않는다.
- 단어는 **단수형**이 원칙이며, 복수는 `List` 접미사로 표현한다. (복수형 `s` 금지, API 4.3 과 동일)
- 언어 관례와 충돌하는 경우의 예외는 03-coding-convention 에서 정의한다.

## 2. 소스 코드 (언어 독립)
| 대상 | 케이스 | 규칙 | 예시 |
|---|---|---|---|
| 패키지/네임스페이스 | 소문자 | 루트는 프로젝트별 정의(✏️). **기능코드 폴더는 대문자 2자리** 허용(5.7 예외) | `com.falosis.finresearch.IS` |
| 업무 클래스/파일 | 5장 규칙 | `{시스템2}{기능2}{계층1}{일련번호4}{접미사}` | `FRISB0001Service` |
| 공통/설정 클래스 | PascalCase | 명사형, 5장 대상 아님(`common`, `config`) | `BsUtils`, `MiniConfig` |
| 인터페이스 | PascalCase | 접두 `I` 사용하지 않음 | |
| 메서드/함수 | camelCase | `{표준 동사}{Target}` 형식 (아래 참조) | `selectUserStrategy` |
| 변수/필드 | camelCase | 명사형, 컬렉션은 `List` 접미사 | `strategyList` |
| 상수 | UPPER_SNAKE_CASE | | `MAX_RETRY_COUNT` |
| Boolean | camelCase | `is` / `has` / `can` 접두 | `isUse`, `hasAuth` |
| enum 타입 / 값 | PascalCase 단수 / UPPER_SNAKE_CASE | | `StatusType` / `NORMAL` |

- 업무 클래스(Controller·Service·Dto·Mapper 등)의 이름은 5장 파일 명명규칙이 곧 클래스명이다. 계층별 접미사는 5.5·5.6 을 따른다.
- 파라미터명·지역 변수도 변수 규칙을 따른다.

### 메서드 동사 표준 🔒
API 기능명과 동일한 **표준 동사 사전(4.3)** 을 코드의 메서드명에도 사용한다. (`select`, `insert`, `update`, `delete`, `save`, `check`, `verify`, `execute` 등) `get`, `find`, `create`, `remove` 등 유사 동사는 사용하지 않는다.
- Controller 메서드명 = 기능명(4.6). Service·Mapper 메서드도 같은 사전의 동사를 사용한다.
- 단순 속성 접근자(`getter`/`setter`)는 언어·프레임워크 관례를 따르며 이 규칙의 예외이다.

### DB 컬럼 ↔ 코드 필드 매핑
- DB 컬럼(`UPPER_SNAKE_CASE`)은 코드 필드(`camelCase`)로 단어별 변환한다. 약어는 그대로 유지한다.
  - `CUST_ID` → `custId`, `FRST_REG_DTM` → `frstRegDtm`, `USE_YN` → `useYn`
- 필드 이름을 임의로 풀어쓰지 않는다. (`custId` 를 `customerId` 로 쓰지 않음)

## 3. 데이터베이스
DBMS 독립 규칙을 이 장에 두고, DBMS 전용 값(길이·타입·예약어·감사 컬럼)은 프로파일 문서에 둔다.
- **기본(default) 프로파일: Oracle** — [02-1-db-profile-oracle.md](02-1-db-profile-oracle.md) (금융권 SI). 별도 지정이 없으면 Oracle 을 적용한다.
- 표준 용어/약어 사전: [02-2-standard-term-dictionary.md](02-2-standard-term-dictionary.md)
- 🔒 고정 / ✏️ 가변

### 3.1 기본 원칙 🔒
1. **표기**: 영문 대문자(`A-Z`), 숫자(`0-9`), 언더스코어(`_`)만 사용하는 `UPPER_SNAKE_CASE`. 따옴표 식별자 사용 금지.
2. **길이**: 모든 DB 객체명·컬럼명은 프로파일이 정한 최대 길이 이내. (Oracle 프로파일: **30 Byte**)
3. **단어 조합**: 표준 용어/약어 사전(02-2)에 등록된 **영문 약어만 조합**한다. 임의의 축약어 사용 금지.
4. **예약어 금지**: DBMS 예약어 단독 사용 금지. (`USER` → `USR`, `ACCOUNT` → `ACNT` 등 사전의 예약어 회피 약어 사용)
5. 시작 문자는 영문, 단어는 단수형.

### 3.2 업무 구분 코드
- DB 객체명의 업무 구분은 5.3 **기능코드(2자리)** 를 그대로 사용한다. 파일명·URL·DB 가 같은 코드로 추적된다.
- **공통 업무(공통코드·권한·메뉴·사용자·배치관리 등)는 예약 기능코드 `CM`** 을 사용한다. (프로젝트에서 5.3 표에 `CM` 을 반드시 등록) 🔒
- 기존 금융권 3자리 업무코드 사례는 02-1 에 참고로 수록한다.

### 3.3 객체별 명명규칙
`{기능}` = 기능코드 2자리, `{테이블명}` = 접두 `TB_` 를 제외한 이름.

| 객체 | 명명 패턴 | 예시 | 비고 |
|---|---|---|---|
| 테이블 | `TB_` + `{기능}` + `_` + `{엔티티명}` + `_` + `{유형1}` | `TB_IS_USR_STRTG_M` | 3.4 유형 코드 |
| 파티션명 | `PT_` + `{기준년월 또는 년월일}` | `PT_202611`, `PT_20261125` | 월별 `YYYYMM`, 일별 `YYYYMMDD` |
| 뷰 | `VW_` + `{기능}` + `_` + `{뷰명}` | `VW_IS_STRTG_S` | |
| 기본키 (PK) | `PK_` + `{테이블명}` | `PK_IS_USR_STRTG_M` | 테이블당 1개 |
| 외래키 (FK) | `FK_` + `{자식테이블명}` + `_` + `{순번2}` | `FK_IS_USR_STRTG_D_01` | 성능상 미생성 후 앱 검증 권장 |
| 일반 인덱스 | `IX_` + `{테이블명}` + `_` + `{순번2}` | `IX_IS_USR_STRTG_M_01` | 01부터 순차 채번 |
| 유니크 인덱스 | `UX_` + `{테이블명}` + `_` + `{순번2}` | `UX_IS_USR_STRTG_M_01` | 고유키 제약용 |
| 시퀀스 | `SQ_` + `{기능}` + `_` + `{채번대상}` | `SQ_IS_STRTG_NO` | |
| 함수 | `FN_` + `{기능}` + `_` + `{기능명}` | `FN_CM_GET_CD_NM` | |
| 프로시저 | `SP_` + `{기능}` + `_` + `{기능명}` | `SP_IS_CLOSE_DAY` | |
| 패키지 | `PG_` + `{기능}` + `_` + `{기능명}` | | |
| 트리거 | `TR_` + `{테이블명}` + `_` + `{순번2}` | `TR_IS_USR_STRTG_M_01` | 이력 적재용 |
| 시노님 | 원 객체명과 동일 | `TB_IS_USR_STRTG_M` | 계정 분리 운영 시 |

- 함수/프로시저/패키지의 `{기능명}` 도 사전 약어만 사용한다. (`GET` 등 사전에 없는 단어는 등록 후 사용)
- 업무 로직은 가급적 애플리케이션 계층에서 처리하고, DB 객체(함수·프로시저·패키지·트리거)는 필요한 경우에 한해 사용한다.

### 3.4 테이블 유형 코드 (접미 1자리) 🔒
| 코드 | 구분 | 설명 | 예시 |
|---|---|---|---|
| `M` | Master (원장·기본) | 고객, 계좌, 계약 등 핵심 기준 정보 | `TB_IS_USR_STRTG_M` |
| `D` | Detail (상세) | 마스터의 하위 내역 | `TB_IS_USR_STRTG_D` |
| `H` | History (이력) | 변경 전/후 스냅샷 | `TB_IS_USR_STRTG_H` |
| `L` | Log (거래·로그) | 입출금, 전문 송수신, 접속 기록 | |
| `S` | Summary (집계·통계) | 일/월 마감 및 요약 | |
| `C` | Code (코드) | 공통코드 및 기준율(금리, 환율) | `TB_CM_CODE_C` |
| `I` | Interface (인터페이스) | 대외계 송수신 임시 테이블 | |
| `T` | Temp (임시) | 배치 작업용 임시 | |

### 3.5 컬럼 · 도메인 · 감사 컬럼 🔒
- 컬럼명 = `{수식 약어}_{도메인 접미어}` (예: `CUST_ID`, `OPEN_DT`, `TRN_AMT`).
- 도메인 접미어 및 데이터 타입은 프로파일(02-1) 2장을 따른다. 같은 의미의 컬럼은 모든 테이블에서 같은 이름·같은 도메인을 쓴다.
- 모든 테이블의 최하단에 **감사 컬럼 6개**(`FRST_REG_*`, `LAST_MDFCN_*`)를 필수로 둔다. (02-1 3장) `*_PGM_ID` 에는 6장 프로그램 ID 를 기록한다.
- `USE_YN`(사용 여부)은 필요한 테이블에 둔다. **논리삭제(`DEL_YN`)는 기본 필수가 아니며**, 삭제 이력은 이력 테이블(`H`)과 감사 컬럼으로 관리한다. 논리삭제가 필요한 테이블만 `DEL_YN` 을 추가한다.

### 3.6 SQL(Mapper) 식별자
- Mapper 의 SQL ID(메서드명)는 **표준 동사 사전(4.3)** 을 사용한다. (`selectUserStrategy`, `insertUserStrategy`, `updateUserStrategy`, `deleteUserStrategy`, `saveUserStrategy`)
- Mapper 파일은 5장 규칙(`FRISD0001Mapper`)을 따르고, 파일 위치는 `{기능코드}/Mapper` 이다.
- DB 컬럼(UPPER_SNAKE_CASE)과 코드 필드명(camelCase)의 매핑 규칙은 2장 "DB 컬럼 ↔ 코드 필드 매핑"을 따른다.

## 4. API / URL
언어·프레임워크와 무관한 규칙이다. 🔒 고정 / ✏️ 가변 / [제안]은 확정 전 안.
파일 명명규칙(5장)과 추적 가능해야 하므로 **URL ↔ API ID(접두부 9자) ↔ 기능코드 폴더**를 대장으로 연결한다.

### 4.1 HTTP 메서드 🔒
보안(WAF) 및 인프라 호환성을 위해 **`GET` 과 `POST` 만 사용**한다. `PUT`, `DELETE`, `PATCH` 등 그 외 메서드는 사용 금지.

| 메서드 | 용도 |
|---|---|
| `GET` | 단순 조건 조회, 파일 다운로드 |
| `POST` | 다중/복합 조건 검색(Request Body 필요 시), 등록, 수정, 삭제, 실행, 업로드 |

- 동작의 의미는 메서드가 아니라 **기능명의 동사**(4.3)로 표현한다.

### 4.2 URL 구조 🔒
```
/api/{기능코드2}/{기능명}
 예) POST /api/is/selectUserStrategy
```
| 구성 | 규칙 | 예시 |
|---|---|---|
| 접두 | `/api` 고정 | `/api` |
| 기능코드 | 5.3 기능코드 2자리, **소문자** | `is`, `am` |
| 기능명 | `{동사}{Target}` (4.3) | `selectUserStrategy` |

- 경로는 `/api/{기능코드2}/{기능명}` **2단계로 고정**한다. 하위 리소스 경로·path 변수는 사용하지 않고, 식별자·조건은 쿼리(GET) 또는 Request Body(POST)로 전달한다.
- URL에 확장자, 한글, 언더스코어, 끝 `/`, 파일 명명규칙의 ID(`FRISB0001`)를 쓰지 않는다.
- 내부 업무용이며 외부 시스템과 연결하지 않으므로 URL 버전(`v1`, `v2`)은 **현재 제외**한다. 버전 관리는 추후 고려 사항이다.

### 4.3 기능명 규칙 🔒
**형식**: `{동사}{Target}` — 동사는 소문자 camelCase 의 첫 단어, `Target` 은 PascalCase.

1. 사용하는 영단어는 **단수형만** 사용한다. (`user`, `transfer`, `asset`, `stock`)
2. `{Target}`: PascalCase **단수형**. 복수형 `s` 사용 금지. 다건이면 접미사 `List` 를 붙인다. (`UserStrategy`, `ScreenerList`)
3. 아래 **표준 동사 사전**의 동사만 사용한다. 유사 동사(`get`, `find`, `fetch`, `create`, `remove` 등) 혼용 금지.

#### 표준 동사 사전
| 구분 | 동사 / 형식 | 예시 |
|---|---|---|
| 조회 | 단건 `select{Target}` | `selectUser` |
| | 목록/조건 `select{Target}List` | `selectScreenerList` |
| | 건수 `select{Target}Count` | |
| | 코드/요약 `select{Target}CodeList`, `select{Target}Summary` | |
| 등록·수정·삭제·저장 | 단건 `insert{Target}`, `update{Target}`, `delete{Target}` | |
| | 다건 일괄 `insert{Target}List`, `update{Target}List`, `delete{Target}List` | |
| | Upsert(등록+수정, 그리드 일괄 저장) `save{Target}`, `save{Target}List` | `saveUserStrategy` |
| 상태 변경 | 단순 상태 변경 `update{Target}Status` | |
| | 승인/반려/취소 `approve{Target}`, `reject{Target}`, `cancel{Target}` | |
| 검증 | 중복/한도/유효성 사전 검증 `checkDuplicate{Target}`, `check{Target}` | |
| | 본인/비밀번호 인증 `verify{Target}` | |
| 비즈니스 실행 | 복합 금융/트랜잭션 실행 `execute{Target}` | `executeTransfer` |
| | 시뮬레이션/배치 실행 `simulate{Target}`, `execute{Target}Batch` | |
| 파일/엑셀 | 일반 파일 `upload{Target}File`, `download{Target}File` | |
| | 엑셀 `upload{Target}Excel`, `download{Target}Excel`, `download{Target}Template` | |
| 외부 연동/알림 | 데이터 동기화 `sync{Target}` | |
| | 알림/문자 발송 `send{Target}` | |

- 사전에 없는 동사가 필요하면 임의로 만들지 않고 이 사전에 먼저 등록(변경 절차는 00-governance)한 뒤 사용한다.

### 4.4 메서드 선택 기준 🔒
| 조건 | 메서드 |
|---|---|
| 단순 조건 조회(`select*`), 파일 다운로드(`download*`) | `GET` |
| 복합 조건 검색(Request Body 필요), `insert/update/delete/save`, 상태 변경, 검증, 실행, `upload*` 등 그 외 모두 | `POST` |

### 4.5 최종 예시
| 메서드 | URL | 설명 |
|---|---|---|
| POST | `/api/is/selectUserStrategy` | 고객의 투자전략 정보 불러오기 |
| POST | `/api/is/saveUserStrategy` | 고객의 투자전략 정보 저장하기 |

### 4.6 Controller 와 URL 매핑 🔒
- 하나의 Controller(API ID)에 **여러 URL 을 매핑**할 수 있다.
- **URL 매핑 단위는 Controller 메서드**이다. (메서드 1개 = URL 1개)
- **Controller 메서드명은 기능명과 동일**하게 한다. (`selectUserStrategy` 메서드 ↔ `/api/is/selectUserStrategy`)

### 4.7 API 대장 (URL ↔ ID 매핑) ✏️
대장은 **Controller 메서드(URL) 단위**로 한 행씩 작성하며, 같은 Controller 의 행은 API ID 를 공유한다.

| API ID(접두부) | 메서드 | URL | 한글명 | Controller | Controller 메서드 | 업무 유형 | 목표 응답 시간 | 상태 |
|---|---|---|---|---|---|---|---|---|
| FRISB0001 | POST | `/api/is/selectUserStrategy` | 투자전략 조회 | `IS/Controller/FRISB0001Controller` | `selectUserStrategy` | 일반 온라인 | 3초 이내 | |
| FRISB0001 | POST | `/api/is/saveUserStrategy` | 투자전략 저장 | `IS/Controller/FRISB0001Controller` | `saveUserStrategy` | 일반 온라인 | 3초 이내 | |

- **업무 유형·목표 응답 시간**은 06 3.3.1 응답 시간 기준표(초단기 실시간 / 일반 온라인 / 복합 연동·결제 / 대용량·배치성)로 분류하여 기록한다. 🔒

- 대장 위치는 08 산출물 구조를 따른다.

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
| CM | 공통 (예약) | Common — 공통코드·권한·메뉴·사용자·배치관리 등, 모든 프로젝트 필수 등록 |
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
| Api | API 호출 함수(`services`) | `FRISP0100Api` |
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
- **테스트 파일**: 대상 파일명 뒤에 `Test` 를 붙인다. (`FRISB0001Service` → `FRISB0001ServiceTest`) **프론트엔드는 Vitest 기본 패턴인 `{대상명}.test.ts(x)` 를 허용한다.** (`FRISP0001C.test.tsx`)
- **MyBatis XML 매퍼**: Mapper 인터페이스와 같은 base name 으로 만든다. (`FRISD0001Mapper` → `FRISD0001Mapper.xml`)
- **요청/응답 객체**: `Dto` 로 통일하는 것이 원칙이며, 필요한 경우에 한해 `ReqDto`, `ResDto` 로 구분할 수 있다. (`FRISB0000Dto`, 구분 시 `FRISB0000ReqDto` / `FRISB0000ResDto`) 구분하더라도 `Dto` 폴더에 함께 둔다.

| 계층 | 허용 접미사 |
|---|---|
| P | `P`, `M`, `C`, `Api` (필요 시 추가) |
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

**프론트엔드 (계층 P) 구조 (확정)**
소스 루트 `src/` 아래에 다음 최상위 폴더를 둔다.

| 폴더 | 역할 및 포함 내용 |
|---|---|
| `pages` | 메뉴 코드 및 URL 과 1:1 매핑되는 업무 화면 단위 |
| `components` | 화면을 구성하는 재사용 UI 컴포넌트 (공통·업무별 하위 분리) |
| `services` | 백엔드 전문(API) 호출 함수 및 요청/응답 DTO 매핑 |
| `stores` | 사용자 세션, 권한, 공통 코드 등 전역 상태 관리 |
| `routes` | 메뉴 트리 기반 라우팅, 세션 타임아웃 및 접근 권한 가드 |
| `hooks` | 입력값 검증(주민번호/계좌/금액), 포맷팅 등 공통 커스텀 훅 |
| `utils` | 금액 원화/외화 계산(BigDecimal.js 등), 암호화, 날짜 유틸리티 |
| `constants` | 오류 코드, 전문 헤더 상수, 정규식 패턴 정의 |
| `types` | 공통 전문 규격(`pageNo`, `pageSize`, `totalCnt`) 및 전역 인터페이스 |
| `assets` | CI/BI 이미지, 웹폰트, 공통 스타일시트 |

- `pages`·`components`·`services` 아래는 파일명 **앞 4자리(시스템+기능, 예: `FRAM`)** 기준의 **기능코드 폴더**(`AM`)로 구분하고, 공통은 `common` 폴더에 둔다. [제안]
- `pages` 에는 메인 화면(`M`), `components` 에는 컴포넌트(`C`)와 팝업(`P`), `services` 에는 API 호출 파일(`Api`)을 둔다. 역할 접미사별 하위 폴더는 만들지 않는다. [제안]
- `stores`·`routes`·`hooks`·`utils`·`constants`·`types`·`assets` 는 기능과 무관한 공통 영역이며 5.1 파일 명명규칙 대상이 아니다. (자유 명명, 훅은 `use` 로 시작, 스토어는 `…Store`)
- 최상위 폴더 추가·변경은 표준 관리자 승인 후 이 표에 등록한다.

```
src
├─ pages
│   ├─ AM
│   │   ├─ FRAMP0000M.tsx
│   │   ├─ FRAMP0100M.tsx
│   │   ├─ FRAMP0200M.tsx
│   │   └─ FRAMP0210M.tsx
│   └─ IS
│       └─ FRISP1000M.tsx
├─ components
│   ├─ common               # 공통 UI
│   ├─ AM
│   │   ├─ FRAMP0001P.tsx   # 팝업
│   │   └─ FRAMP0201C.tsx   # 컴포넌트
│   └─ IS
│       └─ FRISP1010C.tsx
├─ services
│   ├─ common               # 단일 API 클라이언트·공통 호출
│   ├─ AM
│   │   └─ FRAMP0100Api.ts
│   └─ IS
├─ stores
├─ routes
├─ hooks
├─ utils
├─ constants
├─ types
└─ assets
```
- `pages` 의 화면 경로 형식과 메뉴 코드 체계는 프로젝트별로 정한다. [결정 필요]

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
| 프로그램 ID | 접두부 9자 (파일명에서 역할 접미사 제외). 대장은 접두부 9자 + 접미사 단위로 관리 | `FRISB0001` / 대장: `FRISB0001Controller` |
| 화면 ID | 접두부 9자, 계층 `P` 또는 `U` | `FRISP0001` |
| API/서비스 ID | 접두부 9자, 계층 `B` 또는 `U` | `FRISB0001` |
| 데이터(DB) 접근 ID | 접두부 9자, 계층 `D` | `FRISD0001` |
| 인터페이스 ID | `IF` + 송신시스템(3) + 수신시스템(3) + 처리유형(1) + 업무코드(3) + 일련번호(4) = **16자리 고정**. 상세는 [02-3-interface-id.md](02-3-interface-id.md) | `IFMBKCOROLON0001` |
| 에러 코드 (**인터페이스 ID 와 별개 체계**) | `E` + **순번 4자리**. **시스템 오류 전용**(업무 예외는 에러 코드를 쓰지 않고 응답의 예외 데이터로 전달, 04 3.1·5장) | `E0493` |
| 공통코드 그룹 ID ✏️ 가변 | 프로젝트별로 정의 (아래 6.1) | 프로젝트 생성 시 확정 |

- 같은 접두부를 쓰는 파일·화면·API·에러코드는 하나의 기능 단위로 본다.
- **프로그램 ID 대장**은 `프로그램(접두부 9자 + 접미사 n자)` 단위로 관리한다. (예: `FRISB0001Controller`, `FRISB0001Service`) 항목: 프로그램 ID 전체 / 접두부 / 접미사 / 한글명 / 기능코드 / 계층 / 담당자 / 상태. 위치는 [08-deliverables-structure.md](08-deliverables-structure.md) 참조.
- 에러 코드는 인터페이스 ID 와 **별개로 관리**한다. (프로그램·화면·API 와도 독립된 코드 체계)
- 인터페이스 ID 는 소스 코드 체계(5.1~5.4)와 **별개의 독립 체계**(별개의 시스템)이다. 인터페이스 업무코드(3자리)와 기능코드(2자리)는 서로 별개로 사용하며 매핑하지 않는다. (02-3)

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
- 로그 카테고리: 03 4.3 로그 종류(`app`·`error`·`access`·`audit`)와 같은 이름을 사용한다. 설정 키(`application-{환경}.yml`)는 Spring 관례의 kebab-case 를 따른다.
- 테스트: `대상Test`, 메서드 `메서드_상황_기대결과`

## 변경이력
| 버전 | 일자 | 작성자 | 내용 |
|---|---|---|---|
| 0.1 | | | 최초 작성 |
| 1.0 | | | **확정**. 잔여 `[결정 필요]`(프로젝트별·기술 확정 후 항목)는 해당 시점에 MINOR 개정으로 반영 |
| 1.1 | | | FE 테스트 파일 `.test.tsx` 허용 반영 |
| 1.2 | | | MyBatis XML 매퍼 파일명 규칙 추가 |
| 1.3 | | | FE 공통 폴더 목록, 로그 카테고리·설정 키 규칙 추가 `[제안]` |
| 1.4 | | | FE `src/` 최상위 폴더 구조(pages·components·services·stores·routes·hooks·utils·constants·types·assets) 확정, `Api` 접미사 추가, 로그 카테고리·설정 키 확정 |
