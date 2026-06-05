# 공통 규칙 (KR) - Claude 용

## 작업 전 읽을 문서

- `karpathy-plus.md` — 공통 개발 규칙(Karpathy 기반 + 변형). 모든 작업에 적용.
- `workflow-rules.md` — docs 디렉토리(backlog/plans/history) 관리 규칙.
- `multi-agents-orchestration.md` — 멀티에이전트 협업·역할 규칙.
- `README.md` — 이 프로젝트가 무엇을 하는지·현재 상태·다음 단계 (프로젝트별).

위 규칙 문서(karpathy-plus·workflow-rules·multi-agents)가 실제 규칙의 단일 진실 소스(SSOT)이며, 이 파일은 가리키기만 합니다. 프로젝트 한정 내용은 `README.md`와 `docs/`에만 둡니다. codex·agy는 같은 규칙을 `AGENTS.md`를 통해 읽습니다.

---

## graphify

이 프로젝트는 `graphify-out/`에 graphify 지식 그래프를 둡니다.

코드 그래프를 탐색할 때는 다음 규칙을 따릅니다.

- 아키텍처나 코드베이스 질문에 답하기 전에 `graphify-out/GRAPH_REPORT.md`를 읽고 중심 노드와 커뮤니티 구조를 확인합니다.
- `graphify-out/wiki/index.md`가 있으면 원문 파일을 직접 읽기 전에 먼저 그 인덱스를 따라갑니다.
- 모듈 관계 질문은 grep보다 `graphify query "<question>"`, `graphify path "<A>" "<B>"`, `graphify explain "<concept>"`를 우선 사용합니다.
- graphify가 설정된 프로젝트에서 코드 구조에 영향이 있는 변경을 한 뒤에는 `graphify update .`를 실행해 그래프를 최신 상태로 유지합니다. 이 작업은 AST 기반이며 추가 API 비용이 들지 않습니다.

---

## docs 워크플로우

이 프로젝트는 `workflow-rules.md`에 정의된 `docs/` 디렉토리 사용 규칙을 따릅니다.

- 모든 에이전트는 작업을 시작하기 전에 `workflow-rules.md`를 읽고 그에 따라 문서(`docs/backlog`, `docs/plans`, `docs/history`)를 관리합니다.
- 비단순 작업 시 `docs/plans/`에 단일 플랜 파일을 생성하고, 작업 완료 후 `docs/history/project/`로 이동하는 흐름을 준수합니다.
- 다른 문서와 이 규칙이 충돌하면 `docs` 워크플로우에 대해서는 `workflow-rules.md`를 최우선으로 합니다.

---

## 멀티에이전트 협업

이 프로젝트는 Claude를 PM/오케스트레이터로 두고 codex(GPT)·agy(Gemini)를 하위 에이전트로 활용하는 협업 규칙을 `multi-agents-orchestration.md`에 둡니다.

- 작업을 시작하기 전에 `workflow-rules.md`(docs 디렉토리 관리)와 `multi-agents-orchestration.md`(에이전트 협업)를 읽고, 둘의 역할을 **구분하여** 따릅니다.
- 단순 작업은 단일 에이전트로 처리하고, 멀티에이전트 파이프라인은 `multi-agents-orchestration.md`의 분기 기준에 해당하는 복잡 작업에만 적용합니다.
- 외부 에이전트(codex·agy) 호출 방법, 무결성 가드, 핸드오프 프로토콜은 `multi-agents-orchestration.md`를 기준으로 합니다.
