---
name: translation-harness-builder
description: 프로젝트의 원문·스크립트·번역 자료를 실제로 조사하여 계층형 translation-harness를 구축하고 실내용 번역 지식까지 작성·검증한다. 원본 코퍼스의 전체 접근 가능 범위를 확인하고 장면·화자·관계·시점·분기·용어·UI/기술 제약을 분석해 근거와 적용 조건이 있는 가이드, 용어집, 인물·서사·도메인 상세 문서를 채운다. 대규모 자료를 배치별로 처리하며 미완료를 기록하고, 복수 프로젝트의 하네스를 격리하고, 번역 전 필독 Rule을 연결한다. 새 하네스 구축, 기존 템플릿 내용 채우기, 프로젝트별 분리, 원문 반영 보강·유지보수, 하네스 완성도 점검에 사용한다.
---

# Translation Harness Builder

## 산출물

프로젝트의 **실제 원문에 근거한 번역 판단 지식**을 `translation-harness/` 또는 프로젝트에서 지정한 하네스 경로에 구축한다. 문서 생성만이 아니라 내용 작성, 근거·반례 대조, 링크·Rule 연결, 누락 검증까지 수행한다.

하네스의 산출물은 다음과 같다.

- `README.md`와 `TRANSLATION_GUIDE.md`: 대상 범위, 전체 문서 지도, 번역 작업별 상세 문서 탐색 경로.
- `PROMPT_TEMPLATE.md`, `guides/`: 번역 작업 입출력 계약, 원문 형식, 문체·용어·대사·서사·기술 제약, 검수 정책.
- `glossary/`, 해당되는 `characters/`, `story/`, `knowledge/`, `media/`: 원문에서 실제 확인한 프로젝트 지식과 번역 선택·사용 조건·반례·근거가 들어 있는 상세 문서.
- `operations/`: 소스 및 처리 범위, 결정, 미확정, QA, 변경·재개 기록.
- `AGENTS.md` 또는 실제 사용하는 에이전트 Rule: 번역 전에 **해당 프로젝트** 하네스의 상위·관련 상세 본문을 읽도록 안내.

**기본 요청 범위:** 사용자가 하네스 구축·초안 완성을 요청하고 원문에 접근할 수 있다면 **실제 내용까지 작성**한다. 사용자가 명시적으로 폴더 골격만 요구한 경우에만 구조 작성으로 끝낸다. 템플릿이 이미 있으면 같은 폴더·문서에 내용을 채우고 누락만 보완한다. 원문이 없거나 접근 불가한 경우에는 양식·작업 규격을 구축하되 실제 분석을 수행한 것처럼 표시하지 않는다.

## 실행 순서

### 1. 작업 대상과 소스 범위 지정

1. 프로젝트 루트, 실제 번역 대상, 언어쌍·로캘, 원본 버전, 기존 번역·지침·승인 기록, 사용 에이전트와 프로젝트 Rule을 조사한다. 확인되지 않은 값은 추측하지 않는다.
2. 같은 작업 공간에 복수 작품·게임·제품·로캘이 있으면 [workspace-scoping.md](references/workspace-scoping.md)에 따라 **대상별 `scope_id`, 소유 소스, 쓰기 대상 하네스 루트**를 지정한다. 대상별 규칙·사실·출처·승인을 섞지 않는다.
3. 현재 `translation-harness/`(또는 운영 중인 지정 경로)의 **실제 파일 본문**을 읽는다. 기존 목차·문서·승인·사용자 편집분을 보존하고, 의미가 같은 구조를 중복 생성하지 않는다.
4. 소스 폴더와 관련 자료의 목록을 발견·분류하고, 접근 가능한 전체 조사 범위와 미확인·제외 근거를 확정한다. [corpus-ingestion.md](references/corpus-ingestion.md)와 `operations/SOURCES.md`를 사용한다.

### 2. 필수 구조와 조사 원장 준비

1. [architecture.md](references/architecture.md)의 계층과 [authoring-blueprints.md](references/authoring-blueprints.md), [domain-knowledge-blueprints.md](references/domain-knowledge-blueprints.md), [evidence-and-governance.md](references/evidence-and-governance.md)의 문서별 실제 섹션·표 규격을 적용한다.
2. README, 라우터, 번역 단위 계약, 공통 실행·목표 문체·용어·QA 가이드, 용어집, 운영 기록을 보장한다. 대사·서사·전문 분야·UI·자막 계층은 프로젝트 자료에 해당할 때 구성한다. 인물·루트·문서 개수를 미리 고정하지 않는다.
3. 원본이 많거나 작업을 여러 회에 나누어야 하면 `operations/WORK_LEDGER.md` 등 재개 가능한 원장을 만들고 **원본별 발견·본문 읽기·문맥 분석·문서 반영·검증 상태**를 별도로 기록한다. [coverage-and-resumption.md](references/coverage-and-resumption.md)를 따른다.
4. 이미 작성된 문서나 전달된 폴더 골격은 현재 하네스의 실제 작성 틀로 이용한다. 빈 항목을 완료로 처리하지 않고 해당 문서의 필수 정보를 채운다.

