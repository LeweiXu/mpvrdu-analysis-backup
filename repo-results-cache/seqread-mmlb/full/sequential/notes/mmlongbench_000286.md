## Turn 1 — document page 2 (rank 1 of 10)

Figure 2: The architecture of our QACHECK system.
The figure shows a diagram with several boxes and arrows. The boxes are labeled: "Claim", "Claim Verifier", "Question Generator", "QA Model", "Validator", "Reasoner", and "Label". The "QA Model" box is connected to the "Validator" box and the "Reasoner" box. The "QA Model" box is also connected to a box labeled "(Q, A)". The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim" box is connected to the "Claim Verifier" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "QA Model" box is also connected to a box labeled "(Q, A)". The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim" box is connected to the "Claim Verifier" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "QA Model" box is also connected to a box labeled "(Q, A)". The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim" box is connected to the "Claim Verifier" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "QA Model" box is also connected to a box labeled "(Q, A)". The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim" box is connected to the "Claim Verifier" box. The "Claim Verifier" box is connected to the "Question Generator" box. The "Question Generator" box is connected to the "QA Model" box. The "QA Model" box is connected to the "Validator" box. The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "QA Model" box is also connected to a box labeled "(Q, A)". The "Validator" box is connected to the "Reasoner" box. The "Reasoner" box is connected to the "Label" box. The "Claim Verifier" box is connected to the "Question Generator" box

## Turn 2 — document page 5 (rank 2 of 10)

Figure 4: The screenshot of the QACHECK user interface showing its key annotated functions. First, users have the option to select a claim or manually input a claim that requires verification. Second, users can start the verification process by clicking the Submit button. Third, the system shows a step-by-step question-answering guided reasoning process. Each step includes the reasoning depth, the generated question, relevant retrieved evidence, and the corresponding predicted answer. Finally, it presents the final prediction label with the supporting rationale.

The figure shows a user interface with four main annotated steps:
1. "Select or input a custom claim" — highlighted with a red rectangle.
2. "Submit to fact-check the input claim" — highlighted with a red rectangle.
3. "Visualize the question-answering guided reasoning process" — highlighted with a red rectangle.
4. "The final prediction result with rationale" — highlighted with a red rectangle.

The text in section 3.5 Reasoner states: "We provide two different implementations for the reasoner: 1) the end-to-end QA model based on FLAN-T5, and 2) the InstructGPT model with the prompts given in Appendix A.4."

## Turn 3 — document page 3 (rank 3 of 10)

none

## Turn 4 — document page 4 (rank 4 of 10)

Figure 3: Illustrations of the three different implementations of the Question Answering module in QACHECK.

(a) Retriever–Reader
- Input: Question
- Process: 
  - Retriever retrieves evidence from Wikipedia.
  - Reader predicts an answer conditioned on the retrieved documents.
- Output: Answer

(b) FLAN-T5
- Input: Question
- Process: 
  - FLAN-T5 generates the answer and evidence directly from its parametric knowledge.
- Output: Answer

(c) GPT Reciter–Reader
- Input: Question
- Process: 
  - InstructGPT is prompted to "recite" knowledge stored within it.
  - InstructGPT responds with relevant evidence.
  - Evidence is fed into a reader model to produce the corresponding answer.
- Output: Answer

The figure shows three diagrams labeled (a), (b), and (c), each depicting a different QA implementation. The diagrams are drawn with colored rectangles and arrows. The rectangle in diagram (a) is light blue. The rectangle in diagram (b) is light green. The rectangle in diagram (c) is light purple.

## Turn 5 — document page 6 (rank 5 of 10)

none

## Turn 6 — document page 1 (rank 6 of 10)

none

## Turn 7 — document page 10 (rank 7 of 10)

This page contains prompts for different components of the QACHECK system (Claim Verifier, Question Generation, Validator, and Reasoner) and includes example interactions. The page is divided into sections with colored boxes highlighting different parts of the prompts. The "Reasoner" section (A.4) is highlighted with a light purple rectangle. The "Claim Verifier" section (A.1) is highlighted with a light blue rectangle. The "Question Generation" section (A.2) is highlighted with a light green rectangle. The "Validator" section (A.3) is highlighted with a light purple rectangle.

## Turn 8 — document page 7 (rank 8 of 10)

none

## Turn 9 — document page 9 (rank 9 of 10)

none
