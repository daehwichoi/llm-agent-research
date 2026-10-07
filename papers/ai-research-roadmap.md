# AI Research Roadmap — Essential Papers

2026년 기준 주요 AI 연구 흐름을 **Reasoning / Agent / RL / World Model / Embodied AI / Synthetic Data / Evaluation**의 7개 축으로 나누고, 각 분야를 이해하기 위해 우선 읽을 논문을 정리합니다.

> 목표: 최신 논문을 단순 나열하기보다 `기초 아이디어 → 패러다임 전환 → 현재 연구 방향`의 흐름을 이해하는 것.

---

## 1. Reasoning & Test-time Compute

### 핵심 질문
모델 크기를 키우는 것 외에, inference 시점에 더 많은 탐색·검증·계산을 사용하면 reasoning 능력을 얼마나 향상시킬 수 있는가?

### Essential Papers

1. **Chain-of-Thought Prompting Elicits Reasoning in Large Language Models** — Wei et al. (2022)
   - CoT reasoning의 대표적인 출발점.
   - 중간 reasoning step을 생성하여 복잡한 문제 해결 능력을 끌어냄.
   - https://arxiv.org/abs/2201.11903

2. **Self-Consistency Improves Chain of Thought Reasoning in Language Models** — Wang et al. (2022)
   - 여러 reasoning path를 sampling하고 최종 답을 aggregate.
   - inference-time compute/scaling의 초기 형태로 볼 수 있음.
   - https://arxiv.org/abs/2203.11171

3. **Tree of Thoughts: Deliberate Problem Solving with Large Language Models** — Yao et al. (2023)
   - reasoning을 단일 chain이 아니라 search problem으로 확장.
   - https://arxiv.org/abs/2305.10601

4. **DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning** — DeepSeek-AI (2025)
   - RL을 통해 reasoning behavior를 강화하는 현대 reasoning model의 핵심 사례.
   - https://arxiv.org/abs/2501.12948

### 추천 순서
`CoT → Self-Consistency → Tree of Thoughts → DeepSeek-R1`

---

## 2. AI Agent & Tool Use

### 핵심 질문
LLM을 단순 응답 모델이 아니라 환경을 관찰하고, 계획하고, 도구를 사용하고, 실패에서 복구하는 시스템으로 어떻게 만들 것인가?

### Essential Papers

1. **ReAct: Synergizing Reasoning and Acting in Language Models** — Yao et al. (2023) ★★★★★
   - `Thought → Action → Observation` loop.
   - 현대 LLM Agent architecture의 핵심 출발점.
   - https://arxiv.org/abs/2210.03629

2. **Toolformer: Language Models Can Teach Themselves to Use Tools** — Schick et al. (2023)
   - LLM이 API/tool을 언제 호출할지 학습하는 방법.
   - https://arxiv.org/abs/2302.04761

3. **Reflexion: Language Agents with Verbal Reinforcement Learning** — Shinn et al. (2023)
   - 실행 실패를 reflection/memory로 남기고 다음 시도에 활용.
   - https://arxiv.org/abs/2303.11366

4. **Voyager: An Open-Ended Embodied Agent with Large Language Models** — Wang et al. (2023)
   - automatic curriculum, skill library, iterative improvement.
   - 장기적으로 능력을 축적하는 agent 사례.
   - https://arxiv.org/abs/2305.16291

5. **SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering** — Yang et al. (2024) ★★★★★
   - 실제 software engineering 환경에서 agent-computer interface의 중요성을 보여줌.
   - https://arxiv.org/abs/2405.15793

### 추천 순서
`ReAct → Toolformer → Reflexion → SWE-agent → Voyager`

---

## 3. Reinforcement Learning & Verifiable Reward

### 핵심 질문
LLM의 행동과 reasoning을 reward를 이용해 어떻게 학습하고, 특히 정답을 검증할 수 있는 영역에서 어떻게 self-improvement를 만들 것인가?

### Essential Papers

1. **Proximal Policy Optimization Algorithms (PPO)** — Schulman et al. (2017)
   - 현대 RLHF를 이해하기 위한 기본 RL 알고리즘.
   - https://arxiv.org/abs/1707.06347

2. **Training Language Models to Follow Instructions with Human Feedback (InstructGPT)** — Ouyang et al. (2022)
   - `SFT → Reward Model → PPO` RLHF pipeline의 대표 논문.
   - https://arxiv.org/abs/2203.02155

3. **Direct Preference Optimization: Your Language Model is Secretly a Reward Model (DPO)** — Rafailov et al. (2023)
   - 별도의 RL loop 없이 preference optimization을 단순화.
   - https://arxiv.org/abs/2305.18290

4. **Let's Verify Step by Step** — Lightman et al. (2023)
   - Outcome reward와 Process Reward Model의 차이를 이해하는 핵심 논문.
   - https://arxiv.org/abs/2305.20050

5. **DeepSeek-R1** — DeepSeek-AI (2025)
   - RL을 alignment를 넘어 reasoning 능력 강화에 활용한 중요한 사례.
   - https://arxiv.org/abs/2501.12948

### 추천 순서
`PPO → InstructGPT → DPO → Let's Verify Step by Step → DeepSeek-R1`

---

## 4. World Models

### 핵심 질문
Agent가 실제 환경에서 모든 경우를 경험하지 않고도, 환경의 dynamics를 학습하여 미래를 예측하고 그 안에서 행동을 계획할 수 있는가?

### Essential Papers

1. **World Models** — Ha & Schmidhuber (2018) ★★★★★
   - latent representation 안에서 환경 dynamics를 학습한다는 기본 아이디어.
   - https://arxiv.org/abs/1803.10122

