# AGENTS.md — codex·agy 공통 진입 규칙

codex(GPT)·agy(Gemini)가 이 프로젝트에서 작업할 때 자동으로 읽는 진입 파일.
**실제 규칙은 여기 복붙하지 않고 공통 문서를 가리킨다(SSOT).** 규칙을 고칠
때는 아래 공통 문서를 고친다. (Claude는 `CLAUDE.md`로 같은 문서를 읽는다.)

## 프로젝트 개요

이 프로젝트가 무엇을 하는지·현재 상태·다음 단계는 `README.md`에 있다. 작업
전 먼저 읽는다. 프로젝트별 작업·결정·백로그는 `docs/`(backlog/plans/history)에
있다. (이 파일 `AGENTS.md`는 프로젝트와 무관한 범용 규칙만 담는다.)

## 작업 전 반드시 읽을 문서

- **`karpathy-plus.md`** — 공통 개발 규칙(단순성, 외과적 수정, 가정 명시,
  한국어 출력·문장 끝 콜론 금지, 새 소스 파일 첫 줄 한국어 역할 주석, 완료
  전 테스트 등). codex·agy도 이 규칙을 따른다.
- **`workflow-rules.md`** — `docs/`(backlog/plans/history) 관리 규칙. 비단순
  작업은 `docs/plans/`에 단일 플랜 파일 하나를 만들고 완료 시
  `docs/history/project/`로 이동한다.
- **`multi-agents-orchestration.md`** — 멀티에이전트 협업·역할 규칙.

## 멀티에이전트 — 너의 역할은 "실행 모드"로 정해진다

상세는 `multi-agents-orchestration.md` 2.1절. 핵심만 요약하면,

- **headless(`-p`/`exec`)로 호출됐다면 → 너는 워커다.** 지정된 단위 작업
  (구현/리뷰/검증)만 하고, **다른 외부 에이전트를 호출하지 마라**(단방향 =
  루프 차단). 호출 프롬프트가 역할을 지정한다.
- **사람이 인터랙티브로 너를 띄웠고 작업이 복잡하면**(다파일·설계판단·
  교차검증) → `claude`를 PM으로 호출(`claude -p`)해 위임하라. 단독으로 팀을
  자처해 여러 에이전트를 엮지 마라.
- 단순 작업은 위임 없이 직접 처리한다.

## 무결성 (어길 시 작업 거부)

- 쓰기는 한 번에 한 에이전트만. 워커로 호출됐다면 지시 범위 밖 파일을
  건드리지 마라.
- 구현 작업은 격리된 브랜치/worktree에서 하고, 머지 판단은 PM(claude)이 한다.
- 상세는 `multi-agents-orchestration.md` 4·5절(무결성·핸드오프).

## graphify

이 프로젝트는 `graphify-out/`에 graphify 지식 그래프를 둔다.

- 아키텍처·코드베이스 질문 전에 `graphify-out/GRAPH_REPORT.md`가 있으면 먼저 읽는다.
- `graphify-out/wiki/index.md`가 있으면 원문 직접 읽기 전에 인덱스를 따른다.
- 모듈 관계 질문은 grep보다 `graphify query`/`path`/`explain`을 우선한다.
- `GRAPH_REPORT.md`가 없거나 오래됐으면 `graphify update .`로 갱신한다(AST 기반, 추가 API 비용 없음).
