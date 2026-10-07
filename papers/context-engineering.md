# Context Engineering & Long-Running Agents

확인일: 2026-10-07. 아래는 **Anthropic 공식 엔지니어링 글**이며 peer-reviewed 논문이 아닙니다. Harness 논문과 함께 읽는 실무 참고 자료로 분리했습니다.

## 자료 목록

| 자료 | 우선순위 | 핵심 |
|---|---|---|
| Effective Context Engineering for AI Agents | P1 | 필요한 context를 적시에 선택하고 관리 |
| Effective Harnesses for Long-Running Agents | P1 | session을 넘는 작업의 상태와 artifact 유지 |
| Harness Design for Long-Running Application Development | P2 | 장기 개발 작업의 실행과 평가 구조 |

## Effective Context Engineering for AI Agents

[공식 글](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

Prompt 문장뿐 아니라 model이 보는 전체 context를 설계합니다. Tool을 통한 just-in-time retrieval, compaction, structured notes와 작업 분해를 다룹니다.

실무 질문: 어떤 정보는 항상 유지하고 어떤 정보는 필요할 때 다시 가져올 것인가? 오래된 상태와 tool 결과를 어떻게 구분할 것인가?

## Effective Harnesses for Long-Running Agents

[공식 글](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

Initializer와 후속 coding 작업을 나누고 progress 기록과 검증 절차를 통해 다음 session으로 작업을 이어갑니다.

실무 질문: 완료 상태를 모델의 선언에 의존하는가, 실행 가능한 검사로 확인하는가? 다음 session이 직전 결과를 재현할 수 있는가?

## Harness Design for Long-Running Application Development

[공식 글](https://www.anthropic.com/engineering/harness-design-long-running-apps)

장기 application 개발에서 harness의 task 분해와 평가 설계를 살펴보는 자료입니다. 단일 제품에서의 관찰을 모든 domain의 최적 구조로 일반화하지 않습니다.

## 읽은 뒤 구현할 최소 구조

1. Task: 요청, 성공 조건, budget을 저장.
2. Context: 최신 schema/metadata와 필요한 기록을 조회.
3. Execute: model의 tool 요청을 실행.
4. Verify: 결과 artifact를 규칙과 실제 실행으로 확인.
5. Persist: 진행 상태와 증거를 저장.
6. Recover: 오류를 분류하고 제한된 재시도 또는 종료.

## 함께 볼 논문

[Harness Engineering 목록](harness-engineering.md)의 Harness-Bench와 Survey는 runtime 평가와 분류를 보완합니다.

장기 작업에서는 context window 크기 외에도 상태의 정확성, 검증의 신뢰도, 중단 후 복구 비용을 측정해야 합니다.
