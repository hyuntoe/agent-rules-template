# agent-rules-template

AI 에이전트가 프로젝트에서 일관된 방식으로 작업하도록 돕는 규칙 보일러플레이트 저장소입니다. 이 저장소에서 문서와 워크플로우를 개선해 GitHub에 올리고, 다른 프로젝트는 필요한 규칙을 읽어 프로젝트 상황에 맞게 병합해 사용합니다.

## 한 줄 소개

Claude, Codex(GPT), agy(Gemini)가 같은 프로젝트 문맥에서 공통 규칙, docs 워크플로우, 멀티에이전트 협업 규칙을 공유하도록 만드는 템플릿입니다.

## 무엇이 들어 있나

- `karpathy-plus.md`
  - 공통 개발 규칙의 단일 진실 소스입니다.
  - 가정 명시, 단순성 우선, 외과적 수정, 작업별 단일 플랜 파일, 완료 전 테스트 같은 원칙을 정의합니다.
- `workflow-rules.md`
  - `docs/backlog`, `docs/plans`, `docs/history` 사용 규칙을 정의합니다.
  - 단순·비단순 작업의 판정 기준, 활성 플랜과 브랜치 운영, 완료 이력 이동 규칙을 담습니다.
- `multi-agents-orchestration.md`
  - 인터랙티브 세션을 PM 후보로 두고, 필요한 에이전트를 워커로 쓰는 협업 규칙을 정의합니다.
  - 실행 모드에 따른 역할 판정, headless 워커의 단방향 호출, worktree 격리, 핸드오프 기준을 담습니다.
- `local-context-routing.md`
  - 대용량 로그, 긴 단일 파일, 긴 문서를 로컬 Ollama 모델로 먼저 라우팅하는 규칙을 정의합니다.
  - 입력 크기별 경계값, `gemma4:e2b-it-q4_K_M`과 `qwen2.5-coder:3b` 프로파일, Ollama 장애 시 폴백을 담습니다.
- `skill-usage-rules.md`
  - 공통 스킬을 언제 사용하고 Codex CLI, Claude Code CLI, agy CLI에 어디로 배포할지 정의합니다.
- `skills/`
  - Codex CLI, Claude Code CLI, agy CLI에 복제할 공통 스킬 원본입니다.
  - `context-budget-gate`, `local-context-router`, `graphify-code-map`을 둡니다.
- `AGENTS.md`, `CLAUDE.md`
  - 각 에이전트용 진입 파일입니다.
  - 규칙 본문을 중복하지 않고 공통 문서를 가리키는 포인터 역할만 합니다.
- `docs/`
  - 프로젝트별 backlog, 진행 중 플랜, 완료 이력을 저장하는 공간입니다.

## 목표

이 템플릿의 목표는 다음과 같습니다.

- 규칙 문서를 프로젝트별 내용과 분리합니다.
- 여러 에이전트가 같은 작업 기준을 공유하게 합니다.
- 세션 기억이 아니라 저장소 문서를 기준으로 다음 작업을 이어갈 수 있게 합니다.
- 복잡한 작업에서 계획, 구현, 검증, 기록을 분리된 문서 흐름으로 관리하게 합니다.
- 큰 입력을 다룰 때 로컬 라우터로 필요한 원문 조각만 골라 토큰과 외부 전송량을 줄입니다.

## 사용 방법

1. 이 저장소를 새 프로젝트의 시작점으로 복사합니다.
2. 프로젝트 고유 정보는 `README.md`와 `docs/`에만 작성합니다.
3. 공통 규칙을 바꾸고 싶으면 `karpathy-plus.md`, `workflow-rules.md`, `multi-agents-orchestration.md`를 수정합니다.
4. 대용량 입력 처리 규칙을 바꾸고 싶으면 `local-context-routing.md`를 수정합니다.
5. 공통 스킬을 바꾸고 싶으면 `skills/` 원본과 `skill-usage-rules.md`를 수정한 뒤 각 CLI 스킬 디렉토리에 복제합니다.
6. 에이전트 진입 파일인 `AGENTS.md`, `CLAUDE.md`는 가능한 한 얇은 포인터로 유지합니다.

## 현재 상태

현재 이 저장소는 실제 애플리케이션 코드베이스가 아니라, 에이전트 작업 규칙을 정리한 보일러플레이트 템플릿입니다. 다음 규칙과 원본 스킬이 준비되어 있습니다.

- Claude, Codex, agy가 공통 SSOT 문서를 읽는 얇은 진입 파일.
- 작업 복잡도 경계값과 `docs/backlog`, `docs/plans`, `docs/history` 생명주기.
- 인터랙티브 PM과 headless 워커의 역할, 격리, 핸드오프 규칙.
- 입력 크기별 로컬 컨텍스트 라우팅과 Ollama 장애 폴백.
- 컨텍스트 예산 점검, 로컬 라우팅, graphify 코드맵 스킬 원본.

현재 활성 플랜은 없으며, 다음 작업은 `docs/backlog/`에, 완료된 규칙 정비 기록은
`docs/history/project/`에 있습니다.

## 다음에 보강하면 좋은 것

- 새 프로젝트를 시작할 때 바로 복사해 쓸 수 있는 예시 `docs/plans/` 파일 추가.
- `README.md`에 프로젝트 초기화 체크리스트 추가.
- WSL에서 Windows Ollama API를 찾는 예시 스크립트 추가.
- 공통 스킬을 세 CLI 스킬 디렉토리에 동기화하는 스크립트 추가.
