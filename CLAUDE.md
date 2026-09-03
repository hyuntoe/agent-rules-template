# 공통 규칙 (KR) - Claude 용

## 문서 로딩 — 필요할 때 읽는다 (항상 전부 읽지 않음)

`README.md`는 프로젝트 개요·현재 상태 파악을 위해 작업 전 먼저 읽습니다.

아래 두 줄은 모든 작업에서 상시 유지합니다.

- 비단순 작업(파일 2개 이상 수정, 공통 규칙·워크플로 변경 등) 전에는 플랜 파일 하나를 먼저 만듭니다.
- 기본은 단일 에이전트입니다. 다른 에이전트를 부르는 건 예외입니다.

그 외에는 아래 **관찰 가능한 조건**을 만났을 때만 해당 문서를 읽습니다. 어느 조건에도 해당하는지 애매하면, 안전한 쪽으로 관련 문서를 읽습니다.

| 문서 | 언제 읽는가 |
|---|---|
| `karpathy-plus.md` | 저장소 산출물(코드·설정·문서)을 구현·수정·리뷰·진단할 때. |
| `workflow-rules.md` | `docs/`를 만들거나 옮길 때, 파일을 2개 이상 수정할 가능성이 있을 때, 공통 규칙·워크플로·템플릿 의미를 바꿀 때, 브랜치·worktree·핸드오프·커밋 생명주기를 다룰 때. |
| `multi-agents-orchestration.md` | 유저가 위임·리뷰어·병렬 작업·핸드오프를 요청했을 때, 또는 실제로 다른 에이전트를 호출하기 직전. |
| `local-context-routing.md` | 2,000줄 이상 로그·파일을 다루거나 32,768 토큰을 넘길 가능성이 있는 입력을 클라우드 LLM에 보내기 전. |
| `skill-usage-rules.md` | 이 저장소의 공통 스킬을 사용·수정·설치·동기화할 때. |

위 규칙 문서(karpathy-plus·workflow-rules·multi-agents·local-context-routing·skill-usage-rules)가 실제 규칙의 단일 진실 소스(SSOT)이며, 이 파일은 가리키기만 합니다. 프로젝트 한정 내용은 `README.md`와 `docs/`에만 둡니다. codex·agy는 같은 규칙을 `AGENTS.md`를 통해 읽되, `multi-agents-orchestration.md` 2.4절의 세션 메시징은 Claude 전용이라 codex·agy에는 적용되지 않습니다.

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

- 위 "문서 로딩" 표의 트리거를 만나면 `workflow-rules.md`를 읽고 그에 따라 문서(`docs/backlog`, `docs/plans`, `docs/history`)를 관리합니다.
- 비단순 작업 시 `docs/plans/`에 작업별 플랜 파일을 생성하고, 작업 완료 후 `docs/history/project/`로 이동하는 흐름을 준수합니다.
- 다른 문서와 이 규칙이 충돌하면 `docs` 워크플로우에 대해서는 `workflow-rules.md`를 최우선으로 합니다.

---

## 멀티에이전트 협업

이 프로젝트는 사용자가 진입한 인터랙티브 에이전트를 PM/오케스트레이터로
두고, 필요할 때 다른 에이전트를 워커로 활용하는 협업 규칙을
`multi-agents-orchestration.md`에 둡니다.

- 위 "문서 로딩" 표에서 `workflow-rules.md`와 `multi-agents-orchestration.md`의 트리거는 서로 독립적으로 적용합니다. 한쪽 트리거만 해당하면 그 문서만 읽고, 둘 다 해당하면 둘 다 읽어 역할을 **구분하여** 따릅니다.
- 단순 작업은 단일 에이전트로 처리하고, 멀티에이전트 파이프라인은 `multi-agents-orchestration.md`의 분기 기준에 해당하는 복잡 작업에만 적용합니다.
- 외부 에이전트(codex·agy) 호출 방법, 무결성 가드, 핸드오프 프로토콜은 `multi-agents-orchestration.md`를 기준으로 합니다.
