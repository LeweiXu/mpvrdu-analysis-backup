## Turn 1 — document page 15 (rank 1 of 20)

Table 6: Statistics of nine datasets used. Note that the #mentions for event detection tasks refers to the number of trigger words, while the #mentions for event argument extraction tasks refers to the number of arguments.
| Dataset | Named Entity Recognition | Relation Extraction | Event Detection | Event Arg Extraction |
| --- | --- | --- | --- | --- |
|  | CONLL OntoNotes FewNERD | TACREV TACRED | ACE05 MAVEN ERE | ACE05 RAMS ERE |
| #Label Type | 4 18 66 | 41 41 | 33 168 38 | 33 139 38 |
| #Sents | 14,041 49,706 131,965 | 68,124 68,124 | 14,024 32,360 14,736 | 14,024 7329 14,736 |
| #Mentions | 23,499 128,738 340,247 | 13,012 13,012 | 5,349 77,993 6,208 | 4,859 17,026 8,924 |

Table 7: The statistics of few-shot training sets. We set different random seeds and generate 5 training sets for each setting. We report their average statistics.
| Dataset Settings | # Labels | # Sent | # Sample | # Avg shot |
| --- | --- | --- | --- | --- |
| CONLL'03 | 4 | 4.8 16.2 29.2 65.6 | 5.8 21.8 42.6 82.0 | 1.4 5.5 10.7 20.5 |
| OntoNotes | 18 | 20.0 84.8 158.6 332.8 | 33.4 148.0 281.0 547.2 | 1.9 8.2 15.6 30.4 |
| FewNERD | 66 | 89.8 286.2 538.0 1027.2 | 147.0 494.8 962.0 1851.4 | 2.2 7.5 14.6 28.1 |
| TACREV | 41 | 81.6 387.6 741.2 1367.2 | 41.0 205.0 406.0 806.0 | 1.0 5.0 9.9 19.7 |
| TACRED | 41 | 81.6 387.6 741.2 1367.2 | 41.0 205.0 406.0 806.0 | 1.0 5.0 9.9 19.7 |
| ACE05 | 33 | 47.4 192.8 334.6 213.4 | 41.0 165.0 319.4 630.2 | 1.2 5.0 9.7 19.1 |
| MAVEN | 168 | 579.4 157.6 540.4 1286.4 | 598.2 1262.2 1262.2 4611.4 | 18.1 1.8 7.5 27.4 |
| ERE | 38 | 48.4 175.0 304.8 521.6 | 54.6 219.2 432.4 806.6 | 1.4 5.8 11.4 21.2 |
| ACE05 | 33 | 23.4 79.8 130.8 213.4 | 40.

## Turn 2 — document page 1 (rank 2 of 20)

In the Introduction section, the text states: "We fairly evaluate SLMs-based and LLMs-based methods across nine datasets spanning four common IE tasks: (1) Named Entity Recognition, (2) Relation Extraction, (3) Event Detection and (4) Event Argument Extraction." This indicates that the experiments are conducted on nine datasets.

## Turn 3 — document page 2 (rank 3 of 20)

In section 3.1 "Task, Dataset and Evaluation" on page 2, the text explicitly states: "We run experiments on nine widely-used datasets across four IE tasks." This is corroborated by Table 6 on page 1, which lists nine datasets (CONLL03, OntoNotes, FewNERD, TACRED, TACREV, ACE05, MAVEN, ERE, and another ACE05 which is likely a duplicate or error in the table but the text confirms nine distinct datasets).

## Turn 4 — document page 14 (rank 4 of 20)

## A.1 Full Datasets
The text states: "We construct few-shot IE datasets and conduct the empirical study on nine datasets spanning four tasks, with varying schema complexities ranging from 4 to 168. We show their statistics in Table 6."

## A.2 Details of Few-shot IE Datasets
The text confirms the use of nine datasets: "We downsample sentences from original training dataset to construct few-shot training and valid datasets. We adopt K-shot sampling strategy that each label has (at least) K samples. We set 6 K-values (1, 5, 10, 20, 50, 100) for RE tasks and 4 K-values (1, 5, 10, 20) for other tasks. For RE task, each sentence has exactly one relation and we simply select K sentences for each label. For NER, ED and EAE tasks, each sentences is possible to contain more than one entities/events/arguments. Since our sampling is at sentence-level, the algorithm of accurate sampling, i.e., finding exactly K samples for each label, is NP-complete and unlikely to find a practical solution. Therefore we follow Yang and Katiyar (2020) adopting a greedy sampling algorithm to select sentences for NER and ED tasks, as shown in Algorithm 1. Note that the actual sample number of each label can be larger than K under this sampling strategy. For all three tasks, we additionally sample negative sentences (without any defined labels) and make the ratio of positive sentences (with at least one label) and negative sentences as 1:1. The statistics of the curated datasets are listed in Table 7."

## Turn 5 — document page 19 (rank 5 of 20)

This page contains experimental results and details about prompt formats and demo selection strategies, but it does not introduce any new datasets or contradict the previously established count of nine datasets. The tables (Table 13, Table 14) refer to specific datasets (FewNERD, TACREV, ACE) which are part of the nine datasets already identified in earlier pages. The text discusses experiments on these datasets but does not add or remove any from the total count.

## Turn 6 — document page 7 (rank 6 of 20)

Table 2: Comparative ratios of negative to positive samples across various datasets and subsets. We set fixed threshold τ here for simplicity.
| Dataset | Overall | Easy samples (τ > 0.9) | Hard samples (τ < 0.6) |
| --- | --- | --- | --- |
| FewNERD | 5.88 | 9.44 | 1.28 |
| TACREV | 3.03 | 3.21 | 2.68 |
| ACE05 | 38.2 | 44.0 | 1.36 |

The text in section 5.2 "Experimental Setup" states: "We conduct experiments on FewNERD for NER task, TACREV for RE task and ACE05 for ED task." This confirms the use of three specific datasets for the experiments described in this section, but does not contradict or add to the previously established total count of nine datasets.

## Turn 7 — document page 4 (rank 7 of 20)

Figure 2 presents results across four IE tasks: (a) Named Entity Recognition (NER), (b) Relation Extraction (RE), (c) Event Detection (ED), and (d) Event Argument Extraction (EAE). Each subplot corresponds to a specific dataset: CONLL03 for NER, OntoNotes for RE, ACE05 for ED, and RAMS for EAE. The figure caption explicitly states that these results are shown for "nine datasets across four IE tasks." The subplots also show results for other datasets like FewNERD (NER), TACREV (RE), MAVEN (ED), and ERE (EAE), confirming the use of multiple datasets per task. The text below the figure confirms the use of specific models and datasets, but does not alter the total count of nine datasets.