2. **Dream to Control: Learning Behaviors by Latent Imagination (Dreamer)** — Hafner et al. (2019)
   - learned world model 내부의 imagined trajectory에서 policy를 학습.
   - https://arxiv.org/abs/1912.01603

3. **Mastering Diverse Domains through World Models (DreamerV3)** — Hafner et al. (2023)
   - 다양한 domain에서 general world-model RL을 보여줌.
   - https://arxiv.org/abs/2301.04104

4. **Genie: Generative Interactive Environments** — Bruce et al. (2024)
   - video에서 action-controllable interactive environment를 학습하는 foundation world model 방향.
   - https://arxiv.org/abs/2402.15391

### 추천 순서
`World Models → Dreamer → DreamerV3 → Genie`

---

## 5. Embodied AI / Robotics / VLA

### 핵심 질문
Vision, Language, Sensor 정보를 실제 physical action으로 어떻게 연결할 것인가?

### Essential Papers

1. **RT-1: Robotics Transformer for Real-World Control at Scale** — Brohan et al. (2022)
   - Transformer 기반 large-scale robot control.
   - https://arxiv.org/abs/2212.06817

2. **PaLM-E: An Embodied Multimodal Language Model** — Driess et al. (2023)
   - Vision, language, robot sensor를 language model과 통합.
   - https://arxiv.org/abs/2303.03378

3. **RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control** — Brohan et al. (2023) ★★★★★
   - web-scale vision-language knowledge를 robot action으로 연결.
   - VLA 패러다임의 대표 논문.
   - https://arxiv.org/abs/2307.15818

4. **OpenVLA: An Open-Source Vision-Language-Action Model** — Kim et al. (2024)
   - open-source VLA로 구현과 실험을 따라가기 좋은 자료.
   - https://arxiv.org/abs/2406.09246

### 추천 순서
`RT-1 → PaLM-E → RT-2 → OpenVLA`

---

## 6. Synthetic Data & Self-Improvement

### 핵심 질문
모델이 스스로 학습 데이터, reasoning trajectory, feedback을 만들어 자신의 능력을 지속적으로 개선할 수 있는가?

### Essential Papers

1. **Self-Instruct: Aligning Language Models with Self-Generated Instructions** — Wang et al. (2022) ★★★★★
   - 모델이 instruction data를 생성하고 filtering하여 다시 학습에 활용.
   - https://arxiv.org/abs/2212.10560

2. **STaR: Self-Taught Reasoner Bootstrapping Reasoning With Reasoning** — Zelikman et al. (2022)
   - 성공적인 reasoning trajectory를 이용해 reasoning 능력을 반복적으로 향상.
   - https://arxiv.org/abs/2203.14465

3. **Self-Play Fine-Tuning Converts Weak Language Models to Strong Language Models (SPIN)** — Chen et al. (2024)
   - 모델의 이전 버전과 self-play하면서 preference를 개선.
   - https://arxiv.org/abs/2401.01335

4. **The Curse of Recursion: Training on Generated Data Makes Models Forget** — Shumailov et al.
   - synthetic data의 재귀적 학습에서 발생할 수 있는 model collapse 문제.
   - https://arxiv.org/abs/2305.17493

### 추천 순서
`Self-Instruct → STaR → SPIN → The Curse of Recursion`

---

## 7. Evaluation & Benchmark

### 핵심 질문
AI가 benchmark 문제를 잘 푸는 것과 실제 업무를 수행하는 능력 사이의 차이를 어떻게 측정할 것인가?

### Essential Papers

1. **Measuring Massive Multitask Language Understanding (MMLU)** — Hendrycks et al. (2020)
   - 범용 language-model knowledge benchmark의 대표적인 출발점.
   - https://arxiv.org/abs/2009.03300

2. **BIG-Bench: Beyond the Imitation Game** — Srivastava et al. (2022)
   - 다양한 task를 이용한 broad capability evaluation.
   - https://arxiv.org/abs/2206.04615

3. **SWE-bench: Can Language Models Resolve Real-World GitHub Issues?** — Jimenez et al. (2023/2024) ★★★★★
   - 실제 repository와 GitHub issue를 이용한 software-agent evaluation.
   - https://arxiv.org/abs/2310.06770

4. **OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments** — Xie et al. (2024)
   - 실제 desktop environment에서 computer-use agent를 평가.
   - https://arxiv.org/abs/2404.07972

### 추천 순서
`MMLU → BIG-Bench → SWE-bench → OSWorld`

---

# Recommended Core 10

전체를 한 번에 읽기 부담스럽다면 다음 10편부터 시작합니다.

| Priority | Paper | Theme | Why |
|---:|---|---|---|
| 1 | Attention Is All You Need | Foundation | Transformer 기본 구조 |
| 2 | Chain-of-Thought Prompting | Reasoning | LLM reasoning의 출발점 |
| 3 | ReAct | Agent | reasoning + acting의 기본 구조 |
| 4 | Toolformer | Tool Use | LLM의 API/tool 사용 |
| 5 | Reflexion | Agent | feedback, reflection, memory |
| 6 | DeepSeek-R1 | Reasoning/RL | 현대 reasoning + RL 흐름 |
| 7 | SWE-bench | Evaluation | 실제 software task 평가 |
| 8 | SWE-agent | Agent | 실전 coding agent architecture |
| 9 | Self-Instruct | Synthetic Data | self-generated training data |
| 10 | DreamerV3 | World Model | latent imagination 기반 planning/RL |

## 개인 학습 우선순위

Data Engineering / Data Platform / AI Agent 실무와 연결한다면 다음 순서를 우선 추천합니다.

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
