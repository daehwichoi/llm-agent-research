# AI Research Roadmap — Essential Papers

2026년 기준 주요 AI 연구 흐름을 **Reasoning / Agent / RL / World Model / Embodied AI / Synthetic Data / Evaluation**의 7개 축으로 나누고, 각 분야를 이해하기 위해 우선 읽을 논문을 정리합니다.

> 목표: 최신 논문을 단순 나열하기보다 `기초 아이디어 → 패러다임 전환 → 현재 연구 방향`의 흐름을 이해하는 것.

---

## 1. Reasoning & Test-time Compute

모델 크기를 키우는 것 외에, inference 시점에 더 많은 탐색·검증·계산을 사용하면 reasoning 능력을 얼마나 향상시킬 수 있는가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | Chain-of-Thought Prompting | 중간 reasoning step을 생성하는 CoT의 대표적 출발점 | [📄 arXiv](https://arxiv.org/abs/2201.11903) |
| 2 | Self-Consistency | 여러 reasoning path를 sampling하고 답을 aggregate | [📄 arXiv](https://arxiv.org/abs/2203.11171) |
| 3 | Tree of Thoughts | reasoning을 단일 chain이 아닌 search problem으로 확장 | [📄 arXiv](https://arxiv.org/abs/2305.10601) |
| 4 | **DeepSeek-R1** ⭐ | RL을 통한 현대 reasoning model의 핵심 사례 | [📄 arXiv](https://arxiv.org/abs/2501.12948) |

**읽기 순서:** `CoT → Self-Consistency → Tree of Thoughts → DeepSeek-R1`

---

## 2. AI Agent & Tool Use

LLM을 단순 응답 모델이 아니라 환경을 관찰하고, 계획하고, 도구를 사용하고, 실패에서 복구하는 시스템으로 어떻게 만들 것인가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | **ReAct** ⭐ | `Thought → Action → Observation` Agent loop | [📄 arXiv](https://arxiv.org/abs/2210.03629) |
| 2 | Toolformer | LLM이 API/tool을 언제 호출할지 학습 | [📄 arXiv](https://arxiv.org/abs/2302.04761) |
| 3 | Reflexion | 실패를 reflection/memory로 남겨 다음 시도에 활용 | [📄 arXiv](https://arxiv.org/abs/2303.11366) |
| 4 | **SWE-agent** ⭐ | 실제 SW 환경에서 Agent-Computer Interface의 중요성 | [📄 arXiv](https://arxiv.org/abs/2405.15793) |
| 5 | Voyager | curriculum + skill library + iterative improvement | [📄 arXiv](https://arxiv.org/abs/2305.16291) |

**읽기 순서:** `ReAct → Toolformer → Reflexion → SWE-agent → Voyager`

---

## 3. Reinforcement Learning & Verifiable Reward

LLM의 행동과 reasoning을 reward로 어떻게 학습하고, 특히 정답을 검증할 수 있는 영역에서 어떻게 self-improvement를 만들 것인가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | PPO | 현대 RLHF를 이해하기 위한 기본 RL 알고리즘 | [📄 arXiv](https://arxiv.org/abs/1707.06347) |
| 2 | InstructGPT | `SFT → Reward Model → PPO` RLHF pipeline | [📄 arXiv](https://arxiv.org/abs/2203.02155) |
| 3 | DPO | 별도 RL loop 없이 preference optimization 단순화 | [📄 arXiv](https://arxiv.org/abs/2305.18290) |
| 4 | Let's Verify Step by Step | Outcome Reward vs Process Reward Model | [📄 arXiv](https://arxiv.org/abs/2305.20050) |
| 5 | **DeepSeek-R1** ⭐ | RL을 alignment를 넘어 reasoning 강화에 활용 | [📄 arXiv](https://arxiv.org/abs/2501.12948) |

**읽기 순서:** `PPO → InstructGPT → DPO → Let's Verify Step by Step → DeepSeek-R1`

---

## 4. World Models

Agent가 실제 환경에서 모든 경우를 경험하지 않고도 환경의 dynamics를 학습하여 미래를 예측하고 그 안에서 행동을 계획할 수 있는가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | **World Models** ⭐ | latent representation에서 환경 dynamics 학습 | [📄 arXiv](https://arxiv.org/abs/1803.10122) |
| 2 | Dreamer | imagined trajectory에서 policy 학습 | [📄 arXiv](https://arxiv.org/abs/1912.01603) |
| 3 | DreamerV3 | 다양한 domain으로 general world-model RL 확장 | [📄 arXiv](https://arxiv.org/abs/2301.04104) |
| 4 | Genie | video에서 action-controllable interactive environment 학습 | [📄 arXiv](https://arxiv.org/abs/2402.15391) |

**읽기 순서:** `World Models → Dreamer → DreamerV3 → Genie`

---

## 5. Embodied AI / Robotics / VLA

Vision, Language, Sensor 정보를 실제 physical action으로 어떻게 연결할 것인가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | RT-1 | Transformer 기반 large-scale robot control | [📄 arXiv](https://arxiv.org/abs/2212.06817) |
| 2 | PaLM-E | Vision + Language + robot sensor를 LM과 통합 | [📄 arXiv](https://arxiv.org/abs/2303.03378) |
| 3 | **RT-2** ⭐ | web-scale VLM knowledge를 robot action으로 연결 | [📄 arXiv](https://arxiv.org/abs/2307.15818) |
| 4 | OpenVLA | 구현과 실험을 따라가기 좋은 open-source VLA | [📄 arXiv](https://arxiv.org/abs/2406.09246) · [💻 GitHub](https://github.com/openvla/openvla) |

**읽기 순서:** `RT-1 → PaLM-E → RT-2 → OpenVLA`

---

## 6. Synthetic Data & Self-Improvement

모델이 스스로 학습 데이터, reasoning trajectory, feedback을 만들어 자신의 능력을 지속적으로 개선할 수 있는가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | **Self-Instruct** ⭐ | self-generated instruction data + filtering | [📄 arXiv](https://arxiv.org/abs/2212.10560) |
| 2 | STaR | 성공한 reasoning trajectory로 반복 학습 | [📄 arXiv](https://arxiv.org/abs/2203.14465) |
| 3 | SPIN | 이전 모델과 self-play하며 preference 개선 | [📄 arXiv](https://arxiv.org/abs/2401.01335) |
| 4 | The Curse of Recursion | recursive synthetic training의 model collapse 문제 | [📄 arXiv](https://arxiv.org/abs/2305.17493) |

**읽기 순서:** `Self-Instruct → STaR → SPIN → The Curse of Recursion`

---

## 7. Evaluation & Benchmark

AI가 benchmark 문제를 잘 푸는 것과 실제 업무를 수행하는 능력 사이의 차이를 어떻게 측정할 것인가?

| 순서 | 논문 | 핵심 | 바로가기 |
|---:|---|---|---|
| 1 | MMLU | 범용 language-model knowledge benchmark | [📄 arXiv](https://arxiv.org/abs/2009.03300) |
| 2 | BIG-Bench | 다양한 task를 이용한 broad capability evaluation | [📄 arXiv](https://arxiv.org/abs/2206.04615) |
| 3 | **SWE-bench** ⭐ | 실제 repository + GitHub issue 기반 SW Agent 평가 | [📄 arXiv](https://arxiv.org/abs/2310.06770) |
| 4 | OSWorld | 실제 desktop environment에서 computer-use Agent 평가 | [📄 arXiv](https://arxiv.org/abs/2404.07972) |

**읽기 순서:** `MMLU → BIG-Bench → SWE-bench → OSWorld`

---

# Recommended Core 10

전체를 한 번에 읽기 부담스럽다면 아래 10편부터 시작합니다. **논문명을 누르거나 바로가기에서 즉시 원문으로 이동할 수 있습니다.**

| Priority | Paper | Theme | Why | Link |
|---:|---|---|---|---|
| 1 | [Attention Is All You Need](https://arxiv.org/abs/1706.03762) | Foundation | Transformer 기본 구조 | [📄](https://arxiv.org/abs/1706.03762) |
| 2 | [Chain-of-Thought Prompting](https://arxiv.org/abs/2201.11903) | Reasoning | LLM reasoning의 출발점 | [📄](https://arxiv.org/abs/2201.11903) |
| 3 | [ReAct](https://arxiv.org/abs/2210.03629) | Agent | reasoning + acting의 기본 구조 | [📄](https://arxiv.org/abs/2210.03629) |
| 4 | [Toolformer](https://arxiv.org/abs/2302.04761) | Tool Use | LLM의 API/tool 사용 | [📄](https://arxiv.org/abs/2302.04761) |
| 5 | [Reflexion](https://arxiv.org/abs/2303.11366) | Agent | feedback, reflection, memory | [📄](https://arxiv.org/abs/2303.11366) |
| 6 | [DeepSeek-R1](https://arxiv.org/abs/2501.12948) | Reasoning/RL | 현대 reasoning + RL 흐름 | [📄](https://arxiv.org/abs/2501.12948) |
| 7 | [SWE-bench](https://arxiv.org/abs/2310.06770) | Evaluation | 실제 software task 평가 | [📄](https://arxiv.org/abs/2310.06770) |
| 8 | [SWE-agent](https://arxiv.org/abs/2405.15793) | Agent | 실전 coding agent architecture | [📄](https://arxiv.org/abs/2405.15793) |
| 9 | [Self-Instruct](https://arxiv.org/abs/2212.10560) | Synthetic Data | self-generated training data | [📄](https://arxiv.org/abs/2212.10560) |
| 10 | [DreamerV3](https://arxiv.org/abs/2301.04104) | World Model | latent imagination 기반 planning/RL | [📄](https://arxiv.org/abs/2301.04104) |

## 개인 학습 우선순위

Data Engineering / Data Platform / AI Agent 실무와 연결한다면:

`ReAct → Toolformer → Reflexion → SWE-bench → SWE-agent → DeepSeek-R1`

이후 관심에 따라 두 갈래로 확장합니다.

- **Agent self-improvement:** Self-Instruct → STaR → RL / Verifiable Reward
- **Physical / interactive intelligence:** World Models → DreamerV3 → RT-2 → OpenVLA

---

## 연구 흐름 요약

```text
Transformer / Foundation Models
        ↓
Chain-of-Thought / Reasoning
        ↓
Reasoning + Tool Use
        ↓
Agent + Environment + Memory + Verification
        ↓
RL / Verifiable Reward + Synthetic Data
        ↓
Self-improving Agents

World Models ──→ Embodied AI / VLA
```

핵심 변화는 **더 큰 모델 자체를 만드는 것**에서 **추론하고, 도구를 사용하고, 환경과 상호작용하고, 결과를 검증하며 개선되는 시스템을 만드는 것**으로 연구 범위가 확장되고 있다는 점입니다.
