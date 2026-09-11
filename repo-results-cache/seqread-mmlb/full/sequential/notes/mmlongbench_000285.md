## Turn 1 — document page 5 (rank 1 of 10)

Figure 4: The screenshot of the QACHECK user interface showing its key annotated functions. First, users have the option to select a claim or manually input a claim that requires verification. Second, users can start the verification process by clicking the Submit button. Third, the system shows a step-by-step question-answering guided reasoning process. Each step includes the reasoning depth, the generated question, relevant retrieved evidence, and the corresponding predicted answer. Finally, it presents the final prediction label with the supporting rationale.

The figure is annotated with four steps:
1. Select or input a custom claim.
2. Submit to fact-check the input claim.
3. Visualize the question-answering guided reasoning process.
4. The final prediction result with rationale.

## Turn 2 — document page 6 (rank 2 of 10)

The current page describes the QACHECK user interface and its functionality. It references Figure 4 (located at the top of page 5) and explains that after users select or input a claim and click “Submit,” the system visualizes a step-by-step reasoning process. The description confirms that the final step is to show the “final veracity prediction for the original claim accompanied by a comprehensive rationale” in the “Prediction with rationale” section. This aligns with the annotation from page 5 which listed the final step as “The final prediction result with rationale.”

## Turn 3 — document page 2 (rank 3 of 10)

This page describes the QACHECK system architecture and its components, including the claim verifier, question generator, QA module, validator, and reasoner. It references Figure 4 (user interface) and Figure 2 (system architecture) but does not contain the figure itself or a direct description of the steps in the user interface. The page confirms that the system visualizes a step-by-step reasoning process and that the final step involves the reasoner outputting the final veracity label based on all collected contexts. However, it does not explicitly state the final step as described in the figure annotation from page 5.

## Turn 4 — document page 3 (rank 4 of 10)

The current page describes the internal workflow of the QACHECK system, detailing the sequence of modules: Claim Verifier → Question Generator → Question-Answering Model → Validator → Reasoner. It explicitly states that the process continues until the claim verifier returns "True," indicating sufficient context. At that point, the reasoner module is called to output the final label: "{Supported, Refuted}". This aligns with the annotation from page 5, which listed the final step as "The final prediction result with rationale." The page also confirms that the reasoner justifies the veracity of the claim using the stored context.

## Turn 5 — document page 4 (rank 5 of 10)

This page contains Figure 3, which illustrates the three different implementations of the Question Answering (QA) module in QACHECK: (a) Retriever-Reader, (b) FLAN-T5, and (c) GPT Reciter-Reader. It describes the components and workflow for each implementation, including the use of a retriever, a reader, and the specific models involved (e.g., BM25, RoBERTa-large, FLAN-T5, InstructGPT). The page also discusses the QA Validator module, which ensures the usefulness of generated QA pairs by checking if they add new information and are useful for verifying the original claim. However, this page does not contain the figure located at the top of page 5 (Figure 4) or any description of the final step in the user interface workflow.

## Turn 6 — document page 1 (rank 6 of 10)

Figure 1: An example of question-guided reasoning for fact-checking complex real-world claims. It shows a two-step process: Q1: "What is the greatest depth of the Black Sea?" with answer A1: "Black sea has a maximum depth of 2,212 meters." followed by Q2: "How far can sunlight penetrate water?" with answer A2: "Sunlight does not penetrate water below 1,000 meters." The final conclusion is: "2,212 is greater than 1,000. Therefore, the claim is FALSE."
