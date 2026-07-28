• STEM: MMLU (Hendrycks et al., 2020) contains a series of benchmarks across diverse domains to evaluate model’s language understanding. We consider the high school physics and chemistry portions of MMLU because of the deep reasoning involved.

• Knowledge QA: We consider TimeQA (Chen et al., 2021) since it contains complex queries that require challenging time-sensitive knowledge. We also experiment with SituatedQA (Zhang & Choi, 2021), another challenging open-retrieval QA dataset requiring model to answer questions given temporal or geographical contexts.

• Multi-Hop Reasoning: We experiment with MuSiQue (Trivedi et al., 2022), a hard multihop reasoning dataset created via composable pairs of single-hop questions, and StrategyQA (Geva et al., 2021) with open-domain questions that demands some strategy to solve.

### 3.2 MODELS

We use the following state of the art LLMs: PaLM-2L (Anil et al., 2023) and GPT-4 (OpenAI, 2023). We experiment with a variety of baselines with an instruction-tuned PaLM-2L model.

### 3.3 EVALUATION

Conventional evaluation metric such as accuracy, F1 score has limitations specifically for evaluating the generations of state of the art LLMs since these models often generate long form answers which are hard to capture. We instead conduct evaluation using the PaLM2-L model where we few-shot prompt the model to identify equivalence between target answers and the model predictions. Few-shot examples, prompts and other details we use for this evaluation are in Appendix C.

### 3.4 BASELINE METHODS

• PaLM-2L, PaLM-2L 1-shot: PaLM-2L is either queried directly with the question or has a single demonstration exemplar of question-answer included in the prompt.

• PaLM-2L + CoT, PaLM-2L + CoT 1-shot: PaLM-2L model is queried with zero-shot CoT prompting (Kojima et al., 2022): “Let’s think step by step” is appended to the question. For 1-shot, One demonstration example of a question and answer pair is provided in the prompt, where the answer is in the style of CoT (Wei et al., 2022b) with intermediate reasoning steps.

• PaLM-2L + TDB: Zero-shot prompting with “Take a deep breath and work on this problem step-by-step.” (Yang et al., 2023) prepended to the question.

• PaLM-2L + RAG: For Sections 5 and 6, we use retrieval-augmented generation (RAG) where the relevant passage retrieved is used as context by the LLM.

• GPT-4: GPT-4 API is directly queried.

We do not use RAG for MMLU, because of the inherent reasoning nature of this benchmark contrary to the other fact-seeking datasets. All inferences are done using greedy decoding.

## 4 STEM

We evaluate STEP-BACK PROMPTING on STEM tasks (Hendrycks et al., 2020) to gauge the efficacy of our method on reasoning in highly-specialized domains. We explain below our experimental setup, result and analysis of applying STEP-BACK PROMPTING on the MMLU high-school Physics and Chemistry benchmarks.

### 4.1 STEP-BACK PROMPTING

Questions in the MMLU benchmarks require deeper reasoning. Furthermore, they also require understanding and application of formulae which are often physics and chemistry principles and concepts. In this case, we first teach the model to do abstraction in the form of concepts and first principles such as Newton's first law of motion, Doppler effect, and Gibbs free energy etc. The implicit step-back question here is "what are the physics or chemistry principles and concepts involved in