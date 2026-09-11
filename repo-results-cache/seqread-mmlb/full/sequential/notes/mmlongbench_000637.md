## Turn 1 — document page 5 (rank 1 of 20)

Figure 2: The Codex prompt template used to generate reasoning programs, consisting of a task instruction, in-context examples, and a prompt for the <input_claim>. The full templates are given in Appendix D.
![](images/0.jpg)

Figure 3: Implementation of the question-answering sub-task function for three different settings.

The text on page 6985 includes the following code snippet:
# The claim is that Both James Cameron and the director of the film Interstellar were born in Canada.
def program():
    fact_1 = Verify("James Cameron was born in Canada.")
    Answer_1 = Question("Who is the director of the film Interstellar?")
    fact_2 = Verify("Answer_1) was born in Canada.")
    label = Predict(fact_1 and fact_2)

The text also includes the following code snippet:
# The claim is that <input_claim>
def program():

## Turn 2 — document page 6 (rank 2 of 20)

This page contains Table 1 and its description, which discusses the performance of various models including PROGRAMFC and baselines on few-shot fact-checking tasks. The text mentions that for PROGRAMFC, examples are used as in-context examples for reasoning program generation. It also discusses the effectiveness of decomposition and aggregation of reasoning programs. However, this page does not contain any figure or visual content at the top of page 6985, nor does it show any in-context examples. The page is focused on presenting experimental results and analysis.

## Turn 3 — document page 8 (rank 3 of 20)

This page contains Figure 6, which is described as an error case from the HOVER 4-hop dataset. The figure shows a generated reasoning program with incorrect program structure, with incorrect segments marked in red and correct revisions marked in green. The figure is accompanied by Table 2 and Table 3, which discuss error types and model performance, respectively. The text references Figure 6 as an example of a structural error, but does not show any in-context examples in the figure itself. The figure is located at the top of page 6988, not page 6985.

## Turn 4 — document page 15 (rank 4 of 20)

Figure 7 shows six examples of generated reasoning programs by PROGRAMFC that cover diverse reasoning chains.
Figure 8 shows five examples of erroneous cases where the generated reasoning programs are incorrect.

## Turn 5 — document page 17 (rank 5 of 20)

Figure 8 is shown at the bottom of the page, and its caption states: "Example error cases where the generated reasoning programs are incorrect. The incorrect segment(s) are marked in red, and the correct revisions are marked in green." The figure contains five examples (labeled Example 1 through Example 5), each showing a predicted program and its corrected version. The figure is located on page 6997, not page 6985.

## Turn 6 — document page 4 (rank 6 of 20)

This page discusses the structure of reasoning programs and the use of in-context examples for program generation. It mentions that Codex can learn effectively from a small number of in-context examples, denoted as D = {d₁, ..., d|D|}, where each example dᵢ consists of a claim and a program. The text states that K=20 in-context examples are used to maintain a balance between diversity and model capacity. However, this page does not contain any figure at the top of page 6985, nor does it show any in-context examples visually. The page is focused on describing the program generation process and sub-task functions.