### 3. 원문 전체 조사와 문맥 복원

[corpus-ingestion.md](references/corpus-ingestion.md)의 절차를 적용한다.

1. 접근 가능한 번역 대상 원본을 **실제로 열어 읽는다**. 파일·행·키·화자 ID 목록이나 일부 표본만 추출한 것은 원문 분석이 아니다.
2. 자료 형식에 맞춰 텍스트 단위와 주변 맥락을 복원한다. 스크립트는 화자/수신자 상태, 선택지, 분기·점프, 이벤트·변수와 장면 흐름을, UI는 기능·화면 상태를, 영상은 cue·타임코드 등을 확인한다.
3. 파일·장면·기능 단위로 작업을 나누되, 각 단위를 실제로 읽고 중요한 인물·관계·사건·정보 공개·명칭·표기·기술 제약을 추출한다.
4. 여러 장면에 걸쳐 반복·변화하는 대상은 **전체 출현을 비교**한다. 단순 연속 행이나 파일명 정렬로 인과·화자·시점·관계를 확정하지 않는다.
5. 대량 자료는 배치별로 처리하고 완료 범위와 다음 재개 지점을 원장에 저장한다. 처리하지 못한 원본은 `NOT_READ` 또는 `BLOCKED`로 구체적인 이유와 함께 남긴다.

### 4. 실제 번역 지식 집필

[semantic-population.md](references/semantic-population.md)에 따라 **조사·추출 → 비교·해석 → 적용 조건/반례 확인 → 문서 작성 → 원문 재대조**를 수행한다.

1. 각 정보 항목을 `scope/source/unit ID → 직접 관찰 → 앞뒤 문맥·대조 → 번역상의 의미 → 목표어 후보 또는 처리 지침 → 적용/금지 조건 → 상태`로 연결한다.
2. 공통 `guides/`에는 해당 프로젝트 원문의 실제 특성, 원문 포맷과 보호 요소, 목표 문체·용어·대사·서사·QA 정책을 **판단 가능한 문장**으로 집필한다. 일반적인 조언만 나열하지 않는다.
3. `glossary/`에는 실제 용어·이형 표기·지칭 대상·번역 후보·적용/예외·출처를 등록한다. 무조건적인 전역 치환을 유도하지 않는다.
4. 대사 프로젝트라면 실제 확인된 인물을 인덱스에 등록하고 상세 카드에 **화자→수신자 방향, 관계 단계·시점, 호칭·말투, 변화 계기, 실제 대사 근거와 목표어 표현**을 작성한다.
5. 서사 프로젝트라면 실제 파일과 논리 장면을 매핑하고 **사건의 인과관계, 분기 조건, 화자별 지식 상태, 정보 공개 시점, 번역상 주의점**을 상세 카드에 작성한다. 문자열·선택지 목록만으로 끝내지 않는다.
6. 제품·전문 분야·UI·자막 프로젝트라면 실제 개념의 관계와 기능·상태, 화면/타임코드 맥락, 기술·표기 제약을 작성한다.
7. 실제 사례를 근거로 유효한 번역 초안을 제안할 수 있으면 `DRAFT`로 작성한다. 원문 사실·추론·승인·실행 검증은 서로 혼동하지 않는다. 확인할 수 없는 사실은 꾸며내지 않는다.
8. 모든 신규 상세 문서를 상위 인덱스에 연결하고, 중앙 라우터에서 **언제 어떤 상세 문서를 열어야 하는지** 실제 경로로 안내한다.

**조사표와 실내용 문서의 차이:** 원문 ID/화자/행 수를 전부 기록해도 인물의 상대별 화법, 장면별 정보 공개, 용어의 지칭 개념과 적용 조건, 실제 번역 예외가 비어 있으면 작성이 끝난 것이 아니다. 번역 담당자가 실제 원문 단위에서 참조·적용할 수 있는 **구체적 규칙과 근거**까지 작성한다.

### 5. 조사 범위와 내용 반영 대조

