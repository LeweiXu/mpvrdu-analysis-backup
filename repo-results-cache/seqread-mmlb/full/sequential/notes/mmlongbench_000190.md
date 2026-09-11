## Turn 1 — document page 8 (rank 1 of 20)

Figure 6: The overall architecture of our adaptive filter-then-rerank paradigm. We color easy samples in orange and hard samples in pink. For easy samples, the final predictions are exactly from the SLM-based methods. For hard samples, the top-N predictions from SLMs are fed into LLMs as the format of multiple-choice questions (pink box). The question is paired with demos (green box). LLMs rerank these N candidates and generate the final prediction.

Text: filter, and Vicuna-13B, InstructGPT or GPT-4 as the reranker. The threshold τ to determine sample difficulty is optimized on the valid set. For hard sample, the top-3 SLM predictions and None (if not included) are feed to LLMs for reranking. Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1. We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2. We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We follow the prompts in Section 3.3 and conduct experiments on three LLMs.

Text: We follow previous SoTA methods shown in Section 3.4 (FSLS or Know-Prompt).

Text: We additionally combine two SLMs with ensemble or reranking approach (i.e., replace the LLM with another SLM as the reranker) to verify that improvements from our SLM-LLM integrated system are not solely due to the ensemble effects.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-th

## Turn 2 — document page 21 (rank 2 of 20)

In our filter-then-rerank paradigm, we utilize templates converting candidate labels to question options. We list the template for FewNERD dataset in Table 19, for TACREV dataset in Table 20, and for ACE05 datasets in Table 21.

## Turn 3 — document page 6 (rank 3 of 20)

Figure 4: Multi-choice question (MCQ) prompt.
Read Following sentences and identify what is the entity type of "The New Yorker" quoted by <t>.
Sentence:
In 2004 Gourevitch was assigned to cover the 2004 U.S. presidential election for “<t> The New Yorker <t>”.
Candidate Choices:
(a)The New Yorker does not belong to any known entities.
(b)The New Yorker is a broadcast program.
(c)The New Yorker is a kind of written art.
(d)The New Yorker is a media/newspaper organization.
Analysis:
The New Yorker is a well-known American magazine that has been published since 1925, and is primarily known for its long-form journalism, commentary, and satire. It has a reputation for publishing high-quality writing on a wide variety of topics, including politics, culture, and the arts. So The New Yorker is a media/newspaper organization.
Correct Answer: (d)

Text: To mitigate LLMs' drawbacks mentioned above, we propose a filter-then-rerank paradigm to integrate both SLMs and LLMs within the same system. This paradigm uses SLMs as filters to select the top-N candidate labels, then LLMs rerank them to make final decisions. By using SLM-generated candidate answers, the focus of LLMs shifts from sentence-level (i.e., identifying all entities/events in the sentence) to sample-level (i.e., determining single entity/event candidate provided). Each question now corresponds to a single sample, allowing us to reframe prompts as multi-choice questions (MCQ; shown in Figure 4) problem. Under such format, each candidate label is converted to a choice by pre-defined templates.

Text: We claim filter-then-rerank paradigm is more likely to elicit the powers of LLMs and smoothly solve few-shot IE tasks because: (1) LLMs are more familiar with MCQ prompts than IE-format prompts (Zhang et al., 2023a). (2) This paradigm reduces the label scopes significantly, since N is usually much smaller than fine-grained label numbers.

Text: Figure 4: Multi-choice question (MCQ) prompt.

Text: Each candidate label is converted to a choice by pre-defined templates.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022b), i.e., prefacing the answer with an explanation, to facilitate LLMs' reranking procedure.

Text: Each LLM prompt has 4-shot demos. See demo examples in Appendix G.1.

Text: We follow templates in Lu et al. (2022a) for TACREV and carefully design others. See these templates in Appendix G.2.

