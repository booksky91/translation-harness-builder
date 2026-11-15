# Translation Harness Builder

**번역·현지화 프로젝트용 문서형 지식 하네스를 구축하고 관리하는 Agent Skill.** GitHub 저장소 하나로 **Codex(Plugin Marketplace)**, **Claude Code(Plugin Marketplace)**, **Gemini CLI(Extension)**에 배포합니다. 

이 저장소에는 Translation Harness Builder **원본 지침**과, 작성 지침이 들어 있는 **27개 Markdown 템플릿**이 있습니다. 프로젝트 원문이 없어도 Skill을 통해 골격을 구성할 수 있고, 템플릿을 미리 복사해서 시작할 수도 있습니다.

## 설치: GitHub 저장소 주소

아래의 `OWNER/REPO`를 실제 GitHub 저장소 주소로 변경하세요. **ZIP을 그대로 GitHub에 업로드하는 것이 아니라, 압축을 해제하고 내용물을 저장소 최상위에 올려야 합니다.** 특히 `.agents/`, `.claude-plugin/`은 이름이 점(`.`)으로 시작하지만 반드시 커밋해야 합니다.

### Codex

```bash
codex plugin marketplace add OWNER/REPO
codex plugin add translation-harness-builder@translation-harness-marketplace
```

`codex plugin marketplace list` 명령으로 마켓플레이스 등록 여부를 확인하세요. 이미 같은 이름으로 등록했다면 파일을 GitHub에 푸시한 뒤 `codex plugin marketplace upgrade translation-harness-marketplace`로 갱신하세요. 필요하다면 등록된 마켓플레이스를 제거한 후 다시 추가할 수 있습니다.

### Claude Code

```bash
claude plugin marketplace add OWNER/REPO
claude plugin install translation-harness-builder@translation-harness-marketplace
```

확인: `claude plugin list`. 스킬 실행 예시: `/translation-harness-builder:translation-harness-builder` (설치된 플러그인의 Skill 이름으로 호출).

### Gemini CLI

```bash
gemini extensions install https://github.com/OWNER/REPO
```

확인: `gemini extensions list` 및 대화 중 `/skills list`. Gemini CLI는 확장 루트의 `skills/` 디렉터리에서 동일한 v4.3 Skill을 인식합니다.

> 이 배포 방식은 Codex CLI/데스크톱, Claude Code, Gemini CLI 기준입니다. 모든 웹 채팅 제품에서 GitHub 주소만으로 설치되는 것은 아닙니다.

## Codex 오류 해결: marketplace root does not contain a supported manifest

Codex는 GitHub의 **저장소 루트**에서 `.agents/plugins/marketplace.json`을 찾습니다. 다음 경로를 브라우저로 열어 확인하세요.

```text
https://github.com/OWNER/REPO/blob/main/.agents/plugins/marketplace.json
```

404 오류가 발생한다면 마켓플레이스를 설치할 수 없습니다. 특히 아래 두 사례를 확인하세요.

- **중첩 폴더:** GitHub 저장소 최상위에 다시 `translation-harness-builder/`라는 폴더가 있고 그 아래 `.agents/`가 들어 있으면 안 됩니다. `.agents/`는 저장소 최상위에 있어야 합니다.
- **숨김 폴더 누락:** `.agents/`나 `.claude-plugin/`을 빼고 업로드한 경우입니다. Git으로 업로드하면 누락을 줄일 수 있습니다.

Git 프로젝트 루트에서 다음 명령으로 실제 추적 파일인지 확인할 수 있습니다.

```bash
git ls-files .agents/plugins/marketplace.json
git ls-files .claude-plugin/marketplace.json
git ls-files plugins/translation-harness-builder/plugin.json
```

세 명령 모두 해당 경로가 출력되어야 합니다. 아무것도 출력되지 않으면 `git add -A`로 추가하고 `git commit` / `git push` 하세요. 브라우저에서 파일을 확인한 다음 Codex에 다시 마켓플레이스를 추가하세요.

Codex 마켓플레이스의 플러그인 원본 경로는 `./plugins/translation-harness-builder`로 설정되어 있습니다. 플러그인 디렉터리 안에 `plugin.json`, `.codex-plugin/plugin.json`, `skills/`가 존재합니다. 상대 경로는 `.agents/plugins/`가 아니라 **저장소 루트**를 기준으로 해석됩니다.

## Skill이 하는 작업

프로젝트의 원본·번역본·기존 지침을 조사해 `translation-harness/` 계층을 생성·보완합니다. 문서에는 번역 실행 절차, 목표 문체, 용어, 인물의 상대별 화법, 서사·시점, 기술 제약, 근거와 승인 상태, QA·변경 기록을 정리합니다. 에이전트 Rule을 변경할 때는 기존 내용을 보존하고 번역 전 하네스 지침을 실제로 읽도록 연결합니다.

프로젝트 루트에서 다음처럼 요청하세요.

> 현재 프로젝트의 번역 자료를 확인하고 translation-harness를 구성해줘. 있는 문서는 보존하고, 부족한 구조와 정보는 Skill의 설계 기준에 따라 작성해줘. 출처를 확인하지 못한 내용은 미확정으로 남기고, 프로젝트 Rule에 필독 문서 경로를 연결해줘.

## 템플릿

`templates/translation-harness/`에 27개 Markdown 문서 골격이 있습니다. 프로젝트 루트에 폴더째 복사하면 됩니다.

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
```

프로젝트 사실이 채워져 있지 않은 작성용 양식입니다. 인물·서사·매체 관련 문서는 해당 프로젝트에 필요할 때 활성화하세요. 플러그인 설치만으로 템플릿이 작업 프로젝트에 자동 복사되지는 않습니다. 설치된 플러그인에도 동일한 템플릿 사본이 포함되어 있습니다.

## 저장소 구조

```text
.
├── README.md
├── .agents/plugins/marketplace.json      # Codex 마켓플레이스 진입점
├── .claude-plugin/marketplace.json       # Claude Code 마켓플레이스 진입점
├── gemini-extension.json                 # Gemini CLI 확장 진입점
├── skills/translation-harness-builder/  # Gemini CLI 확장용 Skill 사본
├── templates/translation-harness/       # 프로젝트에 직접 복사할 문서 양식
└── plugins/translation-harness-builder/  # Codex·Claude 설치 대상
    ├── plugin.json
    ├── .codex-plugin/plugin.json
    ├── .claude-plugin/plugin.json
    ├── skills/translation-harness-builder/
    │   ├── SKILL.md
    │   ├── agents/openai.yaml
    │   └── references/
    └── templates/translation-harness/
```

Codex·Claude는 하위 플러그인의 Skill을 읽고, Gemini는 확장 루트의 Skill을 읽습니다. 세 환경에서 읽는 Skill 본문과 상세 명세는 동일한 **v4.3 원본 내용**입니다. 배포 형식 때문에 저장소에 두 복사본을 넣었으므로 Skill을 갱신할 때 둘 다 똑같이 갱신해야 합니다. (템플릿도 루트와 플러그인 내부의 두 복사본을 함께 관리하세요.)
