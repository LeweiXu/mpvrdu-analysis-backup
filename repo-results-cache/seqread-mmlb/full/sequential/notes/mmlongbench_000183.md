## Turn 1 — document page 3 (rank 1 of 20)

Figure 3. MMMU contains 11.5K multimodal questions covering six broad disciplines, 30 subjects, and 183 subfields.
- In disciplines such as Art & Design and Humanities & Social Science, where visual data is less complex, models exhibit higher performance. In contrast, Business, Science, Health & Medicine, and Tech & Engineering, which present more complex visual data and require intricate reasoning, see relatively lower model performance.
- Our error analysis on 150 error cases of GPT-4V reveals that 35% of errors are perceptual, 29% stem from a lack of knowledge, and 26% are due to flaws in the reasoning process.
- The document lists subject performance breakdowns, including:
  - Science (280, 3.3%)
  - Math (540, 5.2%)
  - Computer Sci. (406, 3.5%)
  - Tech & Engineering (26%)
  - Health & Medicine (17%)
  - Humanities & Social Sci. (9%)

## Turn 2 — document page 2 (rank 2 of 20)

The current page contains sample questions from the MMMU dataset across various subjects, including Art & Design, Business, Science, Health & Medicine, Humanities & Social Science, and Tech & Engineering. It includes specific examples with image types and difficulties. For instance:
- Art & Design: Music subject, sheet music, medium difficulty.
- Business: Marketing, plots and charts, medium difficulty.
- Science: Math, calculus, mathematical notations, easy difficulty.
- Health & Medicine: Clinical radiology, MRI scans, hard difficulty.
- Humanities & Social Science: History, comics and cartoons, easy difficulty.
- Tech & Engineering: Electronics, analog electronics, diagrams, hard difficulty.

The page also mentions that MMMU is designed to test expert-level knowledge and reasoning, and that GPT-4V achieves an accuracy of 55.7% on the dataset. However, it does not provide a direct comparison of GPT-4V's performance specifically between CS (Computer Science) and Math subjects.

## Turn 3 — document page 1 (rank 3 of 20)

none

## Turn 4 — document page 7 (rank 4 of 20)

Table 3. Result decomposition across question difficulty levels.
| Models           | Easy (2946) | Medium (4917) | Hard (2637) | Overall (10500) |
|------------------|-------------|---------------|-------------|-----------------|
| Fuyu-8B [6]      | 28.9        | 27.0          | 26.4        | 27.4            |
| Qwen-VL-7B [5]   | 39.4        | 31.9          | 27.6        | 32.9            |
| LLaVA-1.5-13B [34] | 41.3       | 32.7          | 26.7        | 33.6            |
| InstructBLIP-T5-XXL [14] | 40.3     | 32.3          | 29.4        | 33.8            |
| BLIP-2 FLAN-T5-XXL [27] | 41.0      | 32.7          | 28.5        | 34.0            |
| GPT-4V [46]      | 76.1        | 55.6          | 31.2        | 55.7            |

Figure 5. Performance of models on different types of images.
- The bar chart shows performance across image types: Diagrams, Charts, Chemical, Paintings, Geometric, Music, Medical.
- GPT-4V consistently outperforms other models across all image types.
- GPT-4V scores 76.1% on Easy, 55.6% on Medium, and 31.2% on Hard difficulty levels.

Text-only LLMs section:
- GPT-4V achieves 55.7% overall accuracy on MMMU.
- The text mentions performance across disciplines, noting higher performance in Art & Design and Humanities & Social Sciences, and lower performance in Science, Health & Medicine, and Technology & Engineering.
- Table 2 (not fully visible) is referenced for detailed comparisons, but Table 3 is the only one fully visible and relevant to the question.

## Turn 5 — document page 16 (rank 5 of 20)

Table 6 on page 16 shows performance of models on the MMMU validation and test set under the "Science" section, broken down by subject: Biology, Chemistry, Geography, Math, and Physics. For GPT-4V (vision) (Playground), the performance is:
- Math: 45.0%
- Physics: 56.4%

This page does not contain performance data for Computer Science (CS) subject, so a direct comparison between CS and Math subjects cannot be made from this page alone.

## Turn 6 — document page 9 (rank 6 of 20)

none

## Turn 7 — document page 14 (rank 7 of 20)

Table 4 on page 14 shows performance of models on the MMMU validation and test set under the "Art & Design" section. For GPT-4V (vision) (Playground), the performance is:
- Validation Overall: 65.8%
- Test Overall: 65.3%
- Art: 74.0%
- Art Theory: 75.5%
- Design: 80.5%
- Music: 38.6%

This page does not contain performance data for Computer Science (CS) subject, so a direct comparison between CS and Math subjects cannot be made from this page alone.

## Turn 8 — document page 18 (rank 8 of 20)

Table 8 on page 18 shows performance of models on the MMMU validation and test set under the "Humanities & Social Science" section, broken down by subject: History, Literature, Sociology, and Psychology. For GPT-4V (vision) (Playground), the performance is:
- Validation Overall: 78.3%
- Test Overall: 76.3%
- History: 79.1%
- Literature: 89.3%
- Sociology: 71.4%
- Psychology: 73.1%

This page does not contain performance data for Computer Science (CS) subject, so a direct comparison between CS and Math subjects cannot be made from this page alone.

## Turn 9 — document page 6 (rank 9 of 20)

| Subject          | GPT-4V (Vision) (Playground) Performance |
|------------------|------------------------------------------|
| Computer Science | 48.4%                                    |
| Math             | 55.7%                                    |
