## Turn 1 — document page 2 (rank 1 of 20)

The current page contains a detailed example question from the CLADDER dataset, which is about a hypothetical world with specific causal relationships and probabilities. The question asks whether getting vaccinated increases the likelihood of death. The page provides a step-by-step solution to this question, including:

- The causal graph is parsed, identifying "Physical vulnerability" as a confounder.
- The query type is classified as "Average Treatment Effect".
- The query is formulated symbolically as: E[Y | do(X=1)] - E[Y|do(X = 0)].
- The available data is collected, which includes:
  - P(Z=1) = 0.5 (50% of the population is vulnerable).
  - P(Y=1|Z=1,X=1) = 0.04 (fatality rate for vulnerable and vaccinated people).
  - P(Y=1|Z=1,X=0) = 0.07 (fatality rate for vulnerable and unvaccinated people).
  - P(Y=1|Z=0,X=1) = 0.01 (fatality rate for strong and vaccinated people).
  - P(Y=1|Z=0,X=0) = 0.058 (fatality rate for strong and unvaccinated people).
  - P(Y=1|X=1) = 0.05 (overall fatality rate for vaccinated people).
  - P(Y=1|X=0) = 0.045 (overall fatality rate for unvaccinated people).
- The estimand is derived using causal inference, resulting in the expression: 0.5*(0.01 - 0.058) + 0.5*(0.04 - 0.07).
- The final calculated effect size is -0.039, which is negative, leading to the conclusion that getting vaccinated does not increase the likelihood of death.

The page also discusses the CLADDER dataset and the CAUSALCOT method for eliciting causal reasoning in LLMs.

## Turn 2 — document page 22 (rank 2 of 20)

- Step ④ Collect all the available data: The available data are: "d".
- Step ⑤ Derive the estimand: Based on the graph structure and causal query, the question can be simplified into estimand "est".
- Step ⑥ Solve for the estimand: Plug in the available data "d" into "est".
est(d)
≈ float(a)
Since the estimate for the estimand is float(a), the overall answer to the question is bool(a).

B Experimental Details
B.1 CAUSALCOT Prompt
Step 4) Gather all relevant data: Extract all the available data. Your answer should contain nothing but marginal probabilities and conditional probabilities in the form "P(...)=..." or "P(...|...) =...", each probability being separated by a semicolon. Stick to the previously mentioned denotations for the variables.
Step 5) Deduce the estimand using causal inference: Given all the information above, deduce the estimand using skills such as do-calculus, counterfactual prediction, and the basics of probabilities. Answer step by step.
Step 6) Calculate the estimand: Insert the relevant data in Step 4 into the estimand, perform basic arithmetic calculations, and derive the final answer. There is an identifiable answer. Answer step by step.

## Turn 3 — document page 6 (rank 3 of 20)

The current page identifies six subskills necessary for causal inference, which are evaluated individually in the step-by-step explanations. These subskills are:
① causal graph extraction;
② correct query type interpretation;
③ symbolic formalization of the query;
④ semantic parsing to compile the available data;
⑤ estimand derivation;
⑥ arithmetic calculation to solve the estimand.

The page also describes the verbalization of prompts and explanations, including how each subskill is verbalized and how the available data is compiled using semantic parsing.

## Turn 4 — document page 7 (rank 4 of 20)

- The current page describes the CAUSALCOT model and its multi-step reasoning process for causal inference.
- It outlines six subskills required for causal inference: ① causal graph extraction; ② correct query type interpretation; ③ symbolic formalization of the query; ④ semantic parsing to compile the available data; ⑤ estimand derivation; ⑥ arithmetic calculation to solve the estimand.
- The page includes Figure 4, which visually represents the CAUSALCOT prompting strategy, showing a preparation phase (Steps 1-4) and a solution phase (Steps 5-6).
- Step 4 in the preparation phase is explicitly labeled as "Gather all relevant data," which involves extracting available data from the prompt.
- The text confirms that Step 4 is about "extracting relevant data from the prompt," which aligns with the subskill of semantic parsing to compile the available data.

## Turn 5 — document page 5 (rank 5 of 20)

- The page defines "data" as numerical values of conditional or do-probabilities, not collections of data samples.
- It explains the process of constructing inputs to the CI Engine, ensuring identifiability by design.
- The page describes how causal queries, graphs, and data are constructed to have a well-defined ground truth answer.
- It mentions that the estimand specifies exactly which terms are necessary to include in the prompt as “available data” to ensure identifiability.
- The page discusses generating stories and verbalizing formal queries and specifications using narratives and templates.
- It references the use of causal Bayesian networks (CBNs) and the application of do-calculus and counterfactual causal inference.

## Turn 6 — document page 19 (rank 6 of 20)

This page is supplementary material for dataset generation and lists references for causal inference (books and papers) and introduces query types (Rung-1: Marginal and Conditional Probabilities). It includes Figure 6 showing causal graphs with treatment-effect pairs (CGTEs) and their aliases (e.g., Confounding, Mediation, Fork, Collision, etc.). The page does not contain any information about subskills required to collect available data.

## Turn 7 — document page 21 (rank 7 of 20)

This page contains Table 4, which lists text templates for different query types in causal inference. It categorizes queries into three rungs: Association (Rung 1), Intervention (Rung 2), and Counterfactuals (Rung 3). The table includes symbolic expressions and natural language question templates for each query type. However, this page does not contain any information about the subskills required to collect available data.

## Turn 8 — document page 4 (rank 8 of 20)

- The page describes the Causal Inference Engine (CI Engine), which takes as input a query, a graph, and some available data (typically from lower rungs than the query) and outputs whether a solution exists and, if so, an equivalent expression of the query estimable from the available data.
- The page mentions that the CI Engine is used to generate ground truth answers for the CLADDER dataset, which consists of triples (question, binary answer, explanation).
- The design principles for the dataset include ensuring broad coverage of all rungs of the ladder of causation, using binary variables, focusing on graphs with few variables, and designing rich templates for natural-sounding prompts.
- The generation pipeline for CLADDER consists of a formal part (specifying inputs and ground truth) and a natural language part (verbalizing the question).
