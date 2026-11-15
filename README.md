# Translation Harness Builder

**원문을 실제로 분석하여 번역·현지화 하네스를 작성하는 범용 Agent Skill.** 단순 폴더/표 양식 생성에 그치지 않고, 원본 파일의 전체 접근 가능 범위를 읽어 인물의 상대별 화법, 서사·정보 공개, 용어와 예외, UI·매체 제약, 출처가 있는 번역 판단을 프로젝트별 Markdown 문서에 채우도록 지시합니다.

**버전: `0.5.1` (개발 단계).** 복잡한 실제 프로젝트에서 결과 품질을 계속 검증해야 합니다. 원본을 못 읽거나 일부만 분석했다면 완료를 주장하지 않고, 조사 원장에 미완료·재개 지점을 남기도록 설계했습니다.

이 저장소는 GitHub에서 공유할 수 있는 다음 배포 형식을 제공합니다.

| 사용 환경 | 패키지 방식 | 진입 파일 |
|---|---|---|
| OpenAI Codex | Plugin Marketplace | `.agents/plugins/marketplace.json` |
| Claude Code | Plugin Marketplace | `.claude-plugin/marketplace.json` |
| Gemini CLI | Extension | `gemini-extension.json` |

MCP 서버·실행용 Python 코드를 포함하지 않습니다. Skill은 Markdown 작업 지침과 참고 명세이며, 실제 원본 조사와 문서 수정은 Skill을 사용하는 에이전트가 프로젝트 도구로 수행합니다.

## 설치

**이 저장소의 파일을 GitHub 최상위에 업로드**하세요. `.agents/`와 `.claude-plugin/` 디렉터리를 누락하지 마세요.

### Codex

```bash
codex plugin marketplace add booksky91/translation-harness-builder
```

Codex에서 해당 Marketplace의 `translation-harness-builder` 플러그인을 설치합니다. CLI에서 설치 명령이 제공되는 버전이라면 다음을 사용합니다.

```bash
codex plugin add translation-harness-builder@translation-harness-marketplace
```

Marketplace 확인/갱신:

```bash
codex plugin marketplace list
codex plugin marketplace upgrade translation-harness-marketplace
```

Marketplace source is now the Git repository root (not a plugins/ subdirectory). Verify .agents/plugins/marketplace.json and the root plugin.json if installation fails.

### Claude Code

```bash
claude plugin marketplace add booksky91/translation-harness-builder
claude plugin marketplace update translation-harness-marketplace
claude plugin install translation-harness-builder@translation-harness-marketplace
```

설치 확인: `claude plugin list`. Skill 호출 예: `/translation-harness-builder:translation-harness-builder`.

### Gemini CLI

```bash
gemini extensions install https://github.com/booksky91/translation-harness-builder
```

설치 확인: `gemini extensions list`. Gemini CLI는 저장소 최상위 `skills/`의 동일한 Skill을 읽습니다.

> 위 설치 안내는 각 도구의 플러그인·확장 기능을 지원하는 버전 기준입니다. GitHub에 저장소를 만든 것만으로 다른 사용자의 환경에 자동 설치되지는 않습니다.


After an upgrade, confirm the installed version is 0.5.1 and start a new session. An old cache path ending in 4.3.0 indicates a stale installation.

## 사용 방법

원본과 기존 번역이 들어 있는 프로젝트에서 Skill을 호출한 뒤 구체적인 작업 범위를 지시합니다. 아래는 입력 예시이며 **기본 작업은 실제 원본 분석과 상세 문서 작성까지** 포함합니다.

### 단일 프로젝트

> 현재 프로젝트의 원문·스크립트·기존 번역을 조사하여 translation-harness를 완성해줘. 접근 가능한 원본 전체를 실제로 읽고 화자·상대별 말투, 사건·정보 공개 시점, 용어·지칭 개념, 화면·기술 제약을 분석해 상세 문서의 실제 내용을 작성해줘. 조사 범위, 문서 반영 범위, 미완료·검증 상태도 보고해줘.

### 하나의 작업 공간에 여러 독립 프로젝트

> 이 작업 공간에 있는 각 프로젝트의 원본과 출력 범위를 분리해줘. translation-harness 아래에 프로젝트별 하위 폴더를 사용하고, 각 하네스가 자기 원본만 분석하도록 해줘. 해당 프로젝트의 인물·스토리·용어·규칙을 실제 자료에서 조사하고, 서로 다른 프로젝트에 혼입되지 않도록 검증해줘.

### 기존 템플릿을 사용하는 경우

`templates/translation-harness/` 안의 Markdown 골격을 프로젝트에 복사해 시작할 수 있습니다. 템플릿은 필수 입력이 아닙니다. Skill이 해당 프로젝트의 부족한 파일·섹션을 만들고 **기존 틀의 내용도 실제 원본 근거로 채웁니다.** 이미 작성된 원문 근거·승인 정책을 임의로 덮어쓰지 않습니다.

## 실행 절차 및 산출 수준

