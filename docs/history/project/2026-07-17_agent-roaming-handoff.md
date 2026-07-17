# 에이전트 로밍과 핸드오프 규칙 추가 계획

## Plan

쿼터 소진 시점을 예측하지 않고도 다른 인터랙티브 PM이 작업을 이어받을 수
있도록 `agent-rules-template`의 공통 규칙에 에이전트 로밍과 핸드오프 스냅샷
규칙을 추가한다. 기준 원본을 먼저 커밋하고 원격에 푸시한 뒤, 프로젝트 리스트에
있는 대상 프로젝트에는 기존 문서를 덮어쓰지 않고 프로젝트별 문맥을 보존하면서
공통 규칙을 병합한다.

## Checklist

- [x] 기준 원본 저장소의 현재 브랜치, 리모트, 변경 상태를 확인한다.
- [x] 작업 브랜치 `plan/agent-roaming-handoff`를 만든다.
- [x] `workflow-rules.md`에 플랜 파일의 `Handoff Snapshot` 규칙을 추가한다.
- [x] `multi-agents-orchestration.md`에 로밍, PM 전환, 체크포인트 트리거를 추가한다.
- [x] 수동 핸드오프 준비와 인수를 돕는 명령·스킬 계약을 문서에 추가한다.
- [x] `README.md`의 현재 상태와 다음 보강 후보에 로밍 규칙을 반영한다.
- [x] 문서 변경을 검증한다.
- [x] 의미 단위 커밋을 만든다.
- [x] 원격 브랜치에 푸시한다.
- [x] PM 전환 시점을 알 수 없다는 점을 반영해 기존 전환 전 최신화 문구를
  트랜잭션 기반 체크포인트 문구로 바꾼다.
- [x] 프로젝트 리스트 대상별 보존 병합 작업 계획을 정리한다.

## Context Notes

- Status: complete.
- Branch/worktree: `plan/agent-roaming-handoff` at
  `/mnt/c/Users/Hyuntoe/agent-rules-template`.
- Last action: 템플릿 문서에 로밍·핸드오프 규칙을 반영하고, 대상 프로젝트별
  보존 병합 계획을 정리했다.
- Current intent: 완료된 플랜을 `docs/history/project/`로 이동하고 `main`에 병합한다.
- Dirty files: 이 플랜 파일의 완료 상태 갱신.
- Next safe step: 플랜 파일을 history로 이동해 커밋한다.
- Blockers: 없음.
- Last verification: `git diff`, 한국어 문장 끝 콜론 `rg` 검사,
  `git status --short --branch` 확인.

## 대상 프로젝트 병합 계획

### 대상

- WSL: `/home/hyuntoe/projects/ai-hq`
- WSL: `/home/hyuntoe/projects/jk-exam-kb`
- WSL: `/home/hyuntoe/projects/jk-math`
- WSL: `/home/hyuntoe/projects/rabbit7-trader`
- WSL: `/home/hyuntoe/projects/rabbit7-wiki`
- Windows: `/mnt/c/users/hyuntoe/jk-japanese`
- Windows: `/mnt/c/users/hyuntoe/jk-make-mathtest`
- Windows: `/mnt/c/users/hyuntoe/jk-manager`
- Windows: `/mnt/c/users/hyuntoe/SCS Mod modding`

`agent-rules-template` 자체는 기준 원본으로만 검증하고, 자기 자신에게 다시 병합하지
않는다.

### 프로젝트별 반복 절차

1. 프로젝트의 현재 브랜치, 리모트, 미커밋 변경을 확인한다.
2. `README.md`, `AGENTS.md`, `CLAUDE.md`, `workflow-rules.md`,
   `multi-agents-orchestration.md`, `docs/backlog`, `docs/plans`의 기존 내용을
   먼저 읽는다.
3. 프로젝트 고유 규칙과 공통 템플릿 규칙의 충돌 지점을 목록화한다.
4. 템플릿 파일로 통째로 덮어쓰지 않고 다음 항목만 필요한 위치에 병합한다.
   - 플랜 파일 `Handoff Snapshot` 권장 또는 필수 규칙.
   - 작업 트랜잭션 기반 체크포인트 트리거.
   - PM 쿼터 소진 시 사용자 주도 인터랙티브 PM 전환 절차.
   - 새 PM 시작 프롬프트 또는 읽기 순서.
5. 프로젝트별 작업 브랜치 또는 worktree를 사용한다.
6. 문서 링크, 경로, 예시 명령이 해당 프로젝트에 맞는지 검증한다.
7. 프로젝트별 적용 내역, 보존한 기존 규칙, 의도적으로 제외한 항목을 해당
   프로젝트의 플랜 또는 history에 남긴다.
8. 프로젝트별 의미 단위 커밋을 만든다.
9. 리모트 푸시는 프로젝트별 배포 필요성과 사용자 승인을 확인한 뒤 진행한다.

### 프로젝트별 확인 포인트

- 기존 문서가 이미 프로젝트 고유 PM 전환 규칙을 갖고 있으면 그 규칙을 우선
  보존하고 공통 용어만 맞춘다.
- `docs/plans/` 운영 방식이 없는 프로젝트에는 최소 구조만 추가한다.
- 코드 저장소가 아닌 문서·지식 저장소는 검증 명령을 문서 링크와 git 상태 확인으로
  축소한다.
- 민감 정보, 로컬 절대 경로, 개인별 인증 상태는 공통 템플릿에서 복사하지 않는다.
- Windows 경로와 WSL 경로가 섞인 프로젝트는 새 PM 시작 프롬프트에 기준 경로를
  명확히 적는다.
