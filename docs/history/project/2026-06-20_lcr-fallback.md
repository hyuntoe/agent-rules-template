# LCR 장애 대응 규칙 추가 계획

## Plan

Ollama 서버가 꺼져 있거나, 모델이 없거나, 응답이 느릴 때 LCR이 작업을 막지 않도록 폴백 규칙을 추가합니다. `local-context-routing.md`와 `local-context-router` 스킬 원본을 수정하고, 세 CLI 설치본에 다시 복제합니다.

## Checklist

- [x] `local-context-routing.md`에 Ollama 장애·지연 대응 기준을 추가합니다.
- [x] `local-context-router` 스킬에 같은 운영 기준을 추가합니다.
- [x] 세 CLI 스킬 설치본을 갱신합니다.
- [x] 변경을 검증합니다.

## Context Notes

- 상태: active.
- 작업 브랜치: 현재 worktree.
- 결정: LCR은 쿼터 절약 장치이지 필수 관문이 아니므로, 느리거나 준비되지 않았으면 `rg`, `git`, graphify, 수동 원문 축소로 폴백하게 합니다.
- 검증: `git diff --check` 통과. 한국어 문장 끝 콜론 검색 통과. 세 CLI 설치본의 `local-context-router`에 fallback 규칙 반영 확인.
