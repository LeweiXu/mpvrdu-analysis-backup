## Turn 1 — document page 5 (rank 1 of 20)

Table 2: The function names, descriptions, and their proportions in our SCITAB dataset.
| Function Names | Descriptions | Prop. (%) |
| --- | --- | --- |
| Simple lookup | Retrieve the value for a specific cell. | 20.6 |
| Comparison | Compare two numbers. | 19.5 |
| Closed-domain knowledge | Extract information from context sentences in the table caption or article. | 12.1 |
| Open-domain knowledge | Extract additional information required by domain experts. | 5.3 |
| Commonsense knowledge | Extract commonsense knowledge necessary for claim verification. | 5.3 |
| Subtract | Perform subtraction of two numbers. | 5.3 |
| Divide | Perform division of two numbers. | 5.3 |
| Rank | Determine the rank of a set of numbers. | 5.3 |
| Different / Same | Determine if two numbers are different or the same. | 5.3 |
| Add | Calculate the sum of two numbers. | 4.0 |
| Max / Min | Retrieve the maximum or minimum number from a set of numbers. | 3.1 |
| Col / Rowname | Retrieve the column or row name from the table. | 3.1 |
| Trend same/different | Determine the trend for two columns or rows, whether they are the same or different. | 2.9 |
| Set check | Verify if a value belongs to a set of numbers. | 2.9 |

Figure 3: The distribution histogram of reasoning steps in our SCITAB dataset. The x-axis is the reasoning steps in each claim, and the y-axis is the frequency for each reasoning step. The shallow claims (with 1–2 reasoning steps) are highlighted in red, while the deep claims (with 3+ reasoning steps) are highlighted in blue.

## Turn 2 — document page 4 (rank 2 of 20)

Table 1: Comparison of SCITAB to three recent table fact verification datasets: TabFact (Chen et al., 2020), FEVEROUS (Aly et al., 2021), and SEM-TAB-FACTS (Wang et al., 2021). The table presents statistics related to the domain, annotator (AMT represents Amazon Mechanical Turk), maximum reasoning hops, veracity labels percentage of each dataset, the total number of claims, and average claims per table.
| Statistics | TabFact | FEVEROUS | SEM-TAB-FACTS | SCITAB |
| --- | --- | --- | --- | --- |
| Domain | Wiki Tables | Wiki Tables | Scientific Articles | Scientific Articles |
| Annotator | AMT | AMT | AMT | Experts |
| Max. Reasoning Hops | 7 | 2 | 1 | 11 |
| Supported | 54% | 56% | 58% | 37% |
| Veracity Refuted | 46% | 39% | 38% | 34% |
| NEI | — | 5% | 4% | 29% |
| Total # of Claims | 117,854 | 87,026 | 5,715 | 1,225 |
| Avg. claims per table | 7.11 | 0.07 | 5.27 | 6.16 |

Text: "Reasoning Depth. We further measure the reasoning depth (the number of required reasoning steps) for each claim and show the reasoning depth distribution in Figure 3. We find that the analyzed claims have an average depth of 4.76 and a maximum depth of 11. Moreover, 86% of the claims requiring 3 or more reasoning steps, which demonstrates the complexity of reasoning in SCITAB."

Text: "We identify 476 atomic reasoning steps from the 100 analyzed samples and show the proportion for each reasoning type in Table 2."

Text: "We observe that SCITAB has a multifaceted complex range of reasoning types and a high proportion of claims requiring different types of domain knowledge."

Text: "We find that the analyzed claims have an average depth of 4.76 and a maximum depth of 11. Moreover, 86% of the claims requiring 3 or more reasoning steps, which demonstrates the complexity of reasoning in SCITAB."

## Turn 3 — document page 6 (rank 3 of 20)

none

## Turn 4 — document page 2 (rank 4 of 20)

Table 2: Applicability (App.), Productivity (Prod.) and Coverage (Cov.) of the various words in the alternatives of the COPA dev set.
| Cue | App. | Prod. | Cov. |
| --- | --- | --- | --- |
| in | 47% | 55.3% | 9.40% |
| was | 55% | 61.8% | 11.0% |
| to | 82% | 40.2% | 16.4% |
| the | 85% | 38.8% | 17.0% |
| a | 106% | 57.5% | 21.2% |

Figure 1: An example of our SCITAB dataset (left) and its corresponding reasoning graph (right). Each data entry contains paper name, paper id, table, one claim, and its corresponding label (Supported, Refuted, Not Enough Info).

