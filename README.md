# 模型编辑
## 方法总结
| 类别 | 方法 | 编辑范围 | 编辑方程 | 是否需要训练 | 批量编辑 | 编辑参数 | 保持架构？ | 只使用(xe,ye) | 单次非连续编辑 | 批量非连续编辑 | 单次连续编辑 | 批量连续编辑 | 扩展到大模型（>10B） |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
|  | IKE | memory+retriever | Input → [Mem : Input] | × | × | - |  |  |  |  |  |  |
|  | MQuAKE |  |  |  |  |  |  |  |  |  |  |  |  |
|  | Language Patch | Output head + params | h → λh+ (1 − λ)Patch(x) | × | √ | dh × #Output |  |  |  |  |  |  |  |
|  | KAFT |  |  |  |  |  |  |  |  |  |  |  |  |
|  | SERAC | memory+classifier +auxiliary model | Output → Modelcf (x) | √ | √ | - | × | √ | √ | √ | √ | √ | √ |
|  | MemPrompt | memory+retriever | Input → [Mem : Input] | × | √ | - |  |  |  |  |  |  |  |
|  | T-Patcher | FFN+params | h → h + FFNadd(x) | √? | × | N × dh | × | × | √ | √ | √ | × | √ |
|  | GRACE | FFN+codebook | h → GRACE(x) | √ | × | N × 2dh | × | √ | √ | √ | √ | √ | √ |
|  | CALINET | FFN+params | h → h + FFNadd(x) | √ | √ | N × dh | √ | √ | √ | √ | × | × | √ |
|  | MeLLo | memory+retriever | Input → [Mem : Input] | × | × | - |  |  |  |  |  |  |  |
|  | ICE | prompt | Input → [Mem : Input] | × | × | - |  |  |  |  |  |  |  |
|  | PokeMQA | memory+retriever | Input → [Mem : Input] | √ | × | - |  |  |  |  |  |  |  |
|  | REMEDI | auxiliary model | h → REMEDI(x) | √ | × | dh × dh |  |  |  |  |  |  |  |
|  | LoRA | Attn or FFN | h → h + s · LoRA(x) | √ | √ | 2L × 2damdh |  |  |  |  |  |  |  |
|  | MELO | Attn or FFN | h → h + s · LoRA(x) | √ | × | 2L × 2damdh |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |

## 论文列表
### 基于外部存储
按模型外和模型内分类

【IKE】Can We Edit Factual Knowledge by In-Context Learning? **(2023.05|EMNLP 2023)** [[paper](https://arxiv.org/abs/2305.12740)]

【MQuAKE】MQuAKE: Assessing Knowledge Editing in Language Models via Multi-Hop Questions **(2023.05|EMNLP 2023)** [[paper](https://arxiv.org/abs/2305.14795)]

【Language Patch】Fixing Model Bugs with Natural Language Patches **(2022.11|EMNLP 2022)** [[paper](https://arxiv.org/abs/2211.03318)]

【KAFT】Large Language Models with Controllable Working Memory **(2022.11)** [[paper](https://arxiv.org/abs/2211.05110)]

【SERAC】Memory-Based Model Editing at Scale **(2022.06|ICML 2022)** [[paper](https://arxiv.org/abs/2206.06520)]

【MemPrompt】Memory-assisted prompt editing to improve GPT-3 after deployment **(2022.01)** [[paper](https://arxiv.org/abs/2201.06009)]

------

【T-Patcher】Transformer-Patcher: One Mistake worth One Neuron **(2023.01|ICLR 2023)** [[paper](https://arxiv.org/abs/2301.09785)]

【GRACE】Aging with GRACE: Lifelong Model Editing with Discrete Key-Value Adaptors **(2022.11|NeurIPS 2023)** [[paper](https://proceedings.neurips.cc/paper_files/paper/2023/hash/95b6e2ff961580e03c0a662a63a71812-Abstract-Conference.html)]

【CALINET】Calibrating Factual Knowledge in Pretrained Language Models **(2022.08|Findings of EMNLP 2022)** [[paper](https://arxiv.org/abs/2210.03329)]
### 基于全局优化
【F-Learning】Forgetting before Learning: Utilizing Parametric Arithmetic for Knowledge Updating in Large Language Models **(2023.11)** [[paper](https://arxiv.org/abs/2311.08011)]

【PPA】Plug-and-Play Adaptation for Continuously-updated QA **(2022.04|Findings of ACL 2022)** [[paper](https://arxiv.org/abs/2204.12785)]

【】Modifying Memories in Transformer Models **(2020.12)** [[paper](https://arxiv.org/abs/2012.00363)]

【RecAdam】Recall and Learn: Fine-tuning Deep Pretrained Language Models with Less Forgetting **(2020.04|EMNLP 2020)** [[paper](https://arxiv.org/abs/2004.12651)]

【Editable Training】Editable Neural Networks **(2020.04)** [[paper](https://arxiv.org/abs/2004.00345)]

------

【KGEditor】Editing Language Model-based Knowledge Graph Embeddings **(2023.01|AAAI 2024)** [[paper](https://arxiv.org/abs/2301.10405)]

【SLAG】Do Language Models Have Beliefs? Methods for Detecting, Updating, and Visualizing Model Beliefs **(2021.11)** [[paper](https://arxiv.org/abs/2111.13654)]

【SLAG】Methods for Measuring, Updating, and Visualizing Factual Beliefs in Language Models **(2023.05|ACL 2023)** [[paper](https://aclanthology.org/2023.eacl-main.199/)]

【MEND】Fast Model Editing at Scale **(2021.08|ICLR 2022)** [[paper](https://arxiv.org/abs/2110.11309)]

【KE】Editing Factual Knowledge in Language Models **(2021.04|EMNLP 2021)** [[paper](https://arxiv.org/abs/2104.08164)]

【Hyper-Network】HyperNetworks **(2016.09|ICLR 2017)** [[paper](https://arxiv.org/abs/1609.09106)]

### 基于定位再编辑
【DEPN】DEPN: Detecting and Editing Privacy Neurons in Pretrained Language Models **(2023.10|EMNLP 2023)** [[paper](https://arxiv.org/abs/2310.20138)]

【PMET】PMET: Precise Model Editing in a Transformer **(2023.08|AAAI 2024)** [[paper](https://arxiv.org/abs/2308.08742)]

【PCGU】Unlearning Bias in Language Models by Partitioning Gradients **(2023.07|Findings of ACL 2023)** [[paper](https://aclanthology.org/2023.findings-acl.375/)]

【MEMIT】Mass-Editing Memory in a Transformer **(2022.10)** [[paper](https://arxiv.org/abs/2210.07229)]

【ROME】Locating and Editing Factual Associations in GPT **(2022.02|NeurIPS 2022)** [[paper](https://arxiv.org/abs/2202.05262)]

【KN】Knowledge Neurons in Pretrained Transformers **(2021.04|ACL 2022)** [[paper](https://arxiv.org/abs/2104.08696)]

------

【MEMITcsk】Editing Common Sense in Transformers **(2023.12|EMNLP 2023)** [[paper](https://aclanthology.org/2023.emnlp-main.511/)]

【BAKE/BIRD】Untying the Reversal Curse via Bidirectional Language Model Editing **(2023.10)** [[paper](https://arxiv.org/abs/2310.10322)]

