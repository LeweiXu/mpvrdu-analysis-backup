## Turn 1 — document page 2 (rank 1 of 20)

The current page presents a hypothetical causal inference problem and its solution using the CLADDER dataset. It outlines a step-by-step reasoning process to determine whether vaccination increases the likelihood of death. The steps are numbered and include:

1. Parse the causal graph: Confounding Subskill: Causal Relation Extraction
2. Classify the query type: Average Treatment Effect Subskill: Causal Question Classification
3. Formulate the query to its symbolic form: E[Y | do(X=1)] - E[Y|do(X = 0)]
4. Collect the available data: P(Z=1)=0.5, P(Y=1|Z=1,X=1)=0.04, P(Y=1|Z=1,X=0)=0.07, P(Y=1|Z=0,X=1)=0.01, P(Y=1|Z=0,X=0)=0.058, P(Y=1|X=1)=0.05, P(Y=1|X=0)=0.045
5. Derive the estimand using causal inference: E[Y | do(X=1)] - E[Y|do(X=0)] = P(Z=0)*[P(Y=1|Z=0,X=1) - P(Y=1|Z=0,X=0)] + P(Z=1)*[P(Y=1|Z=1,X=1) - P(Y=1|Z=1,X=0)]
6. Solve for the estimand by plugging in the relevant data: = 0.5*(0.01 - 0.058)+0.5*(0.04-0.07) = -0.039 < 0, so the final answer is "No"

The text also mentions the "Ladder of Causation" with three rungs: associational (Rung 1), interventional (Rung 2), and counterfactual (Rung 3). The CLADDER dataset is designed to cover causal queries across these three rungs.

## Turn 2 — document page 22 (rank 2 of 20)

## A.8 Explanation Template
Step ① Extract the causal graph: The causal graph expressed in the context is: "G".
Step ② Identify the query type: The query type of the above question is "query_type".
Step ③ Formulate the query to its symbolic form: The formal form of the query is "symbolic_expression".
Step ④ Collect all the available data: The available data are: "d".
Step ⑤ Derive the estimand: Based on the graph structure and causal query, the question can be simplified into estimand "est".
Step ⑥ Solve for the estimand: Plug in the available data "d" into "est".

## B Experimental Details
B.1 CAUSALCOT Prompt
Guidance: Address the question by following the steps below:
Step 1) Extract the causal graph: Identify the causal graph that depicts the relationships in the scenario. The diagram should simply consist of edges denoted in "var1 -> var2" format, separated by commas.
Step 2) Determine the query type: Identify the type of query implied by the main question. Choices include "marginal probability", "conditional probability", "explaining away effect", "backdoor adjustment set", "average treatment effect", "collider bias", "normal counterfactual question", "average treatment effect on treated", "natural direct effect" or "natural indirect effect". Your answer should only be a term from the list above, enclosed in quotation marks.
Step 3) Formalize the query: Translate the query into its formal mathematical expression based on its type, utilizing the "do(·)" notation or counterfactual notations as needed.
Step 4) Gather all relevant data: Extract all the available data. Your answer should contain nothing but marginal probabilities and conditional probabilities in the form "P(...)=..." or "P(...|...) =...", each probability being separated by a semicolon. Stick to the previously mentioned denotations for the variables.
Step 5) Deduce the estimand using causal inference: Given all the information above, deduce the estimand using skills such as do-calculus, counterfactual prediction, and the basics of probabilities. Answer step by step.
Step 6) Calculate the estimand: Insert the relevant data in Step 4 into the estimand, perform basic arithmetic calculations, and derive the final answer. There is an identifiable answer. Answer step by step.

## Turn 3 — document page 7 (rank 3 of 20)

## 4 Our CAUSALCOT Model

The text describes a multi-step reasoning process for causal inference, illustrated in Figure 4. The process is divided into two main phases: a Preparation Phase and a Solution Phase.

The Preparation Phase consists of four steps:
1.  Extract the causal graph.
2.  Determine the query type.
3.  Formalize the query.
4.  Gather all relevant data.

The Solution Phase consists of two steps:
5.  Deduce the estimand using causal inference.
6.  Calculate the estimand to answer the question.

The text explicitly states: "We base our prompt design on the multi-step reasoning process of causal inference as shown in Figure 4, first starting with four preparation steps... Then, given all the information collected in the preparation stage, we introduce the formal solution: ⑤ correctly deducing the estimand... and finally ⑥ evaluating the estimand to answer the question."

## Turn 4 — document page 5 (rank 4 of 20)

This page discusses the formal part of question formulation for causal inference, including selecting query types for each rung of the Ladder of Causation (Rung 1: probability distributions; Rung 2: average treatment effects, adjustment sets; Rung 3: counterfactuals, ATT, NDE, NIE). It also describes applying the causal inference engine to derive estimands and ground truth answers. The page mentions the use of causal Bayesian networks (CBNs) and do-calculus, but does not list or describe the key steps of the causal inference process itself.

## Turn 5 — document page 13 (rank 5 of 20)

This page contains a bibliography with citations for various academic papers and books related to causal inference, counterfactual reasoning, and related topics. It includes references to works by Judea Pearl, Madelyn Glymour, Thomas A Glass, and others. However, this page does not contain any information about the number of key steps the author divided causal inference into.

## Turn 6 — document page 23 (rank 6 of 20)

This page provides technical background on causal inference, including graphical models, the causal ladder, and do-calculus. It describes the three rungs of the causal ladder (association, intervention, counterfactuals) and introduces do-calculus as a method to downgrade higher-rung queries to lower-rung quantities. The page details three inference rules for do-calculus but does not list or describe the key steps of the causal inference process itself. It references the causal inference framework from [61] but does not specify the number of steps the author divided causal inference into.
