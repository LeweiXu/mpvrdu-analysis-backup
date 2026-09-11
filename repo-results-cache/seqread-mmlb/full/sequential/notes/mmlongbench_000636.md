## Turn 1 — document page 15 (rank 1 of 20)

- Section B: "Examples of Generated Reasoning Programs" mentions Figure 7 shows six examples.
- Section C: "Error Analysis for Reasoning Programs" mentions Figure 8 shows five examples of erroneous cases.
- Section D: "Program Generation Prompts" states prompts for HOVER and FEVEROUS-S datasets are in Listings 1 and 2.
- Section E: "Prompts for Closed-Book Fact-Checking" details four prompting methods (Direct, ZS-CoT, CoT, Self-Ask) with templates and examples.
- Under "Direct Prompting", "ZS-CoT Prompting", "CoT Prompting", and "Self-Ask Prompting", each section includes a specific example prompt for the claim "Is it true that The woman the story behind Girl Crazy is credited to is older than Ted Kotcheff?" and a placeholder for more in-context examples.
- The page number is 6995.

## Turn 2 — document page 8 (rank 2 of 20)

- This page contains Figure 6, which shows an error case from the HOVER 4-hop dataset with an incorrect program structure. It includes a specific example of a predicted program for the claim about Emery and Edison Local School District.
- Table 2 presents the proportion of different error types (Syntax, Semantic, Token, Structure, Subtask, Incorrect execution) for incorrectly-predicted examples from each hop length (2-hop, 3-hop, 4-hop) in HOVER.
- Table 3 shows macro-F1 scores for PROGRAMFC and baselines (InstructGPT, Codex, FLAN-T5) in the closed-book setting for HOVER and FEVEROUS datasets across different prompting methods (Direct, ZS-CoT, CoT, Self-Ask).
- The page references Appendix C for additional error examples.
- The page number is 6988.

## Turn 3 — document page 22 (rank 3 of 20)

- This page contains Listing 2, which shows prompt examples for the FEVEROUS-S dataset.
- The listing includes seven distinct program examples, each corresponding to a specific claim.
- Each example is structured with a `def program():` block containing `Verify` statements for individual facts and a `Predict` statement combining them.
- The examples cover claims about Alfredo Cornejo Cuevas, Adductor hiatus, Ifor Bowen Lloyd, the 2001 Stanley Cup playoffs, Teldenia helena, William Frick, and an unspecified claim ending with `<input_claim>`.
- The page number is 7002.

## Turn 4 — document page 20 (rank 4 of 20)

- This page contains Listing 1, which shows prompt examples for the HOVER dataset.
- Listing 1 includes two distinct program examples, each corresponding to a specific claim.
- The first example is for the claim: "Thomas Loren Friedman has won more Pulitzer Prizes than Colson Whitehead."
- The second example is for the claim: "The model of car Trevor Bayne drives was introduced for model year 2006. The Rookie of The Year in the 1997 CART season drives it in the NASCAR Sprint Cup."
- The third example is incomplete, starting with "The claim is that <input_claim>", indicating a placeholder for a variable claim.
- The page number is 7000.

## Turn 5 — document page 16 (rank 5 of 20)

- This page contains Figure 7, which shows six distinct examples of generated reasoning programs.
- Each example includes a Claim and a Predicted Program with Verify and Predict statements.
- The examples cover claims about plant genera, Fujairah College, a female board member, solicitors, Anthony Burgess, and films.
- The page number is 6996.

## Turn 6 — document page 14 (rank 6 of 20)

This page (page 6994) discusses implementation details of baselines for few-shot fact-checking, including pre-trained models, fine-tuned models, and in-context learning models. It describes the training procedures, model architectures, and prompt formats for models like BERT-FC, LisT5, RoBERTa-NLI, DeBERTaV3-NLI, MULTIVERS, and Codex. The page does not contain any prompt examples or figures showing generated reasoning programs. It focuses on methodology and implementation, not on displaying examples of prompts.
