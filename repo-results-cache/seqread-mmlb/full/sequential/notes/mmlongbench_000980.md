## Turn 1 — document page 25 (rank 1 of 20)

Table 6: Performance of all models on our CLADDER dataset v1.0. We report the overall accuracy (Acc.), and also fine-grained accuracy by rung and by empirical alignment.
We compare the performance of all models in Table 6. First, we can see that the causal reasoning task in CLADDER is in general very challenging for all models. And models such as the earlier, non-instruction-tuned GPT-3 and both LLaMa and Alpaca are no better than random performance. With instruction-tuning, models start to show some improvement. And amongst all, our CAUSALCOT achieves the highest performance of 66.64%, which is 2.36 points better than vanilla GPT-4.
Moreover, from the accuracy by empirical alignment level in Table 6, we can see that the original GPT-4 model performs the best on commonsensical data, but 5.34 points worse on nonsensical data. However, our CAUSALCOT enhances the reasoning ability across all levels, with substantial improvement on anti-commonsensical data and nonsensical data, indicating that CAUSALCOT is particularly beneficial on unseen data.
Table 7: Ablation study.
E More Experiments
E.1 Details of Our Error Analysis
For Step 2 about the query type prediction, we report the overall F1 classification score, and also F1 by rungs. For the rest of the steps, we manually annotate the correctness of 100 samples of CAUSALCOT. We report the correctness of est by accuracy, and the correctness of the predicted set of available data by taking the F1 with the ground-truth d. For Step 5, we report the accuracy of whether the model simplifies the estimand correctly to est' using causal inference, and also arithmetic correctness (Arith.).
E.2 ROSCOE Evaluation
We employed the ROSCOE suite of evaluation metrics on step-by-step text reasoning, as introduced by  \( [25] \) , to automate the evaluation of the outputs from CAUSALCOT on 2,000 randomly sampled questions from our dataset. Differing from conventional metrics, ROSCOE is specifically designed to scrutinize the quality of large language model outputs, focusing on aspects such as semantic consistency, logicality, informativeness, fluency, and factuality, all evaluated within the context of step-by-step reasoning, rather than solely the final response. This allows for a more objective and comprehensive assessment of a model's output, greatly aiding in the verification of its interpretability. The results of this evaluation can be found in Table 8 and Figure 9. We consider the model's performance as unsatisfying if it falls out of the top quantile, namely receiving a score  \( s \in [0, 1] \)  smaller than 0.25 when the score should be minimized, or greater than 0.75 when it should be maximized.

## Turn 2 — document page 8 (rank 2 of 20)

Table 2 on page 8 shows the performance of all models on CLADDER dataset v1.5. The row labeled "+ CAUSALCOT" has an "Overall Acc." of 70.40%, which is the highest among all models. The text explicitly states, "amongst all, our CAUSALCOT achieves the highest performance of 70.40%".

## Turn 3 — document page 7 (rank 3 of 20)

This page describes the CAUSALCOT model, its design inspired by causal inference engines, and its multi-step prompting strategy. It details the preparation and solution phases for solving CLADDER questions, including identifying causal graphs, determining query types, formalizing queries, extracting data, deducing estimands using causal inference, and evaluating them. The page also includes a figure illustrating the CAUSALCOT prompting strategy. However, this page does not contain any performance metrics or comparisons with other models on the CLADDER dataset.

## Turn 4 — document page 2 (rank 4 of 20)

This page presents an example question from the CLADDER dataset, illustrating a case of Simpson's paradox. It details the correct step-by-step reasoning process to derive the ground-truth answer "No" to the question "Does getting vaccinated increase the likelihood of death?". The steps include parsing the causal graph, classifying the query type, formulating the query symbolically, collecting available data, deriving the estimand using causal inference, and solving for the estimand. The page also explains the motivation for creating CLADDER: to test formal causal reasoning in LLMs, distinguishing it from previous work that focused on commonsense causality. It introduces CAUSALCOT as a chain-of-thought prompting strategy designed to elicit sound causal reasoning in LLMs by guiding them through the steps of causal inference. The page does not contain any performance metrics or comparisons of models on the CLADDER dataset.

## Turn 5 — document page 1 (rank 5 of 20)

This page is the title page and introduction of the paper "CLADDER: Assessing Causal Reasoning in Language Models". It introduces the CLADDER dataset and the CAUSALCOT prompting strategy. It discusses the importance of causal reasoning and the goal of the paper: to evaluate whether LLMs can perform causal inference according to formal rules. It mentions that the task is highly challenging for LLMs. However, this page does not contain any performance metrics or comparisons of models on the CLADDER dataset.

## Turn 6 — document page 27 (rank 6 of 20)

This page contains Table 9, which compares the CLADDER dataset with other causal or reasoning datasets. It categorizes datasets by question types (Association, Intervention, Counterfactual) and skill types (Formalization of Causal Queries, Causal RE, Qualitative Reasoning). CLADDER is shown to cover all three question types and all three skill types, making it comprehensive for testing formal causal reasoning. However, this page does not contain any performance metrics or comparisons of models on the CLADDER dataset.
