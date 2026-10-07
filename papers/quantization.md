# LLM Quantization

확인일: 2026-10-07. P1=우선 읽기, P2=주제별 심화. 우선순위는 실무/방법론 기준이며 citation impact 순위가 아닙니다.

## 핵심 목록

| 논문 | 발표 | 우선순위 | 핵심 기여 |
|---|---|---|---|
| SpinQuant: LLM quantization with learned rotations | ICLR 2025; arXiv 초판 2024 | P1 | 학습한 rotation으로 outlier와 양자화 오차 완화 |
| FlatQuant: Flatness Matters for LLM Quantization | ICML 2025 | P1 | layer별 affine transform과 fused kernel |
| WUSH: Near-Optimal Adaptive Transforms for LLM Quantization | ICML 2026 | P1 | 데이터에 적응하는 blockwise transform; INT/FP 지원 |
| LC-QAT: Data-Efficient 2-Bit QAT for LLMs via Linear-Constrained Vector Quantization | ICML 2026 | P1 | 2-bit weight-only VQ와 미분 가능한 QAT 결합 |
| Towards Quantization-Aware Training for Ultra-Low-Bit Reasoning LLMs | ICLR 2026 | P2 | reasoning 보존을 위한 2단계 QAT |
| PTQ1.61: Push the Real Limit of Extremely Low-Bit Post-Training Quantization Methods for Large Language Models | ACL 2025 | P2 | salient channel 4-bit + 나머지 binary |
| BitNet b1.58 2B4T Technical Report | 2025 기술 보고서 | P2 | 처음부터 학습한 native ternary model |
| Low-Bit Quantization Favors Undertrained LLMs | ACL 2025 | P2 | 학습량과 양자화 손실의 관계 분석 |

## SpinQuant

[원문](https://arxiv.org/abs/2405.16406) · [PDF](https://arxiv.org/pdf/2405.16406)

Random rotation의 품질 편차를 줄이기 위해 rotation 자체를 학습합니다. Weight, activation, KV-cache를 함께 4-bit로 낮추는 접근을 이해하는 기준점입니다.

읽을 질문: rotation 학습 비용과 inference 시 변환 비용은 어디에 발생하는가?

## FlatQuant

[공식 발표](https://proceedings.mlr.press/v267/sun25l.html) · [PDF](https://raw.githubusercontent.com/mlresearch/v267/main/assets/sun25l/sun25l.pdf) · [코드](https://github.com/ruikangliu/FlatQuant)

가중치와 activation 분포를 평탄하게 만드는 affine transformation을 calibration으로 학습합니다. Kronecker 분해와 kernel fusion으로 변환 overhead를 줄입니다.

저자 보고: LLaMA-3-70B W4A4 accuracy drop <1%, FP16 대비 prefill 최대 2.3배, decoding 최대 1.7배. 다른 모델/하드웨어에서 동일한 개선을 보장하는 수치는 아닙니다.

## WUSH

[공식 발표](https://proceedings.mlr.press/v306/chen26z.html) · [PDF](https://raw.githubusercontent.com/mlresearch/v306/main/assets/chen26z/chen26z.pdf) · [코드](https://github.com/IST-DASLab/WUSH)

Hadamard와 데이터의 second moment를 결합한 비직교 transform입니다. 특정 RTN block quantizer와 가정 아래 near-optimal transform을 유도합니다.

저자 보고: Llama-3.1-8B-Instruct MXFP4에서 Hadamard baseline 대비 RTN 평균 +2.8pt. BF16 대비 최대 5.8배는 **layer throughput** 수치이며 전체 서비스 속도 향상이 아닙니다.

## LC-QAT

[공식 발표](https://proceedings.mlr.press/v306/wang26kc.html) · [PDF](https://raw.githubusercontent.com/mlresearch/v306/main/assets/wang26kc/wang26kc.pdf)

Discrete vector에 learned affine mapping을 적용해 2-bit weight-only VQ를 QAT로 최적화합니다. 좋은 PTQ 초기값을 이용해 학습 데이터 요구를 줄이는 접근입니다.

저자 보고: 비교 QAT 방법 학습 데이터의 0.1~10%를 사용하면서 더 좋은 결과. Activation까지 2-bit로 줄였다는 의미는 아닙니다.

## Reasoning QAT

[공식 발표](https://proceedings.iclr.cc/paper_files/paper/2026/hash/209423f076b6479ab3a4f45886e30306-Abstract-Conference.html) · [코드](https://github.com/yasu0001/ReasoningQAT)

Mixed-domain calibration 뒤 teacher-guided reward rectification으로 reasoning 능력을 복구합니다. 일반 perplexity나 zero-shot 점수만으로 reasoning 보존을 판단하기 어려운 문제를 다룹니다.

저자 보고: 2-bit Qwen3-8B가 5개 reasoning benchmark에서 PTQ baseline 대비 평균 50.45% 개선. 이를 50.45 percentage point 개선으로 읽으면 안 됩니다.

## PTQ1.61

[공식 발표](https://aclanthology.org/2025.acl-long.225/) · [PDF](https://aclanthology.org/2025.acl-long.225.pdf) · [코드](https://github.com/zjq0455/PTQ1.61)

중요 channel을 4-bit로 두고 나머지를 binary로 만들어 평균 1.61-bit를 목표로 합니다. Structured mask로 추가 저장 비용을 낮춥니다.

읽을 질문: 평균 weight bit 수와 scales/masks를 포함한 실제 메모리, 지원 kernel, 정확도 손실은 각각 얼마인가?

## BitNet b1.58 2B4T

[원문](https://arxiv.org/abs/2504.12285) · [PDF](https://arxiv.org/pdf/2504.12285)

Ternary weight {-1, 0, 1}를 사용하는 2B parameter 모델을 4T token으로 학습한 기술 보고서입니다. 기존 FP 모델에 PTQ를 적용하는 연구와 구분해야 합니다.

읽을 질문: 실제 저장 표현과 연산 kernel은 무엇이며, 같은 품질/학습 예산의 모델과 비교했는가?

## Low-Bit Quantization Favors Undertrained LLMs

[공식 발표](https://aclanthology.org/2025.acl-long.1555/) · [PDF](https://aclanthology.org/2025.acl-long.1555.pdf)

모델의 학습 정도와 양자화 내성을 함께 분석합니다. 작은 모델을 충분히 학습한 뒤 양자화하는 전략이 항상 유리한지 재검토할 때 유용합니다.

## Production 평가 체크

- VRAM: weights, scales, KV-cache, temporary buffers를 각각 측정.
- Latency: TTFT, prefill, decode tokens/s를 분리.
- Workload: 실제 batch와 context length 사용.
- Quality: 도메인 질의, tool calling, reasoning 정확도 평가.
- 배포: serving runtime의 해당 format/kernel 지원 확인.
