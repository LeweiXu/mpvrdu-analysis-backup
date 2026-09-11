## Turn 1 — document page 21 (rank 1 of 20)

| Subject | Correct Case | Perception | Lack of Knowledge | Reasoning | Other |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Mechanical Engineering | 93 |  |  | 94, 95 |  |

## Turn 2 — document page 20 (rank 2 of 20)

none

## Turn 3 — document page 117 (rank 3 of 20)

none

## Turn 4 — document page 99 (rank 4 of 20)

Error Category: Perceptual Error
Error Reason: GPT-4V recalls the correct knowledge “Interleaved processing occurs when two transactions are processed alternately, meaning that one starts, then the other starts before the first one finishes, and then the first one might resume, and so on.” However, it fails to interpret the image w.r.t. transaction A and B: “Transaction A on CPU1 starts and finishes without being interleaved with any other transaction. Transaction B on CPU1 starts after A finishes and completes without being interleaved with any other transaction. Transaction A on CPU2 starts and finishes without any interleaving. Transaction B on CPU2 starts after A finishes and completes without any interleaving.” The figure intends to illustrate transaction A and B being processed concurrently on one CPU in an interleaved fashion. These two processes have nothing to do with the CPU1 and CPU2 shown on the right side of the figure. On the perception level, the model made a wrong connection by saying the first appearance of transaction A is on CPU1 and the second appearance is on CPU2 (and the same for transaction B). With that said, the figure is indeed a non-trivial one to interpret and a model might need to know some subject-specific convention to interpret it correctly.
Ground Truth: (A) A and B

## Turn 5 — document page 109 (rank 5 of 20)

## Mechanical Engineering: Engineering Dynamics Error Case (Page 109)

- **Question**: With what minimum horizontal velocity u can a boy throw a rock at A and have it just clear the obstruction at B?
- **Options**: (A) 18.014 m/s, (B) 24.014 m/s, (C) 28.014 m/s
- **Error Category**: Reasoning Error
- **Error Reason**: GPT-4V made a sequential calculation error. It incorrectly calculated the time to fall 26m from A (Step 3) and used it to find the horizontal velocity. The correct approach is to calculate the time to fall 10m after clearing B (≈1.428s) and use the horizontal distance to B (40m) to find the minimum velocity: 40m / 1.428s ≈ 28.014 m/s.
- **Ground Truth**: (C) Minimal $ v_m = 28.014 \, \text{m/s} $

## Turn 6 — document page 8 (rank 6 of 20)

## Error Types Mentioned in the Case Studies (Pages 95-100)

Based on the current page (Page 8), the document categorizes errors into the following types:

- **Perceptual Error (35%)**: This is the largest category and is further divided into:
  - Basic perceptual errors: Occur when the model accurately processes information but fails in elementary visual interpretation (e.g., misjudging sequence like "from left to right, top to bottom").
  - Domain-specific perceptual errors: Occur due to lack of specialized knowledge (classified under "Lack of Knowledge").

- **Lack of Knowledge (29%)**: A fundamental root cause of domain-specific perceptual errors, exemplified by the model's inability to interpret domain-specific visual elements (e.g., double circles as an "accept state" in Deterministic Finite Automata).

- **Reasoning Errors (26%)**: Flawed reasoning occurs when the model correctly interprets text and images and recalls relevant knowledge but fails to apply logical or mathematical reasoning effectively.

- **Other Errors (9%)**: This includes:
  - Textual Understanding Error (6%)
  - Rejection to Answer (3%)
  - Annotation Error (2%)
  - Answer Extraction Error (1%)

The current page does not contain case studies from Pages 95-100, but it provides the error classification framework used for analyzing the 150 sampled errors, which includes the case studies referenced in the question.

## Turn 7 — document page 100 (rank 7 of 20)

## Computer Science: Compiler Principle Case Study (Page 100)

- **Question**: Is the one shown in the figure a minimal DFA?
- **Options**: (A) Yes, (B) No
- **Error Category**: Perceptual Error
- **Error Reason**: The model misreads the transition function. It incorrectly states that δ(0, b) = 4, when the image shows δ(0, b) = 2. It also incorrectly states that δ(1, b) = 0, when the image shows δ(1, b) = 1. The model fails to ground its reasoning on the image.
- **Ground Truth**: (B) No

## Turn 8 — document page 98 (rank 8 of 20)

## Computer Science: Compiler Principle Case Study (Page 98)

- **Question**: Is the DFA shown in the image minimal?
- **Error Category**: Perceptual Error, Lack of Knowledge
- **Error Reason**: GPT-4V chose the wrong answer "not sure" because it did not know "which states are accepting". The model failed to recognize the double circles denoting accepting states. This error stems from two possible causes: (1) a perceptual error in missing the visual signal of double circles, or (2) recognizing the double circles but failing to connect them with the concept of "accept state" due to lack of specific subject knowledge.
- **Ground Truth**: (A) Yes

## Turn 9 — document page 85 (rank 9 of 20)

## Literature: Comparative Literature (Page 85)

- **Question**: Refer to the image, which term best matches the given set of characteristics?
- **Options**: (A) Common elements in horror stories, (B) Literary elements in horror, (C) Scary plot twists, (D) Intensity
- **Error Category**: Perceptual Error
- **Error Reason**: GPT-4V did not capture the expressions of the characters in the painting or the chopping action of the person on the far left, focusing instead only on the muscles and movements of the character on the far right. As a result, GPT-4V failed to recognize the elements were terrifying.
- **Ground Truth**: (A) Common elements in horror stories
