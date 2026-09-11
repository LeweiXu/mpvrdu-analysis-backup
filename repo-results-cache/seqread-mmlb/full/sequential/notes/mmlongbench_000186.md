## Turn 1 — document page 9 (rank 1 of 20)

Table 3: Overall results of LLM-based ICL methods, SLM-based supervised methods, and our proposed filter-then-rerank (SLM+LLM) methods. The best results are in bold face and the second best are underlined. All results except InstructGPT and GPT-4 are averaged over 5 runs, and sample standard deviations are in the round bracket.
| | FewNERD (NER) | | | TACREV (RE) | | | ACE (ED) | | |
|---|---|---|---|---|---|---|---|---|---|
| | 5-shot | 10-shot | 20-shot | 20-shot | 50-shot | 100-shot | 5-shot | 10-shot | 20-shot |
| LLM | CODEX | 53.8(0.5) | 54.0(1.4) | 55.9(0.5) | 59.1(1.4) | 60.3(2.4) | 62.4(2.6) | 47.1(1.2) | 47.7(2.8) | 47.9(0.5) |
| | InstructGPT | 53.6(-) | 54.6(-) | 57.2(-) | 60.1(-) | 58.3(-) | 62.7(-) | 52.9(-) | 52.1(-) | 49.3(-) |
| | GPT-4 | - | - | 57.8(-) | - | - | 59.3(-) | - | - | 52.1(-) |
| SLM | Previous SoTA | 59.4(1.5) | 61.4(0.8) | 61.9(1.2) | 62.4(3.8) | 68.5(1.6) | 72.6(1.5) | 55.1(4.6) | 63.9(0.8) | 65.8(2.0) |
| | + Ensemble (S) | 59.6(1.7) | 61.8(1.2) | 62.6(1.0) | 64.9(1.5) | 71.9(2.2) | 74.1(1.7) | 56.9(4.7) | 64.2(2.1) | 66.5(1.7) |
| | + Rerank (S) | 59.4(1.5) | 61.0(1.7) | 61.5(1.7) | 64.2(2.3) | 70.8(2.3) | 74.3(2.2) | 56.1(0.3) | 64.0(1.0) | 66.7(1.7) |
| | Vicuna-13B | | | | | | | | | |
| | + Rerank (L) | 60.0(1.8) | 61.9(2.1) | 62.2(1.4) | 65.2(1.4) | 70.8(1.6) | 73.8(1.7) | 56.9(4.0) | 63.5(2.7) | 66.0(2.6) |
| | + Ensemble (S) + Rerank (L) | 59.9(0.7) | 62.1(0.7) | 62.8(1.1) | 66.5(0.5) | 73.6(1.4) | 75.0(1.5) | 57.9(5.2) | 64.4(1.2) | 66.2(2.4) |
| | InstructGPT | | | | | | | | | |
| | + Rerank (L) | 60.6(2.1) | 62.7(0.8) | 63.3(

## Turn 2 — document page 8 (rank 2 of 20)

Figure 6: The overall architecture of our adaptive filter-then-rerank paradigm. We color easy samples in orange and hard samples in pink. For easy samples, the final predictions are exactly from the SLM-based methods. For hard samples, the top-N predictions from SLMs are fed into LLMs as the format of multiple-choice questions (pink box). The question is paired with demos (green box). LLMs rerank these N candidates and generate the final prediction.

Text describing the method: filter, and Vicuna-13B, InstructGPT or GPT-4 as the reranker. The threshold τ to determine sample difficulty is optimized on the valid set. For hard sample, the top-3 SLM predictions and None (if not included) are feed to LLMs for reranking. Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1. We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2. We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Baseline: We compare our method with two kinds of baselines to validate its effectiveness.
(1) LLMs with ICL: We follow the prompts in Section 3.3 and conduct experiments on three LLMs.
(2) Supervised SLMs: We follow previous SoTA methods shown in Section 3.4 (FSLS or Know-Prompt). We additionally combine two SLMs with ensemble or reranking approach (i.e., replace the LLM with another SLM as the reranker) to verify that improvements from our SLM-LLM integrated system are not solely due to the ensemble effects.

5.3 Main Results
Table 3 shows that our filter-then-rerank method consistently improves performance across three datasets and nine settings. For instance, with InstructGPT, reranking provides an average F1 gain of 2.4% without SLM ensemble (Lines 4 vs. 7). Based on ensemble SLMs as the filter, our method still achieves 2.1% (Lines 5 vs. 8) gains on average. This confirms (1) the effectiveness of the LLM reranking and (2) its gains are different and (almost) orthogonal to the SLM ensemble.

5.4 Analysis
Few makes big difference Our method selectively reranks hard samples. Table 4 shows that (1) only a minor fraction (0.5%~10%) of samples are deemed hard and are reranked by LLMs. (2) Despite their limited quantity, reranking results in a substantial performance boost on these samples (10%~25% absolute F1 gains). This uplift on a small subset significantly enhances the overall performance.

GPT-4 is more aggressive From Tables 3 and 4, GPT-4 generally improves more on hard samples, yet InstructGPT surpasses GPT-4 in NER and RE tasks when evaluated overall. This discrepancy arises from GPT-4's aggressive reranking which introduces more true positives. InstructGPT, however, focuses more on reducing false positives.

Few makes small cost Figure 7 demonstrates that our method impressively reduces budget and latency by approximately 80%~90% compared to direct ICL. This reduction is due to (1) fewer LLM callings (only for hard samples) and (2) shorter prompts (fewer candidate labels and demos).

5.5 Ablation Study
We investigate the effectiveness of the modules in adaptive filter-then-rerank system by removing each of them in turn: (1) CoT: We exclude the explanation for each examples in demo. (2) Demo:

## Turn 3 — document page 7 (rank 3 of 20)

Figure 5: Relationship between confidence scores and performance with/without LLM reranking. We adopt RoBERTa-large as filter and InstructGPT as reranker.
We conduct experiments to confirm our hypothesis that LLMs excel on hard samples. We group samples by confidence scores and compare two methods within each group: (a) SLM-based methods without LLM reranking, and (b) SLMs as the filter and LLMs as the reranker. Method (b) differs from (a) by adding a single LLM to rerank the top-N SLM predictions, using MCQ prompts.
The results in Figure 5 substantiate our assumption. (1) LLM-based reranking (blue lines) enhances performance on hard samples (left areas in the figure). We provide a detailed analysis of specific challenging instances where LLM rerankers prove advantageous in Appendix F.1. These instances demonstrate the efficacy of LLMs in harnessing external knowledge and complex reasoning to rectify erroneous predictions initially made by SLMs (red lines). (2) Conversely, LLM-based reranking impedes performance on easy samples (right areas), resulting in a significant degradation, particularly for very easy samples (rightmost areas). In conclusion, LLMs exhibit greater proficiency in handling hard samples compared to SLMs, yet they underperform relative to SLMs on easy samples.

Table 2: Comparative ratios of negative to positive samples across various datasets and subsets. We set fixed threshold τ here for simplicity.
| | FewNERD | TACREV | ACE05 |
|---|---|---|---|
| Overall | 5.88 | 3.03 | 38.2 |
| Easy samples (τ > 0.9) | 9.44 | 3.21 | 44.0 |
| Hard samples (τ < 0.6) | 1.28 | 2.68 | 1.36 |

Text: We conduct experiments to confirm our hypothesis that LLMs excel on hard samples. We group samples by confidence scores and compare two methods within each group: (a) SLM-based methods without LLM reranking, and (b) SLMs as the filter and LLMs as the reranker. Method (b) differs from (a) by adding a single LLM to rerank the top-N SLM predictions, using MCQ prompts.
The results in Figure 5 substantiate our assumption. (1) LLM-based reranking (blue lines) enhances performance on hard samples (left areas in the figure). We provide a detailed analysis of specific challenging instances where LLM rerankers prove advantageous in Appendix F.1. These instances demonstrate the efficacy of LLMs in harnessing external knowledge and complex reasoning to rectify erroneous predictions initially made by SLMs (red lines). (2) Conversely, LLM-based reranking impedes performance on easy samples (right areas), resulting in a significant degradation, particularly for very easy samples (rightmost areas). In conclusion, LLMs exhibit greater proficiency in handling hard samples compared to SLMs, yet they underperform relative to SLMs on easy samples.

## Turn 4 — document page 21 (rank 4 of 20)

This page contains case studies (Case 3 and Case 4) illustrating how LLMs can make errors in NER and ED tasks, particularly with subspan predictions and boundary mismatching. It also introduces Section G, which details the demonstration examples and templates for the filter-then-rerank paradigm. However, it does not contain any new performance metrics or results for the filter-then-rerank method on the 50-shot TACREV dataset.

## Turn 5 — document page 10 (rank 5 of 20)

none

## Turn 6 — document page 2 (rank 6 of 20)

The current page discusses the proposed filter-then-rerank framework and its performance. It states: "With a modest cost increase, our framework yields a consistent F1 improvement, averaging 2.4% higher than previous methods on various few-shot IE tasks." This is reiterated in section 2.2: "our framework yields a consistent F1 improvement, averaging 2.4% higher than previous methods on various few-shot IE tasks." The text also mentions that this is the first successful attempt to use LLMs to enhance few-shot IE tasks. However, this page does not specify the exact performance on the 50-shot TACREV dataset, nor does it specify whether the 2.4% improvement is for the method without ensemble or with ensemble. The specific performance value for the 50-shot TACREV dataset is found in Table 3 on page 9, which is not on the current page.

## Turn 7 — document page 19 (rank 7 of 20)

none