Text: "The dataset was created by crawling computer science papers from arXiv. The tables and the texts explaining the tables are extracted from the papers to create (table, description) pairs for the task of data-to-text generation. From all the table descriptions of SciGen, we first filter the check-worthy scientific claims following the criteria established by Lee et al. (2009) for academic writing. We focus on the descriptions that serve the purpose of “highlighting and commenting on key data”, i.e., describing research findings based on the data presented in scientific tables. Given the task’s objective nature and to save the cost of human labor, we hire a graduate student majoring in computer science to manually select scientific claims based on the aforementioned criteria using the user interface in Appendix A.2. This decision was based on a pilot annotation which showed that a well-trained annotator can achieve over 95% accuracy in filtering scientific claims. To safeguard the quality, we include an option to mark the claim as “Discard-It’s not a claim, or it’s an incomplete, or not grammatically correct sentence.” during the subsequent claim verification process. Using this approach, we filtered out 872 real-world scientific claims from 1,301 table descriptions in the SciGen dataset."

Text: "We adopt a human-model collaboration strategy to construct SCITAB, as shown in Figure 2. We describe the steps involved in data preparation (Section 2.1), automatic claim generation (Section 2.2), and manual claim verification (Section 2.3)."

Text: "We use the publicly available SciGen (Moosavi et al., 2021) dataset as our primary data source."

Text: "We observe that all models, with the exception of GPT-4, can only achieve marginally superior F₁ scores than random guessing, which underscores the challenging nature of SCITAB."

Text: "Additionally, established prompting methods like Chain-of-Thought (Wei et al., 2022) and Program-of-Thought (Chen et al., 2022) which typically enhance performance across most reasoning tasks, do not bring performance gain on SCITAB."

Text: "Our error analysis sheds light on several unique challenges in SCITAB that may lead to this, such as table grounding, dealing with ambiguous claims, and compositional reasoning."

Text: "We make our dataset fully accessible to the research community."

Text: "We adopt a human-model collaboration strategy to construct SCITAB, as shown in Figure 2. We describe the steps involved in data preparation (Section 2.1), automatic claim generation (Section 2.2), and manual claim verification (Section 2.3)."

Text: "We use the publicly available SciGen (Moosavi et al., 2021) dataset as our primary data source."

Text: "We observe that all models, with the exception of GPT-4, can only achieve marginally superior F₁ scores than random guessing, which underscores the challenging nature of SCITAB."

Text: "Additionally, established prompting methods like Chain-of-Thought (Wei et al., 2022) and Program-of-Thought (Chen et al., 2022) which typically enhance performance across most reasoning tasks, do not bring performance gain on SCITAB."

Text: "Our error analysis sheds light on several unique challenges in SCITAB that may lead to this, such as table grounding, dealing with ambiguous claims, and compositional reasoning."

Text: "We make our dataset fully accessible to the research community."

## Turn 5 — document page 1 (rank 5 of 20)

The abstract and introduction sections of the paper state that SCITAB consists of 1,225 expert-verified scientific claims. This number is also explicitly mentioned in Table 1 on page 4, which lists "Total # of Claims" as 1,225 for SCITAB.

## Turn 6 — document page 8 (rank 6 of 20)

Table 5: The error types and their estimated proportions for incorrectly-predicted samples in PoT.
| Error Type | Estimated Proportion (%) |
| --- | --- |
| I. Grounding errors | 50 |
| II. Ambiguity errors | 22 |
| III. Calculation errors | 20 |
| IV. Program errors | 8 |

Text: "We divide the errors into four categories, as assessed by human annotators: (i) Grounding errors, where the program incorrectly associates data with the respective cells in the table; (ii) Ambiguity errors, where the claim contains ambiguous expressions that the program fails to represent; (iii) Calculation errors, where incorrect floating point arithmetic calculation in Python lead to inaccurate results and (iv) Program errors, which encompass mistakes such as incorrect or missing arguments/variables, and erroneous operations."

Text: "Compared to other datasets, categories (i) and (ii) present unique challenges in our dataset. Category (i) underlines the difficulty in accurately referencing the specific cells to which a claim refers. Category (ii), on the other hand, emphasizes the difficulties posed by the ambiguous nature of scientific claims, such as “A is significantly better than B”, to program-based methods."

## Turn 7 — document page 9 (rank 7 of 20)

none
