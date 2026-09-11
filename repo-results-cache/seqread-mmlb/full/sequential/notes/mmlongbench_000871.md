## Turn 1 — document page 8 (rank 1 of 20)

Figure 6. Error distribution over 150 annotated GPT-4V errors.
- Perceptual Error: 35%
- Lack of Knowledge: 29%
- Reasoning Error: 26%
- Textual Understanding Error: 4%
- Reject to Answer: 3%
- Annotation Error: 2%
- Answer Extraction Error: 1%

## Turn 2 — document page 3 (rank 2 of 20)

Figure 3. MMMU contains 11.5K multimodal questions covering six broad disciplines, 30 subjects, and 183 subfields.
- LLMs augmented with optical character recognition (OCR) or generated captions do not see notable improvement, indicating that MMMU necessitates deeper joint interpretation of images and text.
- In disciplines such as Art & Design and Humanities & Social Science, where visual data is less complex, models exhibit higher performance. In contrast, Business, Science, Health & Medicine, and Tech & Engineering, which present more complex visual data and require intricate reasoning, see relatively lower model performance.
- Our error analysis on 150 error cases of GPT-4V reveals that 35% of errors are perceptual, 29% stem from a lack of knowledge, and 26% are due to flaws in the reasoning process. These findings underscore the challenges of the MMMU benchmark and point towards areas needing further research and model enhancement.

## Turn 3 — document page 56 (rank 3 of 20)

- This page presents a specific error case (Figure 42) where GPT-4V incorrectly identifies satellites in an image.
- The error category is explicitly labeled as "Perceptual Error, Reasoning Error".
- The error reason explains that GPT-4V fails to match the cartoon image with real satellites and ignores a path hint, suggesting both perceptual and reasoning errors.
- The ground truth is (A) Terra, Aqua, Landsat 7, while GPT-4V selected (C) Landsat 7, Aqua, Terra.

## Turn 4 — document page 92 (rank 4 of 20)

- This page presents a specific error case (Figure 78) where GPT-4V incorrectly identifies the layer in a leaf diagram.
- The error category is explicitly labeled as "Perceptual Error".
- The error reason states that GPT-4V recognized the protective role of the uppermost layer but failed to correctly identify the visual signals indicating the arrow pointed to guard cells (not the waxy cuticle).
- The ground truth is (C) Guard cells.
- The error is attributed to a flawed reasoning process due to mislinking visual information with the correct biological structure.

## Turn 5 — document page 35 (rank 5 of 20)

- This page presents a specific error case (Figure 21) where GPT-4V incorrectly extracts the retained earnings value from the table image.
- The error category is explicitly labeled as "Perceptual Error".
- The error reason states that GPT-4V wrongly extracts $6,000 instead of the correct $4,200 from the table.
- The ground truth is (A) $17,800.
- This error is a perceptual error, not a reasoning error, as the calculation process was mostly correct but the final data extraction was flawed.

## Turn 6 — document page 42 (rank 6 of 20)

- This page presents a specific error case (Figure 28) where GPT-4V incorrectly identifies the correct option for a management model question.
- The error category is explicitly labeled as "Perceptual Error".
- The error reason states that GPT-4V recalled the right knowledge and made the right reasoning, but it failed to correctly map the IDs to the corresponding illustrations in the figure, which is not explicitly marked in the figure but is only described in text (the order is from left to right, top to bottom).
- The ground truth is (B) 2, while GPT-4V selected (C) 3.
