# 공통 스킬 배포 계획

## Plan

Claude Code CLI 의존도를 줄이고 쿼터를 아끼기 위해, 공통 스킬 원본을 저장소에 두고 Codex CLI, Claude Code CLI, agy CLI의 스킬 디렉토리에 같은 스킬을 설치합니다. 우선 자동 hook보다 안전한 반자동 스킬을 만들고, 에이전트 진입 문서에서 사용하도록 연결합니다.

## Checklist

- [x] 공통 스킬 원본 디렉토리를 만듭니다.
- [x] `context-budget-gate`, `local-context-router`, `graphify-code-map` 스킬을 작성합니다.
- [x] 스킬 사용 규칙 문서를 추가하고 진입 파일에서 연결합니다.
- [x] 세 CLI 스킬 디렉토리에 스킬을 복제합니다.
- [x] 스킬과 문서 변경을 검증합니다.

## Context Notes

- 상태: active.
- 작업 브랜치: 현재 worktree.
- 결정: 처음부터 hook으로 자동 개입하지 않고, LLM이 발견해 사용할 수 있는 스킬로 먼저 배포합니다.
- 결정: `context-budget-gate`를 상위 문지기 스킬로 두고, 필요할 때 `local-context-router`와 `graphify-code-map`을 함께 사용하도록 설계합니다.
- 설치: `~/.codex/skills`, `~/.claude/skills`, `~/.agents/skills`에 세 스킬을 복제했습니다.
- 검증: `quick_validate.py`는 PyYAML 미설치로 실행 실패했습니다. 대신 frontmatter 필수 필드, TODO 잔여, `git diff --check`, 한국어 문장 끝 콜론, 설치본 존재 여부를 확인했습니다.