Text: We adopt chain-of-thought reasoning (Wei et al., 2022

## Turn 4 — document page 10 (rank 4 of 20)

none

## Turn 5 — document page 2 (rank 5 of 20)

none

## Turn 6 — document page 9 (rank 6 of 20)

none

## Turn 7 — document page 7 (rank 7 of 20)

Figure 5: Relationship between confidence scores and performance with/without LLM reranking. We adopt RoBERTa-large as filter and InstructGPT as reranker.
We conduct experiments to confirm our hypothesis that LLMs excel on hard samples. We group samples by confidence scores and compare two methods within each group: (a) SLM-based methods without LLM reranking, and (b) SLMs as the filter and LLMs as the reranker. Method (b) differs from (a) by adding a single LLM to rerank the top-N SLM predictions, using MCQ prompts.
The results in Figure 5 substantiate our assumption. (1) LLM-based reranking (blue lines) enhances performance on hard samples (left areas in the figure). We provide a detailed analysis of specific challenging instances where LLM rerankers prove advantageous in Appendix F.1. These instances demonstrate the efficacy of LLMs in harnessing external knowledge and complex reasoning to rectify erroneous predictions initially made by SLMs (red lines). (2) Conversely, LLM-based reranking impedes performance on easy samples (right areas), resulting in a significant degradation, particularly for very easy samples (rightmost areas). In conclusion, LLMs exhibit greater proficiency in handling hard samples compared to SLMs, yet they underperform relative to SLMs on easy samples.
4.3 Why LLMs Fail on Easy Samples
We investigate why LLMs (relatively) fail on easy samples in this section. As shown in Table 2, we observe significant higher negative sample ratios for easy samples across diverse IE tasks. In other
Table 2: Comparative ratios of negative to positive samples across various datasets and subsets. We set fixed threshold τ here for simplicity.
| | FewNERD | TACREV | ACE05 |
|---|---|---|---|
| Overall | 5.88 | 3.03 | 38.2 |
| Easy samples (τ > 0.9) | 9.44 | 3.21 | 44.0 |
| Hard samples (τ < 0.6) | 1.28 | 2.68 | 1.36 |
words, most negative samples are easy samples for SLMs. Here we refer negative samples to those labeled as None. We speculate that the proficiency of SLMs with negative samples stems from their ability to adeptly discern apparent patterns during the fine-tuning stages. Therefore, SLMs could predict negative samples with (relatively) high confidence and accuracy. Due to LLMs' predisposition to false-positive predictions on negative samples, however, the performance of LLMs on easy samples collapses. We attribute such false-positive predictions to (1) hallucination and (2) span boundary mismatch. We detail such two kinds of mistakes with cases in Appendix F.2.
5 Adaptive Filter-then-rerank Paradigm
Above findings can be summarized as: (1) SLMs generally outperform LLMs, especially with more training samples and fine-grained labels. (2) SLMs are much more time- and cost-efficient. (3) LLMs serve as powerful rerankers on hard samples that challenge SLMs. Based on them, we propose a simple, efficient, and effective adaptive reranker that combines the strengths of SLMs and LLMs.
5.1 Method
Our adaptive filter-then-rerank approach, shown in Figure 6, uses supervised SLMs as a filter to make preliminary decisions. Samples with confidence scores exceeding threshold are viewed as easy samples otherwise hard ones. For easy samples, we retain SLM predictions as final results. For hard samples, top-N predictions from SLMs are reranked via LLMs using ICL. Here LLMs employ MCQ prompts (Figure 4), containing demos and a sample to be reranked. The LLMs then generate the final answer and optionally provide an explanation.
5.2 Experimental Setup
We conduct experiments on FewNERD for NER task, TACREV for RE task and ACE05 for ED task. We employ top-performing SLM-based methods from Section 3 (FSLS or KnowPrompt) as the

## Turn 8 — document page 1 (rank 8 of 20)

none

## Turn 9 — document page 29 (rank 9 of 20)

Table 21: Templates for ACE05 dataset, where {evt} is the placeholder for event type.
| Event | Template |
|---|---|
| Contact.Meet | The word {evt} triggers a MEET event: two or more entities come together at a single location and interact with one another face-to-face. |

## Turn 10 — document page 20 (rank 10 of 20)

none

## Turn 11 — document page 19 (rank 11 of 20)

The current page contains tables and figures related to F1-scores across different demo-selection strategies and prompt formats, but it does not contain any information about the specific prompt template used for the label 'Contact.Meet' in the filter-then-rerank method. The relevant template for 'Contact.Meet' was found on page 29 (Turn 9), which states: "The word {evt} triggers a MEET event: two or more entities come together at a single location and interact with one another face-to-face."

## Turn 12 — document page 4 (rank 12 of 20)

The current page contains performance graphs for SLM-based and LLM-based methods across four IE tasks (NER, RE, ED, EAE) on nine datasets. It discusses instruction formats, demo selectors, and prompt formats. The prompt format for NER is given as “Sentence: [S], Entities: ([type1], [entity1]), ([type2], [entity2])...”, but no specific template for 'Contact.Meet' is provided on this page. The page does not contain any information about the prompt template for the 'Contact.Meet' label.

## Turn 13 — document page 3 (rank 13 of 20)

Figure 1 shows examples of prompts used for different Information Extraction (IE) tasks. The green part represents the instruction, the blue part represents the demonstration (demo), and the black part represents the test sentence. The red parts represent the outputs from LLMs. The figure includes examples for Named Entity Recognition (NER), Relation Extraction (RE), Event Detection (ED), and Event Argument Extraction (EAE). The prompt format for each task is shown in the figure, but the specific template for the 'Contact.Meet' label is not provided on this page.

## Turn 14 — document page 5 (rank 14 of 20)

The current page contains performance graphs and tables related to LLMs' performance across different prompt variants, instruction formats, demo numbers, and demo selection strategies. It discusses the impact of these variations on F1 scores for few-shot IE tasks. However, it does not contain any information about the specific prompt template used for the label 'Contact.Meet' in the filter-then-rerank method. The relevant template for 'Contact.Meet' was found on page 29 (Turn 9), which states: "The word {evt} triggers a MEET event: two or more entities come together at a single location and interact with one another face-to-face."
