## Turn 1 — document page 7 (rank 1 of 19)

| Dataset       | ChatGPT (gpt-3.5-turbo) | GPT-3.5 (text-davinci-003) | GPT-4 (gpt-4) |
|---------------|--------------------------|----------------------------|---------------|
|               | Standard | CoT | Logic-LM | Standard | CoT | Logic-LM | Standard | CoT | Logic-LM |
| PrOntoQA      | 47.40    | 67.80 | 61.00     | 51.80    | 83.00 | 85.00     | 77.40    | 98.79 | 83.20     |
| ProofWriter   | 35.50    | 49.17 | 58.33     | 36.16    | 48.33 | 71.45     | 52.67    | 68.11 | 79.66     |
| FOLIO         | 45.09    | 57.35 | 62.74     | 54.60    | 57.84 | 61.27     | 69.11    | 70.58 | 78.92     |
| LogicalDeduction | 40.00   | 42.33 | 65.67     | 41.33    | 48.33 | 62.00     | 71.33    | 75.25 | 87.63     |
| AR-LSAT       | 20.34    | 17.31 | 26.41     | 22.51    | 22.51 | 25.54     | 33.33    | 35.06 | 43.04     |

Table 2: Accuracy of standard promoting (Standard), chain-of-thought promoting (CoT), and our method (LOGIC-LM, without self-refinement) on five reasoning datasets. The best results within each base LLM are highlighted.

4.1 Main Results
We report the results of LOGIC-LM (without self-refinement) and baselines in Table 2. For LOGIC-LM, a symbolic solver does not return an answer when there are grammar errors in the symbolic formulation. For these un-executable cases, we fall back on using chain-of-thought to predict the answer. We have three major observations.
1. Logic-LM significantly outperforms standard LLMs and CoT across all datasets. With GPT-3.5, our method outperforms standard LLM on all datasets, with an average improvement of 39.2%. This highlights the benefit of combining LLMs with external symbolic solvers for logical reasoning. LOGIC-LM also improves CoT by a large margin of 18.4% on average, showing that offloading the reasoning to symbolic solvers greatly improves faithfulness compared with pure language-based reasoning with CoT.
2. GPT-4 outperforms GPT-3.5 by a large margin of 48.46% on average for the standard prompting. This aligns with the assertion that the main enhancement of GPT-4 lies in its ability to carry out complex reasoning (OpenAI, 2023). Although this may indicate that the logical reasoning capability can be boosted by scaling up the LLM, we observe that GPT-4 still makes numerous unfaithful reasoning errors. By delegating the reasoning to symbolic solvers, our method can further improve GPT-4 by an average of 24.98% and 10.44% for standard prompting and CoT prompting, respectively.
3. While integrating CoT generally enhances LLM performance, we find its benefits comparatively less substantial or even negative on FOLIO, LogicalDeduction, and AR-LSAT, with a modest improvement of 11.75%, 9.41%, and -3.2%, respectively. On the contrary, the benefits of CoT on ProntoQA and ProofWriter are 51.59% and 33.82%, respectively. A plausible explanation is that CoT emulates human forward-chain reasoning: beginning with known facts and sequentially deriving new conclusions until the goal is met. This reasoning style aligns well with problems in the PrOntoQA and ProofWriter datasets. However, FOL and CSP problems often necessitate more sophisticated reasoning strategies that are “

## Turn 2 — document page 8 (rank 2 of 19)

Figure 3: Accuracy of different models for increasing size of reasoning depth on the ProofWriter dataset. The chart shows three lines: Standard (dashed gray), CoT (dashed blue), and Logic-LM (solid green). Accuracy is on the y-axis (0 to 90), Reasoning Depth is on the x-axis (0 to 5). For Logic-LM (GPT-4), the accuracy values are: 79.9 at depth 0, 79.9 at depth 1, 79.9 at depth 2, 79.9 at depth 4, and 79.9 at depth 5. The text below the figure states: "For example, LOGIC-LM outperforms CoT by 7.1%, 5.0%, 12.7%, 20.0%, and 39.4% on depth-0, depth-1, depth-2, depth-4, and depth-5 problems, respectively."

Figure 4: The accuracy for different rounds of self-refinement, with the corresponding executable rates. The chart shows two lines: CoT (dashed orange) and Logic-LM (solid green). Accuracy is on the y-axis (55 to 85), Rounds is on the x-axis (0 to 3). For Logic-LM (GPT-4), the accuracy values are: 79.9% at round 0, 85.3% at round 1, 85.3% at round 2, and 85.3% at round 3. The text below the figure states: "For an in-depth analysis, we then evaluate the accuracy and Exe_Rate across different rounds of self-refinement on FOLIO, namely, 0 (no refinement), 1, 2, and 3 rounds. The results are in Figure 4."

Text: "In LOGIC-LM, multi-step logical reasoning is delegated to external symbolic solvers, thereby transitioning the challenge of LLM from problem-solving to problem representation. Ideally, the complexity of formally representing a problem statement in logical form should remain relatively constant, regardless of whether the questions require simple or complex reasoning. The trends in Figure 3 validate this assumption. The performance of Standard and CoT declines precipitously with the escalation of problem complexity. However, this trend is less prominent for LOGIC-LM, indicating that the robust reasoning capabilities provided by external solvers substantially mitigate performance degradation for complex reasoning problems."

