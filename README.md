# LLM & Agent Research Reading List

LLM Quantization, Agent Harness, Context Engineering 및 최신 AI 연구 흐름 관련 논문과 실무 자료를 정리한 읽기 목록입니다.

자료 확인일: **2026-10-07**. 요약은 원문 초록 및 공식 발표 페이지를 바탕으로 작성했습니다.

## 목록

| 주제 | 문서 | 다루는 내용 |
|---|---|---|
| AI Research Roadmap | [필수 논문 로드맵](papers/ai-research-roadmap.md) | Reasoning, Agent, RL, World Model, Embodied AI, Synthetic Data, Evaluation |
| Quantization | [논문 목록](papers/quantization.md) | W4A4/FP4, learned transform, 2-bit QAT, native low-bit |
| Harness Engineering | [논문 목록](papers/harness-engineering.md) | 모델과 runtime 분리 평가, coding agent 구조, 검증 |
| Context Engineering | [실무 자료](papers/context-engineering.md) | context 선택, 상태 유지, 장기 작업, 복구 |

## 추천 읽기 순서

- **AI/Agent 전체 로드맵:** ReAct → Toolformer → Reflexion → SWE-bench → SWE-agent → DeepSeek-R1.
- Agent 구현: Context Engineering → Effective Harnesses → Harness-Bench → Coding Agent Anatomy → Harness Survey.
- Quantization: SpinQuant → FlatQuant → WUSH → LC-QAT → Reasoning QAT → BitNet.

## 선정과 해석 기준

- 주요 학회 발표, 방법론 기여, 재현 가능한 평가, 실무 관련성을 기준으로 선정했습니다.
- **읽기 우선순위는 편집자의 판단이며 인용 수 순위가 아닙니다.** 최신 2026 프리프린트는 관심 연구로 분류하며 이미 영향력이 검증된 논문으로 단정하지 않습니다.
- 논문, 기술 보고서, 기업 엔지니어링 글을 구분합니다.
- 성능 수치는 해당 논문의 실험 결과입니다. GPU, 모델, batch, sequence length, kernel에 따라 달라집니다.
- PDF 바이너리 대신 공식 원문/PDF 링크를 보관합니다. 코드 링크는 확인된 것만 기재합니다.

## 기술 흐름을 읽는 관점

Quantization은 outlier를 줄이는 transform 계열과 초저비트 표현/학습 계열로 나누어 읽는 것이 좋습니다. 모든 논문을 단일 계보나 비트 수가 계속 낮아지는 발전 단계로 볼 수는 없습니다.

Agent는 모델 외에도 context, 도구, 상태, 검증, 복구를 포함한 전체 시스템으로 평가해야 합니다. Harness 설계가 중요하다는 주장은 모델 능력이 중요하지 않다는 의미가 아닙니다.

최신 AI 연구는 Reasoning, Tool Use, Agent, RL, Synthetic Data, World Model이 점차 결합되는 방향으로 읽는 것이 유용합니다. 특히 실제 업무 Agent에서는 모델 자체뿐 아니라 데이터/context 접근, tool interface, verification, evaluation 설계가 핵심 연구·엔지니어링 영역입니다.
