# 개인 프로젝트 공통 에이전트 규칙 롤아웃 완료

## Plan

`agent-rules-template`을 기준 원본으로 삼아 개인 프로젝트 목록의 에이전트 진입
규칙, 공통 개발 규칙, docs 워크플로우, 멀티에이전트 규칙, 로컬 컨텍스트 라우팅
규칙과 공통 스킬을 점검하고 추가 병합 적용했다.

## 대상과 결과

- `ai-hq` — 적용 완료. active Windows usage tray worktree를 보존하고 `main`에 병합·원격 푸시 완료.
- `jk-exam-kb` — 적용 완료. `main`에 병합하고 원격 푸시 완료.
- `jk-math` — 적용 완료. 오래된 로컬 `master` 작업트리를 보존하고 원격 `main`에 반영 완료.
- `rabbit7-wiki` — 적용 완료. `main`에 병합하고 원격 푸시 완료.
- `jk-japanese` — 적용 완료. `main`에 병합하고 원격 푸시 완료.
- `jk-make-mathtest` — 적용 완료. `main`에 병합하고 원격 푸시 완료.
- `jk-manager` — 적용 완료. `main`에 병합하고 원격 푸시 완료.
- `rabbit7-trader` — 제외. `ai-hq/docs/trading/`으로 흡수 통합했고 원격 저장소는 archive 처리했다.
- `SCS Mod modding` — 제외. Git 저장소가 아니므로 공통 규칙 병합 대상에서 뺐다.
- `agent-rules-template` — 기준 원본으로 참조 무결성을 확인했다.

## Checklist

- [x] 기준 원본 `agent-rules-template`의 상태와 참조 무결성을 확인한다.
- [x] 대상 프로젝트의 기존 규칙과 템플릿 차이를 각각 검토한다.
- [x] 필요한 공통 내용을 충돌 없이 추가 병합한다.
- [x] 각 프로젝트에서 문서 링크, 경로와 적용 결과를 검증한다.
- [x] 프로젝트별 적용 내역과 의도적으로 제외한 항목을 기록한다.
- [x] 각 대상 저장소에 의미 단위 커밋을 만들고 원격 푸시한다.
- [x] 완료된 rollout 항목을 backlog에서 history로 이동한다.

## Context Notes

- 대부분의 프로젝트는 프로젝트 고유 규칙을 보존하면서 `Handoff Snapshot`, PM 로밍,
  `handoff prepare`, `handoff receive`, 로밍 후 복귀 규칙을 추가했다.
- `jk-math`는 로컬 `/home/hyuntoe/projects/jk-math`가 오래된 `master`와 대량
  미커밋 변경을 가진 상태였다. 그래서 원격 `main` 기준의 임시 worktree에서만
  확인·정정하고, 오래된 로컬 작업트리는 보존했다.
- `ai-hq`는 active Windows usage tray worktree가 있어 본체 `main`에서 규칙 문서만
  별도 브랜치로 처리했고, active worktree는 건드리지 않았다.
- `rabbit7-trader`는 독립 프로젝트로 유지하지 않고 `ai-hq/docs/trading/`으로
  흡수 통합한 뒤 GitHub 저장소를 archive했다.

## 경험 기록

이번 롤아웃은 각 대상 프로젝트에서는 브랜치나 임시 worktree를 사용했지만,
정작 조율 저장소인 `agent-rules-template` 자체에서는 별도 worktree를 먼저 만들지
않고 시작했다. 결과적으로 큰 문제는 없었지만, 장시간·다중 저장소 롤아웃에서는
조율 저장소도 active 작업으로 취급해야 한다.

다음부터는 같은 유형의 작업을 시작할 때 먼저 다음 절차를 따른다.

1. 템플릿 저장소에서 rollout 전용 브랜치와 worktree를 만든다.
2. `docs/plans/`에 조율 플랜을 만들고 `Handoff Snapshot`을 둔다.
3. 대상 프로젝트 하나를 끝낼 때마다 템플릿 상태표도 같은 worktree에서 갱신한다.
4. 전체 완료 후 조율 플랜을 `docs/history/project/`로 이동하고 템플릿 `main`에 병합한다.

## Handoff Snapshot

- Status: completed.
- Branch/worktree: `main` at `/mnt/c/Users/Hyuntoe/agent-rules-template`.
- Last action: 모든 대상 프로젝트 적용·제외 기록을 완료하고 rollout 기록을 history로 이동했다.
- Current intent: 완료 상태를 원격에 푸시하고 마무리한다.
- Dirty files: 이 history 파일, `docs/backlog/next.md`, `workflow-rules.md`.
- Next safe step: 검증 후 커밋·푸시.
- Blockers: 없음.
- Last verification: 대상 프로젝트별 원격 푸시 확인, 템플릿 참조 무결성 확인.