Skill의 주요 작업 지침은 [SKILL.md](skills/translation-harness-builder/SKILL.md)에 있습니다. 다음 참조 문서가 원본 분석부터 실내용 집필까지 구체적 방법을 정합니다.

| 문서 | 무엇을 수행하는가 |
|---|---|
| [corpus-ingestion.md](skills/translation-harness-builder/references/corpus-ingestion.md) | 원본 인벤토리, 형식별 본문 열람, 장면·화자·분기 복원, 전수 조사 |
| [semantic-population.md](skills/translation-harness-builder/references/semantic-population.md) | 원문을 바탕으로 인물·관계·스토리·용어·UI 판단 지식을 상세 문서에 집필 |
| [coverage-and-resumption.md](skills/translation-harness-builder/references/coverage-and-resumption.md) | 원본 대조·의미 반영 커버리지, 대량 자료 배치 처리, 작업 재개와 완료 판정 |
| [workspace-scoping.md](skills/translation-harness-builder/references/workspace-scoping.md) | 복수 프로젝트의 소스·쓰기 경로·규칙 및 지식 격리 |
| [architecture.md](skills/translation-harness-builder/references/architecture.md) | 문서 계층, 진입점·공통 지침·상세 자산의 책임 |
| [authoring-blueprints.md](skills/translation-harness-builder/references/authoring-blueprints.md) | 최상위 문서와 공통 가이드의 구체적 목차와 작성 규격 |
| [domain-knowledge-blueprints.md](skills/translation-harness-builder/references/domain-knowledge-blueprints.md) | 용어·인물·스토리·전문 지식·매체 문서의 내용 필드 |
| [evidence-and-governance.md](skills/translation-harness-builder/references/evidence-and-governance.md) | 출처, 번역 결정, 검수, 변경 기록과 승인 상태 |
| [population-and-maintenance.md](skills/translation-harness-builder/references/population-and-maintenance.md) | 문서 작성·링크 연결·갱신·무손실 유지 |
| [rule-integration.md](skills/translation-harness-builder/references/rule-integration.md) | 프로젝트 Rule에 번역 전 필독 경로 연결 |
| [quality-and-acceptance.md](skills/translation-harness-builder/references/quality-and-acceptance.md) | 실내용 완료, 근거·언어·실장 검증과 수락 기준 |

### 작업 상태의 차이

- `SCAFFOLD_ONLY`: 폴더·목차·양식만 있고 원문 기반 지식이 없음.
- `POPULATING`: 원본 조사 또는 실제 지식 집필이 진행 중. 미독·미반영 범위가 남음.
- `DRAFT_CONTENT_COMPLETE`: 접근 가능한 전체 작업 범위의 문맥을 분석하고 주요 번역 판단 지식을 상세 문서에 반영한 **실사용 가능한 초안**.
- `REVIEWED`, `RUNTIME_VERIFIED`: 실제 검수/승인 또는 제품·엔진에서의 실행 검증을 수행한 경우에만 사용.

원본 파일 수와 링크 개수만 늘어난 결과는 내용 완성으로 보지 않습니다. `operations/SOURCES.md` 또는 대규모 자료용 `operations/WORK_LEDGER.md`에서 실제 읽은 범위와 작성된 문서의 근거를 확인할 수 있어야 합니다.

## 템플릿

`templates/translation-harness/`에는 최상위 안내, 8종 공통 가이드, 용어집, 인물·스토리 상세 작성 양식, 매체·도메인, 출처·결정·QA·변경 기록과 **원본 조사/문서 반영 진행 원장**의 Markdown 골격이 있습니다. 원본 사실을 미리 넣지 않은 템플릿이며, Skill 실행에 반드시 필요한 것은 아닙니다.

```text
YOUR_PROJECT/
└── translation-harness/
    ├── README.md
    ├── TRANSLATION_GUIDE.md
    ├── PROMPT_TEMPLATE.md
    ├── guides/
    ├── glossary/
    ├── characters/
    ├── story/
    ├── knowledge/
    ├── media/
    └── operations/
        ├── SOURCES.md
        ├── WORK_LEDGER.md
        └── ...
```

프로젝트에 없는 인물·서사·UI·자막 정보를 가공해서 생성하지 마세요. 실제 원문이 있다면 필요한 문서에 근거와 적용 조건을 상세히 작성하세요.

## 저장소 구조

```text
.
|-- README.md
|-- LICENSE
|-- plugin.json                      # Portable plugin manifest, version 0.5.1
|-- .codex-plugin/plugin.json       # Codex compatibility manifest
|-- .claude-plugin/
|   |-- plugin.json                 # Claude Code plugin manifest
|   `-- marketplace.json            # Claude Code marketplace (GitHub source)
|-- .agents/plugins/marketplace.json # Codex marketplace (Git URL source)
|-- gemini-extension.json           # Gemini extension manifest
|-- skills/
|   `-- translation-harness-builder/
|       |-- SKILL.md
|       |-- agents/openai.yaml
|       `-- references/             # 11 reference manuals
`-- templates/translation-harness/ # Optional starter documents
```
