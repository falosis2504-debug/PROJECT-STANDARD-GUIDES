# 02-2. 표준 용어/약어 사전

- 상태: **확정** | 버전: 1.0
- 상위 문서: [02-naming-convention.md](02-naming-convention.md) 3장

## 사용 규칙
- DB 객체명·컬럼명은 이 사전에 등록된 **영문 약어만 조합**한다. 임의의 축약어 사용 금지.
- 사전에 없는 단어는 프로젝트의 표준 관리자(00-governance)에게 등록 요청 후 사용한다.
- 프로젝트 고유 단어는 맨 아래 **[D] 프로젝트 추가**에 등록한다. (✏️ 가변)
- 비고의 "예약어 회피"는 Oracle 예약어와 충돌을 피하려고 정한 약어이다.

## [A] 공통 / 시스템 / 일반
| 한글명 | 영문 약어 | 영문 풀네임 | 비고 |
|---|---|---|---|
| 관리 | MNG | Management | |
| 권한 | AUTH | Authority | |
| 구분 | DV | Division | |
| 그룹 | GRP | Group | 예약어 회피 |
| 기준 | BASE | Base | |
| 내용 | CN | Contents | |
| 단계 | STEP | Step | |
| 대상 | TRGT | Target | |
| 데이터 | DATA | Data | |
| 등록 | REG | Registration | |
| 로그 | LOG | Log | |
| 만료 | EXPR | Expiration | |
| 메뉴 | MENU | Menu | |
| 명칭 | NM | Name | |
| 목록 | LIST | List | |
| 번호 | NO | Number | 예약어 회피 |
| 변경 | CHG | Change | |
| 비고 | RMK | Remark | |
| 사용자 | USR | User | 예약어 회피 |
| 사용 | USE | Use | |
| 삭제 | DEL | Delete | |
| 상세 | DTL | Detail | |
| 상태 | STTS | Status | |
| 생성 | CRT | Create | |
| 설명 | DESC | Description | 예약어 회피 |
| 설정 | SET | Setting | |
| 수정 | MDFCN | Modification | |
| 순번 | SEQ | Sequence | |
| 승인 | APRV | Approval | |
| 시작 | STRT | Start | |
| 시스템 | SYS | System | |
| 에러/오류 | ERR | Error | |
| 여부 | YN | Yes/No | |
| 연결 | LINK | Link | |
| 요청 | REQ | Request | |
| 유형 | TYPE | Type | |
| 이력 | HIST | History | |
| 응답 | RES | Response | |
| 일시 | DTM | Date Time | |
| 일자 | DT | Date | 예약어 회피 |
| 임시 | TEMP | Temporary | |
| 저장 | SAVE | Save | |
| 적용 | APLY | Apply | |
| 전문 | TLGM | Telegram | 대외/채널 전문 |
| 정보 | INFO | Information | |
| 종료 | END | End | |
| 조회 | INQ | Inquiry | |
| 주소 | ADDR | Address | |
| 처리 | PROC | Process | |
| 최초 | FRST | First | |
| 최종 | LAST | Last | |
| 코드 | CD | Code | |
| 통계 | STAT | Statistics | |
| 파일 | FILE | File | |
| 프로그램 | PGM | Program | |
| 화면 | SCRN | Screen | |
| 확인 | CNFM | Confirmation | |

## [B] 고객 / 조직 / 상품
| 한글명 | 영문 약어 | 영문 풀네임 | 비고 |
|---|---|---|---|
| 개인 | INDV | Individual | |
| 고객 | CUST | Customer | |
| 기업/법인 | CORP | Corporation | |
| 등급 | GRD | Grade | |
| 부서 | DEPT | Department | |
| 상품 | PROD | Product | |
| 실명 | RLNM | Real Name | |
| 연락처 | CTPLC | Contact Place | |
| 은행 | BANK | Bank | |
| 점포/지점 | BRNCH | Branch | |
| 주민/사업자 | BZNO | Business Number | |
| 직원/행원 | EMP | Employee | |
| 채널 | CHNL | Channel | |

## [C] 수신 / 여신 / 거래 / 회계
| 한글명 | 영문 약어 | 영문 풀네임 | 비고 |
|---|---|---|---|
| 가산 | ADD | Addition | 가산금리 등 |
| 감면 | RDCN | Reduction | |
| 개설 | OPEN | Open | |
| 거래 | TRN | Transaction | |
| 건수 | CNT | Count | |
| 결제 | STLM | Settlement | |
| 계약 | CNTR | Contract | |
| 계좌 | ACNT | Account | 예약어 회피 |
| 금리/이율 | INTR | Interest Rate | |
| 금액 | AMT | Amount | |
| 납입 | PAY | Payment | |
| 대출 | LOAN | Loan | |
| 만기 | MTRT | Maturity | |
| 발생 | OCCR | Occurrence | |
| 비율/율 | RT | Rate | |
| 상환 | REPAY | Repayment | |
| 세금 | TAX | Tax | |
| 수수료 | FEE | Fee | |
| 실행 | EXEC | Execution | |
| 약정 | AGRM | Agreement | |
| 연체 | OVDU | Overdue | |
| 원금 | PRNC | Principal | |
| 이자 | INT | Interest | |
| 입금 | DPST | Deposit | |
| 잔액 | BAL | Balance | |
| 적요 | SMRY | Summary | |
| 정산 | CLCL | Calculation | |
| 출금 | WDRW | Withdrawal | |
| 취소 | CNCL | Cancel | |
| 통화 | CRNCY | Currency | KRW, USD 등 |
| 한도 | LMT | Limit | |
| 해지 | TRMN | Termination | |
| 환율 | EXRT | Exchange Rate | |

## [D] 프로젝트 추가 ✏️
프로젝트 업무 분석 후 추가 단어를 등록한다. (아래는 샘플 프로젝트 예시, 등록 시 중복·예약어 여부 확인)
| 한글명 | 영문 약어 | 영문 풀네임 | 비고 |
|---|---|---|---|
| 전략 | STRTG | Strategy | 예시 |
| | | | |

## 변경이력
| 버전 | 일자 | 작성자 | 내용 |
|---|---|---|---|
| 0.1 | | | 최초 작성 (금융권 표준단어 약어 사전 반영) |
| 1.0 | | | **확정**. 잔여 `[결정 필요]`(프로젝트별·기술 확정 후 항목)는 해당 시점에 MINOR 개정으로 반영 |