Text: "We find that as the rounds of self-refinement increase, the percentage of executable formulations consistently increases, leading to an enhancement in the final performance. This suggests that self-refinement serves as an effective tool in aiding the LLM to accurately frame the problem. However, the accuracy tends to stagnate in subsequent rounds, even though the Exe_Rate continues to increase. This can be attributed to the type of feedback received by the self-refiner, which is the error message."

## Turn 3 — document page 9 (rank 3 of 19)

none

## Turn 4 — document page 10 (rank 4 of 19)

none

## Turn 5 — document page 6 (rank 5 of 19)

none

## Turn 6 — document page 2 (rank 6 of 19)

none

## Turn 7 — document page 1 (rank 7 of 19)

none

## Turn 8 — document page 3 (rank 8 of 19)

Figure 2: Overview of our LOGIC-LM model, which consists of three modules: (1) Problem Formulator generates a symbolic representation for the input problem with LLMs via in-context learning (2) Symbolic Reasoner performs logical inference on the formulated problem, and (3) Result Interpreter interprets the symbolic answer.

Text: "address this, recent work has begun to augment language models with access to external tools and resources, such as the information retriever (Nakano et al., 2021; Shi et al., 2023; Lazaridou et al., 2022), calculator (Cobbe et al., 2021), code interpreter (Wang et al., 2022), planner (Liu et al., 2023a), and other pre-trained models (Shen et al., 2023). Recent works (Gao et al., 2023; Chen et al., 2022) have achieved improved performance on arithmetic reasoning tasks by generating Python programs that specify the reasoning procedure as chained commands in the order of execution. However, this idea has not been extended to logical reasoning problems, primarily due to the challenge of representing their highly “non-linear” reasoning procedure (e.g., hypothesizing, case-by-case analysis, and the process of elimination) with functional programming. Our work provides a novel way to solve this within the framework of augmented LLMs. Instead of parsing the problem-solving procedure as programs, we only describe the problem with symbolic language using LLMs and then offload the reasoning to external symbolic solvers."

Text: "Auto-Formalization. The concept of converting natural language into symbolic representations has been widely adopted in auto-formalization for mathematical reasoning (Wu et al., 2022; Drori et al., 2022; He-Yueya et al., 2023; Jiang et al., 2023). These works demonstrate the proficiency of LLMs in translating a considerable fraction of mathematical problems into formal specifications defined in tools like SymPy (Meurer et al., 2017), Isabelle/HOL (Paulson, 1994), and Lean (de Moura et al., 2015). Mathematical reasoning can be considered a specialized subset of logical reasoning, primarily focused on numeric deductions. Due to this numeric specificity, mathematical problems are often more readily translatable to symbolic forms. In contrast, logical reasoning covers a wider array of problem types, often requiring a deeper understanding of world knowledge and commonsense for effective parsing into symbolic forms. Despite plenty of works studying mathematical reasoning, our work pioneers in extending the concept of autoformalization to a broader range of logical reasoning tasks with modern LLMs."

Text: "3 LOGIC-LM As shown in Figure 2, the inputs of our model are a logical reasoning problem P described in natural language, along with a goal G in the form of a multiple-choice or free-form question. LOGIC-LM then follows a problem formulation-and-reasoning paradigm to solve the problem."

## Turn 9 — document page 11 (rank 9 of 19)

none

## Turn 10 — document page 14 (rank 10 of 19)

none

## Turn 11 — document page 5 (rank 11 of 19)

Table 1 summarizes the four types of logical reasoning problems, their typical datasets, and the symbolic formulation used to represent each type. The table also gives an example of a natural language statement with its corresponding symbolic formulation for each type. The datasets mentioned are ProntoQA, ProofWriter (for LP), FOLIO (for FOL), LogicalDeduction (for CSP), and AR-LSAT (for SAT). The table does not provide any information about the performance of Logic-LM or any baseline models on these datasets.

## Turn 12 — document page 12 (rank 12 of 19)

none

## Turn 13 — document page 4 (rank 13 of 19)

none

## Turn 14 — document page 18 (rank 14 of 19)

This page contains examples of prompts for different prompting methods (Standard In-Context Learning, Chain-of-Thought Prompting, and Logic-LM) applied to AR-LSAT problems. It also describes the implementation of the Result Interpreter for different datasets, including AR-LSAT, where the method attempts to separately prove each option to find the correct answer. The page provides specific examples for each prompting method, including the problem context, question, options, and the Logic-LM's symbolic formulation for one of the AR-LSAT problems. However, it does not contain any performance metrics or comparison data for Logic-LM against baseline models on the AR-LSAT dataset.

## Turn 15 — document page 17 (rank 15 of 19)

This page contains examples of prompts for different prompting methods (Standard In-Context Learning, Chain-of-Thought Prompting, and Logic-LM) applied to Logical Deduction problems. It shows the problem context, question, options, and the Logic-LM's symbolic formulation for one of the Logical Deduction problems. The page provides specific examples for each prompting method, including the problem context, question, options, and the Logic-LM's symbolic formulation for one of the Logical Deduction problems. However, it does not contain any performance metrics or comparison data for Logic-LM against baseline models on the Logical Deduction dataset.