[coverage-and-resumption.md](references/coverage-and-resumption.md)와 [quality-and-acceptance.md](references/quality-and-acceptance.md)를 읽고 대상 프로젝트별로 검사한다.

- **소스:** 발견한 전체 조사 범위 대비 실제로 읽은 파일/문맥/단위, 미독·차단·제외 사유를 대조한다.
- **의미:** 원문에서 확인한 주요 인물·방향별 관계·사건/장면·분기·용어·개념·화면/기능이 실제 상세 문서·절에 반영됐는지 대조한다.
- **실용성:** 상세 문서가 실제 번역 판단, 적용 조건, 반례, 원본 출처, 미확정 상태를 설명하는지 확인한다.
- **정확성:** 일부 기록을 원문에 다시 대조하고 반례·시점·화자·적용 범위·프로젝트 혼입을 검사한다.
- **무손실:** 원본 파일·기존 승인 문서·타 대상 하네스를 임의로 덮어쓰지 않았는지 확인한다.

조사와 집필이 끝나지 않았다면 `POPULATING`으로 기록하고 가능한 범위까지 실제 문서를 채운 후 **정확한 미완료 소스 및 다음 작업 지점**을 남긴다. 스캐폴드만 완성했거나 일부 문자열을 예시로 넣었을 때 `DRAFT_CONTENT_COMPLETE`라고 보고하지 않는다.

### 6. 번역 사전 읽기 Rule 연결

[rule-integration.md](references/rule-integration.md)의 절차를 적용한다.

1. 프로젝트가 실제로 사용 중인 `AGENTS.md`, `CLAUDE.md` 또는 에이전트 Rule을 읽고 기존 내용은 유지한다.
2. 번역·교정·QA 수행 전에 **대상 프로젝트에 맞는** README와 TRANSLATION_GUIDE 및 현재 원문 단위에 관련된 상세 문서의 본문·앵커를 실제로 열도록 연결한다.
3. Rule과 인덱스의 경로, 상위→상세→원문 근거의 연결을 검사한다. 실제 자동 로딩이 확인되지 않았다면 검증됐다고 주장하지 않는다.

### 7. 결과 보고 및 갱신

작업 대상별로 실제 작성한 정책·인물·서사·용어·기술 지식의 **구체적인 내용**, 대응하는 원본 범위, 조사·반영 완료/미완료, 검증 증거, 다음 배치와 재개 지점, Rule 변경을 보고한다. 구조·링크 개수만 성과로 제시하지 않는다.

상태는 `SCAFFOLD_ONLY / POPULATING / DRAFT_CONTENT_COMPLETE / REVIEWED / RUNTIME_VERIFIED`를 구분한다. 사람이 승인하지 않은 번역 초안은 승인된 정책으로 표시하지 않는다. 새 소스나 버전이 오면 관련 지식 및 번역 결과의 영향 범위를 추적하고 갱신한다.

## 참조 자료

| 자료 | 필수 열람 시점과 내용 |
|---|---|
| [workspace-scoping.md](references/workspace-scoping.md) | 복수 프로젝트/로캘을 처리할 때 소스·하네스 격리와 Rule 라우팅 |
| [corpus-ingestion.md](references/corpus-ingestion.md) | 원본 탐색·형식별 실제 읽기·문맥/분기 복원·대량 처리 |
| [semantic-population.md](references/semantic-population.md) | 출처에서 실용적인 화법·서사·용어·매체 판단 지식을 집필하는 방법 |
| [coverage-and-resumption.md](references/coverage-and-resumption.md) | 원본 대조·의미 커버리지·진행 원장·미완료 재개·완료 판정 |
| [architecture.md](references/architecture.md) | 문서 트리, 계층 책임, 생성 조건, 중복·링크 방지 |
| [authoring-blueprints.md](references/authoring-blueprints.md) | 최상위 문서와 공통 가이드의 목차·표·필드·작성 기준 |
| [domain-knowledge-blueprints.md](references/domain-knowledge-blueprints.md) | 용어·인물·서사·도메인·UI·자막의 실제 상세 문서 계약 |
| [evidence-and-governance.md](references/evidence-and-governance.md) | 근거·추론·번역안·승인·QA·변경 기록 및 상태 구분 |
| [population-and-maintenance.md](references/population-and-maintenance.md) | 내용 집필·교차 참조·변경 영향·문서 보존 |
| [rule-integration.md](references/rule-integration.md) | Rule 적용과 실제 번역 전 문서 열람 |
| [quality-and-acceptance.md](references/quality-and-acceptance.md) | 구조, 원문/의미 반영, 언어 검토, 실제 실행 시험의 완료 검증 |
