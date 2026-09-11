## Turn 1 — document page 5 (rank 1 of 20)

Figure 3: The distribution histogram of reasoning steps in our SCITAB dataset. The x-axis is the reasoning steps in each claim, and the y-axis is the frequency for each reasoning step. The shallow claims (with 1–2 reasoning steps) are highlighted in red, while the deep claims (with 3+ reasoning steps) are highlighted in blue.

The bar chart shows the frequency of claims based on the number of reasoning steps required. The x-axis is labeled "Reasoning Steps" and ranges from 1 to 11. The y-axis is labeled "Percentages (%)" and ranges from 0 to 25. The bars are as follows:
- Reasoning Step 1: 6%
- Reasoning Step 2: 8%
- Reasoning Step 3: 15%
- Reasoning Step 4: 18%
- Reasoning Step 5: 20%
- Reasoning Step 6: 15%
- Reasoning Step 7: 7%
- Reasoning Step 8: 3%
- Reasoning Step 9: 2%
- Reasoning Step 10: 1%
- Reasoning Step 11: 1%

The text below the figure states: "Figure 3: The distribution histogram of reasoning steps in our SCITAB dataset. The x-axis is the reasoning steps in each claim, and the y-axis is the frequency for each reasoning step. The shallow claims (with 1–2 reasoning steps) are highlighted in red, while the deep claims (with 3+ reasoning steps) are highlighted in blue."

## Turn 2 — document page 4 (rank 2 of 20)

The table on this page (Table 1) explicitly states that for the SCITAB dataset, the maximum reasoning hops is 11. The text in the "Reasoning Depth" subsection further confirms this, stating "We find that the analyzed claims have an average depth of 4.76 and a maximum depth of 11." It also mentions that "SCITAB is 1) annotated by domain experts rather than crowd-sourced workers, 2) contains more challenging claims that require up to 11 reasoning steps for verification."

## Turn 3 — document page 2 (rank 3 of 20)

Figure 1 is shown on this page, along with its corresponding reasoning graph. The caption states: "An example of our SCITAB dataset (left) and its corresponding reasoning graph (right). Each data entry contains paper name, paper id, table, one claim, and its corresponding label (Supported, Refuted, Not Enough Info)." The reasoning graph visually depicts the steps involved in verifying the claim "A's productivity of 57.5% expresses that it appears in 7.5% more often than expected by random chance." The graph shows a sequence of reasoning steps: "Simple lookup" → "Subtraction" → "Fact checker: Supported". This visual representation confirms that the reasoning process for this specific claim involves multiple steps, consistent with the maximum of 11 steps mentioned in Table 1 and Figure 3.

## Turn 4 — document page 1 (rank 4 of 20)

This page contains the introduction section of the paper, which discusses the limitations of existing scientific fact-checking benchmarks and introduces SCITAB as a new dataset. It mentions that SCITAB contains 1,225 challenging scientific claims that require compositional reasoning for verification using scientific tables. The text states: "Figure 1 shows a claim from SCITAB and the corresponding reasoning process to verify it." This confirms that Figure 1 is related to a claim from SCITAB and includes its reasoning process, but it does not specify the number of reasoning steps involved in that specific figure.

## Turn 5 — document page 3 (rank 5 of 20)

This page contains Figure 2, which illustrates the human-model collaboration construction process of SCITAB. It details three steps: 1) Data Preparation, 2) Automatic Claim Generation, and 3) Manual Claim Verification. The figure describes the workflow for generating false claims and NEI claims using InstructGPT and human verification. However, this page does not contain any information about the number of reasoning steps involved in Figure 1 or any specific claim from the SCITAB dataset.

## Turn 6 — document page 8 (rank 6 of 20)

This page discusses error analysis for models on the SCITAB dataset, including confusion matrices (Figure 4) and error types (Table 5). It references Figures 11, 12, 13, and 14 in the appendix for examples of error instances. The text mentions that claims erroneously predicted as 'NEI' typically demand "extensive reasoning and a deep understanding of the research findings." It also notes that "such claims typically demand extensive reasoning" and that "when faced with these complex cases, the model tends to default to the safer choice of ‘uncertain’ (NEI)." However, this page does not contain any information about the specific number of reasoning steps involved in Figure 1 or any claim from the SCITAB dataset.
