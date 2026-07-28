(2023) demonstrating the efficacy of STEP-BACK PROMPTING in tackling complex tasks which are otherwise challenging due to the amount of details involved to reason through. Figure 1 shows a summary of all the key results presented in this paper. Some the tasks are very challenging: both PaLM-2L and GPT-4 achieve only  $ \sim $ 40% accuracy on TimeQA and MuSiQue. Chain-of-Thought prompting leads to a minor improvement on a few tasks, while STEP-BACK PROMPTING improves the performance of PaLM-2L across the board: 7% and 11% on MMLU Physics and Chemistry, 27% on TimeQA, and 7% on MuSiQue.

We conduct a variety of analysis and find that STEP-BACK PROMPTING has strong performance improvements (up to 36%) over chain of thought (CoT) prompting (Wei et al., 2022b) and take a deep breathe (TDB) prompting (Yang et al., 2023). We perform a qualitative evaluation where we find that Step-Back fixes a large portion of errors of the base model (up to  $ \sim $ 40%) while introducing a small portion of new errors (max  $ \sim $ 12%). We also conduct an error analysis and find that majority of the errors made by STEP-BACK PROMPTING is attributed to the intrinsic limitations of reasoning capabilities of LLMs while abstraction skills are relatively easy to teach LLMs, pointing out the direction for future improvements of methods alike STEP-BACK PROMPTING.

## 2 STEP-BACK PROMPTING

STEP-BACK PROMPTING is motivated by the observation that many tasks contain a lot of details, and are hard for LLMs to retrieve relevant facts to tackle the task. As shown in the first example (top) in Figure 2, for a Physics question of "What happens to the pressure, P, of an ideal gas if the temperature is increased by a factor of 2 and the volume is increased by a factor of 8?", the LLM can deviate from the first principle of Ideal Gas Law when reasoning directly on the question. Similarly, a question of "Estella Leopold went to which school between Aug 1954 and Nov 1954?" is very hard to address directly given the detailed time range constraint. In both cases, taking a step back and asking a step-back question helps model to solve the problem effectively.

We define a step-back question as a derived question from the original question at a higher-level of abstraction. For instance, instead of directly asking “which school Estella Leopold went to during a specific period”, a step-back question (Figure 2 bottom) would ask about the “education history”, which is a high-level concept encompasses the original question. Answering the step-back question of “Estella Leopold’s education history” in this case will provide all the necessary information to reason about “which school Estella Leopold went to during a specific period”. The premise is that more often the step-back question is much easier to address than the original question. Grounding the reasoning on top of such abstractions helps to avoid reasoning errors in the intermediate steps such as the example shown in Figure 2 (left) from Chain-of-Thought. In short, STEP-BACK PROMPTING consists of two simple steps:

• Abstraction: Instead of addressing the question directly, we first prompt the LLM to ask a generic step-back question about a higher-level concept or principles, and retrieve relevant facts about the high-level concept or principles.

• Reasoning: Grounded on the facts regarding high-level concept or principles, the LLM can reason about the solution to the original question. We term this Abstraction-grounded Reasoning.

In the following sections, we present an empirical study of STEP-BACK PROMPTING on a range of challenging tasks covering STEM, Knowledge QA and Multi-Hop Reasoning involving complex reasoning.

## 3 EXPERIMENTAL SETUP

Here we define the tasks and models we experiment with. We also describe our evaluation metric and the baselines we consider.

### 3.1 TASKS

We experiment with the following diverse tasks: (a) STEM, (b) Knowledge QA and (c) Multi-Hop Reasoning. We describe below the datasets we consider (see Appendix B for more details).