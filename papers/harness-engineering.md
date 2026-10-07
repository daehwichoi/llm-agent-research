# Agent Harness Engineering

확인일: 2026-10-07. Harness는 LLM의 실행 loop, context, tools, state, permissions, tracing, recovery를 담당하는 runtime으로 이해합니다.

**최신 프리프린트의 실무 관련성과 학술적 impact는 다릅니다.** 아래 P1/P2는 읽기 순서이며 인용 수나 검증된 영향력 순위가 아닙니다.

## 핵심 목록

| 논문 | 상태 | 우선순위 | 선정 이유 |
|---|---|---|---|
| Harness-Bench: Measuring Harness Effects across Models in Realistic Agent Workflows | arXiv 2026 프리프린트 | P1 | 모델과 harness 조합을 같은 task 환경에서 비교 |
| Harness Engineering: Anatomy, Architecture, and Evolution of Coding Agents — A Source-Code Study of Eleven Systems | arXiv 2026 프리프린트 | P1 | 실제 coding agent runtime의 구조 비교 |
| Agent Systems with Harness Engineering: A Systematic Survey | Frontiers of Computer Science, 2026; 온라인 9월 16일 | P1 | 구성 요소와 연구 영역의 지도 |
| AI Harness Engineering: A Runtime Substrate for Foundation-Model Software Agents | arXiv 2026 프리프린트 | P2 | 검증 가능성과 trace 중심의 runtime 책임 정의 |
| SWE-Bench Pro: Can AI Agents Solve Long-Horizon Software Engineering Tasks? | arXiv 2025; OpenReview에 ICLR 2026 제출 기록 | P1 | 복잡한 실제 software task 평가 |

SWE-Bench Pro의 제출 기록을 학회 채택 확정으로 표기하지 않았습니다.

## Harness-Bench

[원문](https://arxiv.org/abs/2605.27922) · [PDF](https://arxiv.org/pdf/2605.27922)

106개 sandbox task와 5,194개 trajectory에서 model-harness configuration별 completion, efficiency, failure를 분석합니다.

의의: 모델 이름 하나만으로 agent 성능을 설명하지 않고, 실행 환경까지 평가 단위로 둡니다. “Model × Harness”는 직관적 비유이며 검증된 수학적 법칙이 아닙니다.

읽을 질문: budget과 tool 환경을 어떻게 통제했는가? 개별 harness 구성 요소의 인과 효과까지 분리했는가?

## Coding Agent Anatomy

[원문](https://arxiv.org/abs/2609.00006) · [PDF](https://arxiv.org/pdf/2609.00006)

11개 coding harness의 소스 코드를 비교하고 runtime 구성 요소와 반복되는 설계 패턴을 정리합니다.

저자들은 조사 corpus에서 general-purpose agent framework 사용과 vector embedding 기반 code retrieval을 발견하지 않았다고 보고합니다. 이는 **조사한 시스템과 snapshot 범위의 관찰**이며 모든 agent에 일반화하거나 vector retrieval이 무용하다고 해석할 수 없습니다.

읽을 질문: loop, context compaction, tool dispatch, extension, safety 구현이 시스템마다 어떻게 다른가?

## Harness Survey

[공식 논문](https://journal.hep.com.cn/fcs/EN/10.1007/s11704-026-61123-6) · [DOI](https://doi.org/10.1007/s11704-026-61123-6)

Workflow, memory, skill library, multi-agent orchestration과 software engineering, research, tool/computer use 등의 평가를 연결합니다.

관련 읽기 목록: [Awesome Agent Harness](https://github.com/RUCAIBox/awesome-agent-harness)

읽을 질문: 모델 개선과 harness 개선의 trade-off를 어떻게 평가할 것인가?

## AI Harness Engineering

[원문](https://arxiv.org/abs/2605.13357) · [PDF](https://arxiv.org/pdf/2605.13357)

Task specification부터 verification, permissions, observability까지 11개 책임을 정리합니다. H0~H3 단계와 trace 기반 episode package로 결과의 증거 구조를 평가합니다.

의의: patch 생성 여부에서 검증 가능한 변경과 실행 증거로 평가를 확장합니다. 제한된 controlled validation을 광범위한 production 성능 증명으로 해석하지 않습니다.

## SWE-Bench Pro

[원문](https://arxiv.org/abs/2509.16941) · [PDF](https://arxiv.org/pdf/2509.16941) · [프로젝트](https://scaleapi.github.io/SWE-bench_Pro-os/) · [OpenReview](https://openreview.net/forum?id=9R2iUHhVfr)

더 복잡하고 긴 enterprise software engineering task를 평가합니다. Model, scaffold, task version을 함께 기록해야 비교가 의미 있습니다. 초기 논문 점수를 현재 leaderboard 점수로 사용하지 않습니다.

## 데이터 분석 Agent에 적용하는 실험 아이디어

다음은 논문 결과가 아니라 구현을 위한 제안입니다.

| Runtime 요소 | 구현 예 | 평가 항목 |
|---|---|---|
| Context | DB schema와 관련 metadata를 필요할 때 조회 | 관련성, token 비용 |
| Tools | 제한된 SQL/Python 실행 인터페이스 | 실행 성공률, 비용 |
| State | task ID, 중간 artifact, 완료 조건 저장 | 중단 후 복구율 |
| Verification | row count, units, 기간, 결과 재현 검사 | 잘못된 결과 탐지율 |
| Recovery | 오류 유형별 제한된 retry | 성공률, 반복 비용 |
| Observability | tool input/output, 증거, latency 기록 | 실패 원인 식별 |

같은 모델에서 runtime을 하나씩 바꾸고 성공률, p95 latency, token/DB 비용, 복구율을 비교하는 실험부터 시작할 수 있습니다.
