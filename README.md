# Translation Harness Builder

**번역·현지화 프로젝트의 문서형 지식 하네스를 구축하고 운영하는 Agent Skill.** 하나의 GitHub 저장소에서 **Codex(플러그인)**, **Claude Code(플러그인)**, **Gemini CLI(확장 기능)**로 배포할 수 있습니다. 별도의 공식 디렉터리 등록, MCP 서버, Python 실행 스크립트가 필요하지 않습니다.

이 저장소에는 **Translation Harness Builder Skill v4.3**의 원본 지침과, 프로젝트에서 선택적으로 사용하는 **27개 Markdown 문서 템플릿**이 함께 들어 있습니다. Skill의 지침은 한국어이며 세 플랫폼 모두 같은 `SKILL.md`와 7개의 상세 설계 문서를 사용합니다.

## 어떤 작업을 하나요?

프로젝트의 실제 원문·번역문·가이드·용어집·Rule 등을 조사해 `translation-harness/` 문서 계층을 생성하거나 보완합니다. 인물별·상대별 화법, 서사와 정보 공개 시점, 번역 용어와 승인 상태, 원문 근거, 기술 제약, QA 및 변경 이력을 구조화하고, 번역 작업 시 관련 문서를 읽도록 프로젝트 지침을 연결합니다.

- **원본 근거 우선**: 소스가 확인되지 않으면 임의의 사실·승인·검증 결과를 만들지 않습니다.
- **기존 작업 보존**: 이미 있는 하네스 문서와 승인 기록을 재사용·보완하고 함부로 덮어쓰지 않습니다.
- **조건부 상세 자산**: 캐릭터·스토리·분기·자막 등은 프로젝트에 해당할 때만 사용합니다.
- **문서 구조까지 정의**: 상위 라우팅, 개별 상세 문서의 목차·표·필드, 근거 기록 및 QA 기준을 포함합니다.

## 설치

아래 예시의 `OWNER/REPO`를 **GitHub에 업로드한 실제 계정/저장소**로 바꿔 실행하세요. 저장소를 추가하는 동작과 Skill/Plugin을 설치하는 동작은 구분됩니다. 클라이언트 버전·조직 정책에 따라 일부 기능이 제한될 수 있습니다.

### Codex CLI / 지원되는 ChatGPT 데스크톱 환경

```bash
codex plugin marketplace add OWNER/REPO
codex plugin add translation-harness-builder@translation-harness-marketplace
```

설치한 후 새 Codex 세션을 시작하세요. 데스크톱 클라이언트에서는 **Plugins → Add Marketplace**로 GitHub 저장소를 등록한 다음 `Translation Harness Builder`를 선택해 설치할 수도 있습니다.

확인: `codex plugin marketplace list`. 플러그인 목록에서도 `translation-harness-builder`를 확인하세요.

### Claude Code

```bash
claude plugin marketplace add OWNER/REPO
claude plugin install translation-harness-builder@translation-harness-marketplace
```

Claude Code에서는 `/plugin`에서 설치 상태를 확인할 수 있습니다. 설치 후 프로젝트를 열고 `/translation-harness-builder:translation-harness-builder`로 Skill을 명시적으로 실행하거나 일반적인 한국어 요청으로 호출할 수 있습니다.

### Gemini CLI

```bash
gemini extensions install https://github.com/OWNER/REPO
```

Gemini CLI에서 `/extensions list`와 `/skills list`로 설치 및 Skill 인식을 확인하세요. 필요하면 Gemini CLI 세션을 재시작하세요. 갱신은 `gemini extensions update translation-harness-builder`로 수행합니다.

> **호환 범위**: 위 명령은 **Codex**, **Claude Code**, **Gemini CLI**의 설치 모델을 기준으로 합니다. 이 세 도구 이외의 모든 Claude/Gemini 웹 채팅 제품에서 GitHub URL만으로 동일하게 설치된다는 뜻은 아닙니다.

## 사용 예시

프로젝트 루트에서 해당 에이전트를 실행하고 다음처럼 요청합니다.

> 이 프로젝트의 번역·현지화 자료를 조사해 translation-harness를 구축해줘. 실제 원문에서 확인한 사실만 작성하고, 문서별 상세 구조와 링크를 연결해줘. 기존 프로젝트 Rule은 보존하면서 번역 작업 전 하네스 문서를 읽도록 설정하고, 조사되지 않은 부분은 미확정으로 남겨줘.

이미 `translation-harness/`가 있다면 그 안의 문서와 내용을 확인하고 보완합니다. 폴더나 파일이 없다면 Skill의 상세 설계 규격에 따라 필요한 구조를 생성합니다. 작업 경로에 대한 읽기·쓰기 권한은 에이전트가 실행되는 환경에서 제공되어야 합니다.

## 문서 템플릿 (선택 사항)

[`templates/translation-harness/`](templates/translation-harness/README.md)에는 27개의 Markdown 골격이 들어 있습니다. 미리 준비된 폴더를 사용하려면 해당 디렉터리를 **작업 프로젝트의 루트**에 복사하세요.

```text
YOUR_PROJECT/
├── (프로젝트 원문 및 작업 파일)
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
```

템플릿을 **미리 복사하지 않아도** Skill이 자체 설계 명세에 따라 문서 구조를 구축할 수 있습니다. 템플릿은 프로젝트의 사실·승인 결정이 채워져 있지 않은 **작성용 골격**입니다. 플러그인 또는 확장 기능 설치 자체가 프로젝트에 템플릿 파일을 자동으로 복사하지는 않습니다.

> `AGENTS.md` 등 프로젝트 Rule은 하네스 폴더 안이 아닌 **작업 프로젝트 수준**에 해당합니다. Skill은 현재 사용 중인 에이전트·IDE의 규칙 파일을 확인하고 기존 내용을 보존하며 연동하도록 설계되어 있습니다.

## 저장소 구조

```text
.
├── README.md                       # 배포 및 사용 안내
├── plugin.json                     # 포터블 Agent Plugins 매니페스트 (Codex)
├── gemini-extension.json           # Gemini CLI 확장 매니페스트
├── .agents/plugins/marketplace.json # Codex 마켓플레이스
├── .codex-plugin/plugin.json       # Codex 호환 매니페스트
├── .claude-plugin/
│   ├── plugin.json                 # Claude Code 플러그인 매니페스트
│   └── marketplace.json            # Claude Code 마켓플레이스
├── skills/translation-harness-builder/
│   ├── SKILL.md                    # v4.3 원본 지침
│   ├── agents/openai.yaml
│   └── references/                 # 7개 상세 설계 문서
└── templates/translation-harness/  # 선택용 Markdown 템플릿 27개
```

하나의 `skills/translation-harness-builder/SKILL.md`가 세 환경에서 공유됩니다. 플랫폼별 파일은 **설치·검색을 위한 메타데이터**이며, 각 플랫폼용 Skill 본문을 따로 관리하지 않습니다.
