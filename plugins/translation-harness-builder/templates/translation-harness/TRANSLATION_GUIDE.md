# Translation Guide — 작업별 문서 탐색

> 문서 역할: 현재 번역 단위에 필요한 정책·지식·근거 문서를 정확하게 찾는 라우터  
> 적용 범위: 모든 번역·현지화·교정·번역 QA  
> 문서 상태: SKELETON  
> 기준 근거: `UNKNOWN` (원본 조사 후 기록)  
> 최종 갱신: 미기록

## 0. 이 문서의 한계
이 문서는 **경로와 판단 순서**만 제공한다. 인물의 실제 말투, 확정 용어, 장면의 사실을 여기서 복제하거나 확정하지 않는다.

## 1. 공통 필독 경로
1. [진입점](README.md)과 이 문서를 읽는다.
2. [실행](guides/01_EXECUTION.md), [문체](guides/04_TARGET_STYLE.md), [용어](guides/05_TERMS_AND_NAMES.md), [QA](guides/07_QA_APPROVAL.md) 정책을 현재 단위에 맞게 확인한다.
3. 아래 표에서 **활성화된 모듈만** 선택하고, 인덱스를 거쳐 **해당 상세 절**까지 읽는다.
4. 원본 위치/버전과 번역 결정의 상태를 [SOURCES](operations/SOURCES.md), [DECISIONS](operations/DECISIONS.md)에서 확인한다.

## 2. 작업별 상세 문서 로드 표
| 현재 작업/검출 조건 | 공통 가이드 | 상세 탐색 경로 | 정보 없을 때 |
|---|---|---|---|
| 일반 번역·교정 | [실행](guides/01_EXECUTION.md), [문체](guides/04_TARGET_STYLE.md) | [용어집](glossary/GLOSSARY.md), 관련 원본 | 필요한 의미·언어 정보 보류 |
| 용어·이름 결정 | [용어 정책](guides/05_TERMS_AND_NAMES.md) | [용어집](glossary/GLOSSARY.md)·[결정 기록](operations/DECISIONS.md) | 미확정 항목으로 기록 |
| 화자·대사·관계 (활성화 시) | [화법 정책](guides/02_DIALOGUE_VOICE.md) | [인물 인덱스](characters/CHARACTER_BIBLE.md) → 해당 `profiles/` 상세 절 | 화자/상대 모호하면 관계별 확정 보류 |
| 장면·서사·분기 (활성화 시) | [서사 정책](guides/03_NARRATION_STORY.md) | [스토리 인덱스](story/STORY_BIBLE.md) → 해당 `arcs/`·[타임라인](story/TIMELINE_AND_REVEALS.md) | 정보 공개·순서 추측 금지 |
| UI·기술 제약 (활성화 시) | [기술 정책](guides/06_FORMAT_AND_TECH.md) | [UI 맥락](media/UI_CONTEXT.md) · [도메인](knowledge/DOMAIN_BIBLE.md) | 변수·표시 제약 불명 시 기술 검토 |
| 자막 (활성화 시) | [기술 정책](guides/06_FORMAT_AND_TECH.md) | [자막 제약](media/SUBTITLE_CONSTRAINTS.md) | 타임코드 등 원본 보호 |
| QA·충돌·승인 | [QA 정책](guides/07_QA_APPROVAL.md) | [이슈](operations/ISSUES.md) · [결정](operations/DECISIONS.md) · [QA 로그](operations/QA_LOG.md) | 검수 상태를 승인으로 오인 금지 |

## 3. 판단 우선순위
원본의 변경 불가 요소·실제 장면/화면 맥락 → 승인된 적용 범위 내의 결정 → 관련 상세 지식과 용어 → 공통 문체 후보의 순서로 확인한다. 충돌이 있으면 해당 범위의 결정을 보류하고 [이슈](operations/ISSUES.md)에 기록한다.

## 4. 중단·보류 조건
- 원문 누락, 출처 ID 불명, 화자·상대·시점 확인 실패로 의미가 달라질 때
- 승인 필요 용어가 미확정일 때, 보호 태그·변수·타임코드가 손상될 위험이 있을 때
- 해당 문서 본문이 누락되거나 서로 상충할 때

## 5. 기록과 갱신
사용한 원본 ID, 읽은 실제 문서 경로/절, 적용한 용어·결정 ID, 미해결 사항을 단위 작업 결과에 남긴다. 새 정보가 생기면 상위 인덱스와 관련 상세 문서를 함께 갱신한다.
