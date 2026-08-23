arXiv:2310.06117v1 [cs.LG] 9 Oct 2023
[Non-Text]
Google DeepMind
TAKE A STEP BACK: EVOKING REASONING VIA AB-STRACTION IN LARGE LANGUAGE MODELS
Huaixiu Steven Zheng* Swaroop Mishra* Xinyun Chen Heng-Tze Cheng
Ed H. Chi Quoc V Le Denny Zhou
Google DeepMind
ABSTRACT
We present STEP-BACK PROMPTING, a simple prompting technique that enables LLMs to do abstractions to derive high-level concepts and first principles from instances containing specific details. Using the concepts and principles to guide the reasoning steps, LLMs significantly improve their abilities in following a correct reasoning path towards the solution. We conduct experiments of STEP-BACK PROMPTING with PaLM-2L models and observe substantial performance gains on a wide range of challenging reasoning-intensive tasks including STEM, Knowledge QA, and Multi-Hop Reasoning. For instance, STEP-BACK PROMPTING improves PaLM-2L performance on MMLU Physics and Chemistry by 7% and 11%, TimeQA by 27%, and MuSiQue by 7%.
The purpose of abstraction is not to be vague, but to create a new semantic level in which one can be absolutely precise. — Edsger W. Dijkstra
1 INTRODUCTION
The field of natural language processing (NLP) is witnessing a ground-breaking revolution because of the Transformer-based (Vaswani et al., 2017) large language models (LLMs) (Devlin et al., 2018; Raffel et al., 2020; Brown et al., 2020; Anil et al., 2023). Scaling up the model size and pre-training corpus (Hoffmann et al., 2022; Chowdhery et al., 2022) has brought remarkable improvement in model capabilities and sample efficiency with insights from the scaling law (Kaplan et al., 2020; Hoffmann et al., 2022), as well as emergent abilities (Wei et al., 2022a) such as multi-step reasoning (Wei et al., 2022b; Zhou et al., 2022) and instruction following (Mishra et al., 2022b; Wei et al., 2021).

Figure 1: Strong Performance of STEP-BACK PROMPTING: our proposed Abstraction-and-Reasoning scheme leads to a substantial improvement in a wide range of challenging tasks in STEM, Knowledge QA and Multi-Hop Reasoning requiring complex (often multi-hop) reasoning.
*Equal Contribution
1