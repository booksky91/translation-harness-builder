# Translation Harness — 프로젝트 진입점

> 문서 역할: 작업자가 하네스의 범위, 읽기 순서, 최신 기준 문서와 미확정 사항을 찾는 첫 화면  
> 적용 범위: 프로젝트 전체  
> 문서 상태: SKELETON  
> 기준 근거: `UNKNOWN` (원본 조사 후 기록)  
> 최종 갱신: 미기록

## 1. 프로젝트 정보
| 항목 | 값 | 확인할 근거 |
|---|---|---|
| 프로젝트 이름/버전 | UNKNOWN | 프로젝트 설정·배포 문서 |
| 원문 언어·로캘 | UNKNOWN | 실제 원문 파일 |
| 목표 언어·로캘 | UNKNOWN | 작업 의뢰·스타일 정책 |
| 매체/콘텐츠 종류 | UNKNOWN | 프로젝트 구조 |
| 원본 범위·제외 범위 | UNKNOWN | [소스 등록부](operations/SOURCES.md) |
| 최종 승인 책임 | UNKNOWN | 프로젝트 운영 규칙 |

## 2. 번역 작업 시작
1. 이 문서와 [중앙 번역 가이드](TRANSLATION_GUIDE.md)를 **본문까지** 읽는다.
2. [작업 입력·출력 계약](PROMPT_TEMPLATE.md) 및 해당 작업의 [실행 가이드](guides/01_EXECUTION.md)를 확인한다.
3. 중앙 가이드의 경로를 따라 해당 원문 단위와 관련된 **실제 상세 문서·절**을 읽는다.
4. [출처](operations/SOURCES.md), [결정](operations/DECISIONS.md), [이슈](operations/ISSUES.md)의 상태를 구분한다.
5. 원문·문서 근거가 없으면 추측해 확정하지 않고 보류한다.

## 3. 문서 지도
| 계층 | 역할 | 시작 문서 |
|---|---|---|
| 진입·작업 라우팅 | 작업 유형별 참조 순서 | [중앙 가이드](TRANSLATION_GUIDE.md) |
| 공통 정책 | 실행/문체/용어/검수 규칙 | [실행](guides/01_EXECUTION.md) · [문체](guides/04_TARGET_STYLE.md) · [용어](guides/05_TERMS_AND_NAMES.md) · [QA](guides/07_QA_APPROVAL.md) |
| 용어 지식 | 실제 표제어·표기·적용 조건 | [용어집](glossary/GLOSSARY.md) |
| 대사/화자 (조건부) | 인물별·상대별 말투 | [인물 인덱스](characters/CHARACTER_BIBLE.md) |
| 스토리 (조건부) | 장면·분기·정보 공개 | [스토리 인덱스](story/STORY_BIBLE.md) |
| 도메인 (조건부) | 전문 개념·제품 기능 | [도메인 인덱스](knowledge/DOMAIN_BIBLE.md) |
| 매체 (조건부) | UI/자막 실장 맥락 | [UI](media/UI_CONTEXT.md) · [자막](media/SUBTITLE_CONSTRAINTS.md) |
| 운영/추적 | 출처·승인·품질·변경 | [운영 기록](operations/CHANGELOG.md) |

## 4. 조건부 모듈 활성 상태
템플릿에 파일이 존재하는 것과 실제 프로젝트에서 사용할 수 있다는 것은 다르다. 자료를 확인한 뒤 다음 상태를 갱신한다.
| 모듈 | 사용 상태 | 확인할 기준 |
|---|---|---|
| 대사·캐릭터 | NOT_ASSESSED | 실제 화자/수신자와 관계별 표현이 존재하는가 |
| 서사·분기 | NOT_ASSESSED | 시점/장면/정보 공개가 번역에 영향을 미치는가 |
| 도메인 지식 | NOT_ASSESSED | 별도 개념·제품 기능 정의가 필요한가 |
| UI | NOT_ASSESSED | 화면·문구 타입·길이/변수 제약이 있는가 |
| 자막 | NOT_ASSESSED | 타임코드·발화자·줄 분할 제약이 있는가 |
| 사례집 | NOT_ASSESSED | 실제 근거 있는 검토 사례가 축적됐는가 |

상태 값: `NOT_ASSESSED` / `ACTIVE` / `NOT_APPLICABLE`. 해당 없는 모듈을 억지로 사용하지 않는다.

## 5. 기록과 보류
- 소스 버전/참조 단위: [SOURCES](operations/SOURCES.md)
- 승인된 번역·정책 결정: [DECISIONS](operations/DECISIONS.md)
- 미확정/충돌: [ISSUES](operations/ISSUES.md)
- 실제 검수와 실장 시험: [QA_LOG](operations/QA_LOG.md)
- 변경 영향: [CHANGELOG](operations/CHANGELOG.md)

## 6. 프로젝트 Rule 연계
프로젝트 루트의 `AGENTS.md` 또는 사용 중인 에이전트 Rule에 번역 전 `translation-harness/README.md` 및 `TRANSLATION_GUIDE.md`의 **실제 본문 열람**과 필요한 상세 문서 조회를 요구하는 규칙을 넣는다. Rule은 하네스 폴더 바깥의 프로젝트 수준에서 관리한다. 기존 Rule을 덮어쓰지 않는다.

## 7. 미확정 사항
| 질문 | 필요한 자료 | 담당/상태 |
|---|---|---|
| 원문 언어·로캘·대상 버전은? | 실제 소스와 작업 요청 | UNKNOWN |
| 최종 문체/표기 승인자는? | 운영 의사결정 | UNKNOWN |
