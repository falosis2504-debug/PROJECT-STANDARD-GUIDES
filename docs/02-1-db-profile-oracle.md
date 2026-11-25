# 02-1. DB 프로파일 — Oracle (금융권 SI)

- 상태: 초안 | 버전: 0.1
- 상위 문서: [02-naming-convention.md](02-naming-convention.md) 3장 (DBMS 독립 규칙)
- 약어 사전: [02-2-standard-term-dictionary.md](02-2-standard-term-dictionary.md)

## 목적
02번 3장의 DBMS 독립 규칙에 **Oracle 전용 값**(길이, 타입, 예약어, 감사 컬럼)을 더한 프로파일이다.
DBMS 가 바뀌면 이 문서만 해당 DBMS 프로파일로 교체한다.

## 1. Oracle 전용 제약
| 항목 | 규칙 |
|---|---|
| 식별자 길이 | 모든 DB 객체명·컬럼명은 **최대 30 Byte** (하위 호환성 및 메타 관리) |
| 예약어 | `USER`, `ORDER`, `DATE`, `ACCOUNT`, `NUMBER`, `LEVEL`, `GROUP`, `COMMENT` 등 Oracle 예약어는 **단독 사용 금지** (약어 사전의 예약어 회피 약어 사용: `USR`, `ACNT`, `DT`, `NO`, `GRP`, `DESC` 등) |
| 표기 | `A-Z`, `0-9`, `_` 만 사용 |

## 2. 표준 도메인 (컬럼 접미어 & 데이터 타입)
| 도메인 분류 | 접미어 | Oracle 권장 타입 | 예시 | 설명 |
|---|---|---|---|---|
| 식별자 | `_ID` | `VARCHAR2(20)` | `CUST_ID`, `EMP_ID` | 고객ID, 행원ID |
| 번호 | `_NO` | `VARCHAR2(20)` | `ACNT_NO`, `DEAL_NO` | 계좌번호, 거래번호 |
| 일련번호 | `_SEQ` | `NUMBER(10)` | `HIST_SEQ`, `DTL_SEQ` | 이력순번, 상세순번 |
| 코드 | `_CD` | `VARCHAR2(10)` | `BANK_CD`, `PROD_CD` | 은행코드, 상품코드 |
| 구분코드 | `_DV_CD` | `VARCHAR2(4)` | `TRN_DV_CD` | 거래구분코드 |
| 상태코드 | `_STTS_CD` | `VARCHAR2(4)` | `ACNT_STTS_CD` | 계좌상태코드 |
| 명칭 | `_NM` | `VARCHAR2(100)` | `CUST_NM`, `BRNCH_NM` | 고객명, 지점명 |
| 내용/비고 | `_CN` / `_RMK` | `VARCHAR2(1000)` | `TRN_CN`, `RMK_CN` | 거래적요, 비고내용 |
| 여부 | `_YN` | `CHAR(1)` | `USE_YN`, `DEL_YN` | `'Y'` 또는 `'N'` 고정 |
| 일자 | `_DT` | `VARCHAR2(8)` | `OPEN_DT`, `BASE_DT` | `YYYYMMDD` |
| 시각 | `_TM` | `VARCHAR2(6)` | `TRN_TM` | `HH24MISS` |
| 일시 | `_DTM` | `VARCHAR2(14)` | `FRST_REG_DTM` | `YYYYMMDDHH24MISS` |
| 원화금액 | `_AMT` | `NUMBER(18, 0)` | `TRN_AMT`, `BAL_AMT` | 거래금액, 잔액 |
| 외화금액 | `_FAMT` | `NUMBER(18, 2)` | `EXCH_FAMT` | 소수점 2자리 포함 |
| 비율/금리 | `_RT` | `NUMBER(10, 6)` | `INTR_RT`, `TAX_RT` | 적용금리, 세율 |
| 건수/수량 | `_CNT` / `_QTY` | `NUMBER(10)` | `TRN_CNT`, `STCK_QTY` | 거래건수, 주식수량 |

- 같은 의미의 컬럼은 **모든 테이블에서 같은 이름·같은 도메인**을 사용한다.

## 3. 필수 감사(Audit) 공통 컬럼
모든 테이블의 **최하단**에 내부통제 및 감사 대응을 위해 아래 6개 컬럼을 필수로 배치한다.
```sql
FRST_REG_EMP_ID    VARCHAR2(20)    NOT NULL, -- 최초등록직원ID
FRST_REG_DTM       VARCHAR2(14)    NOT NULL, -- 최초등록일시 (YYYYMMDDHH24MISS)
FRST_REG_PGM_ID    VARCHAR2(30)    NOT NULL, -- 최초등록프로그램ID (화면/배치ID)
LAST_MDFCN_EMP_ID  VARCHAR2(20)    NOT NULL, -- 최종수정직원ID
LAST_MDFCN_DTM     VARCHAR2(14)    NOT NULL, -- 최종수정일시 (YYYYMMDDHH24MISS)
LAST_MDFCN_PGM_ID  VARCHAR2(30)    NOT NULL  -- 최종수정프로그램ID (화면/배치ID)
```
- `*_PGM_ID` 에는 02번 6장의 **프로그램 ID(접두부 9자, 예: `FRISB0001`)** 를 기록한다. (화면/배치 ID 포함)

## 4. 업무코드 참고 사례 (은행 도메인)
참고용 사례이다. 본 템플릿의 DB 업무구분은 5.3 **기능코드(2자리)** 를 사용하므로 프로젝트에서 이 표를 기능코드로 대응시켜 정의한다.

| 업무코드 | 업무명 | 상세 설명 |
|---|---|---|
| COM | 공통 | 공통코드, 권한, 메뉴, 사용자, 배치관리 |
| CST | 고객 | 고객기본, KYC, 신용정보, 고객등급 |
| DEP | 수신 | 요구불, 정기예금, 적금, 입출금 원장 |
| LON | 여신 | 대출신청, 심사, 약정, 실행, 상환, 연체 |
| CRD | 카드 | 카드발급, 승인, 매입, 청구, 한도 |
| FEX | 외환 | 환율, 외화예금, 해외송금, 수출입 |
| TRN | 거래/계정 | 계정계 공통거래, 분개, 시재, 마감 |
| EAI | 대외/채널 | 대외계(FEP), EAI 인터페이스, 전문송수신 |
| BAT | 배치 | 일/월/년 마감 배치, 정산 작업 |

## 변경이력
| 버전 | 일자 | 작성자 | 내용 |
|---|---|---|---|
| 0.1 | | | 최초 작성 (금융권 SI Oracle 표준 반영) |
