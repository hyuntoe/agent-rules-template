# 공통 규칙에 세션 메시징·컨텍스트 엔지니어링 신규 반영

## Plan

Claude Code에 세션 간 메시징(`SendMessage`/`ListAgents`)이 생겼고, Anthropic이
Claude 5세대용 컨텍스트 엔지니어링 가이드를 새로 냈다(judgment over rigid
rules, progressive disclosure, 상충 규칙 배제). 이 두 사실을 공통 SSOT 문서에
반영하고, codex 리뷰를 거쳐 확정한다.

## Checklist

- [x] codex에 1차 설계안(A/B/C) 리뷰 요청 — NO-GO, 6개 지적사항 수령.
- [x] 지적사항 반영한 revised 설계 확정(A: 역할모델 전역 정합, B: 비순환·관찰가능 트리거, C: README 단일화).
- [x] `multi-agents-orchestration.md` 2.2/2.3/5/6/9절에 Claude 세션 워커 개념 반영.
- [x] `CLAUDE.md`(프로젝트), `AGENTS.md` 진입 문서를 관찰가능 트리거 라우터로 재작성, 하단 중복 지시 제거.
- [x] `README.md`에 규칙 유지·정리 원칙 한 번만 추가.
- [x] codex에 2차 리뷰 요청 — 지적사항이 실제로 반영됐는지 확인. → NO-GO, 잔여 2건(결합 트리거, 용어 불일치).
- [x] 잔여 2건 수정 후 codex 3차 리뷰 — VERDICT=GO.
- [x] 완료 후 이 플랜을 `docs/history/project/`로 이동.

## Context Notes

- 세션 메시징은 Claude 네이티브 전용(사용자 확정). codex·agy는 크로스 세션
  메시징 없음(웹 검색 확인, agmsg 같은 서드파티 브리지는 비공식이라 미반영).
- codex 1차 리뷰 핵심: (1) B의 workflow-rules 트리거가 너무 늦음 → 관찰 가능한
  선제 조건으로, (2) A를 2.4/5절만 패치하면 "모든 워커는 headless"(2.2),
  "역할=실행모드"(2.3), "cold start 전역명제"(5절) 전제와 충돌 → 역할 판정
  기준을 "모델이 아니라 진입 경로+명시된 역할"로 재정의, (3) B의 "멀티에이전트/
  스킬 사용 여부 판단 시" 트리거는 순환 논리 → 관찰 가능 조건으로 교체,
  (4) Claude 세션 메시징 예외 범위를 도구명이 아니라 실행 경계로 명시(같은
  Claude Code 네이티브 하네스 + 기능 노출된 세션 간에만, codex 내부 subagent
  메시징은 별개), 메시징≠컨텍스트 자동공유, (5) C는 문서마다 넣지 말고
  README.md 한 곳에만, "모델 버전 올라가도 유지"는 karpathy-plus.md 서두
  전제와 충돌하므로 "성능 향상만으로 자동 삭제하지 않음/중복·버전의존 규칙은
  정기 재검증" 형태로.
- 브랜치: 현재 worktree 자체가 이 작업 전용(`orca-/에이전트-프롬프트-수정`).
  별도 feature 브랜치 불필요.
- codex 2차 리뷰 잔여 지적 2건: (a) CLAUDE.md 하단 "위 표의 트리거를 만나면
  workflow-rules.md와 multi-agents-orchestration.md를 읽고"가 결합 트리거로
  읽혀 한쪽만 충족해도 둘 다 읽는 것으로 해석됨 → "서로 독립적으로 적용"
  문구로 수정. (b) README.md의 "실행 모드에 따른 역할 판정" 표현이 새 기준
  "진입 경로 + 명시된 역할"과 어긋남 → 표현 통일. codex 3차 리뷰에서
  VERDICT=GO 확인.
- **범위 밖으로 의도적으로 제외**: `/home/hyuntoe/CLAUDE.md`(사용자 전역
  개인 설정, 이 저장소 밖)는 이번 작업에서 건드리지 않았다. 이 저장소는
  다른 프로젝트가 "필요한 규칙을 읽어 병합"하는 원본 템플릿이므로, 전역
  설정에 반영하려면 사용자가 별도로 이 저장소 변경분을 참고해 수동 병합해야
  한다.

## Handoff Snapshot

- Status: completed.
- Branch/worktree: `orca-/에이전트-프롬프트-수정` (현재 worktree).
- Last action: codex 3차 리뷰 VERDICT=GO 확인, 체크리스트 전부 완료.
- Current intent: 이 플랜을 `docs/history/project/`로 이동하고 커밋한다.
- Dirty files: `multi-agents-orchestration.md`, `CLAUDE.md`, `AGENTS.md`,
  `workflow-rules.md`, `README.md`, 이 플랜 파일(이동 예정).
- Next safe step: 플랜 이동 후 의미 단위 커밋.
- Blockers: 없음.
- Last verification: codex exec read-only 3회(1차 NO-GO, 2차 NO-GO 부분해결,
  3차 GO).
