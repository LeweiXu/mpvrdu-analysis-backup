## Turn 1 — document page 6 (rank 1 of 20)

Figure 5: Output norm and training loss curves for Chameleon models under various settings.
- (a) Uncontrolled growth of output norms is a strong indicator of future training divergence. The plot shows output norm vs. training step.
- (b) An ablation with Chameleon-7B with and without QK-Norm. The plot shows training loss vs. training step.
- (c) An ablation with Chameleon-7B with and without dropout. The plot shows training loss vs. training step.

## Turn 2 — document page 7 (rank 2 of 20)

Figure 6: Training loss curves for Chameleon models under various settings.
- (a) Training Curves for 600k steps for Chameleon-7B and Chameleon-34B over Mixed-Modal Data.
- (b) Training loss curve with image generation disabled does not suffer from instability issues.
- (c) For Chameleon-34B, using dropout does not fix divergences, both with and without norm-reordering.

## Turn 3 — document page 12 (rank 3 of 20)

Figure 9: Performance of Chameleon vs baselines, on mixed-modal understanding and generation on a set of diverse and natural prompts from human annotators.
- (a) The prompt task fulfillment rates. (Bar chart showing percentage of responses that fulfill, partially fulfill, or do not fulfill tasks for Chameleon, Gemini+, GPT-4V+, Gemini, and GPT-4V.)
- (b) Chameleon vs. the baselines: Gemini+, GPT-4V+, Gemini, GPT-4V. (Bar chart showing win/tie/loss percentages for Chameleon vs. each baseline.)

## Turn 4 — document page 13 (rank 4 of 20)

Figure 10: The inter-annotator agreement on the questions in the absolute evaluation. The figure is a bar chart showing the count of agreements (All, Two, None) across different categories (Containing images, Image quality, Image relevance, Language quality, Objectionable content, Relevance, Task fulfillment, Accuracy).

## Turn 5 — document page 1 (rank 5 of 20)

none

## Turn 6 — document page 2 (rank 6 of 20)

Figure 1: A diagram illustrating Chameleon's architecture for mixed-modal pre-training and generation. It includes two subfigures:
- (a) Mixed-Modal Pre-Training: Shows the flow from a text prompt and image prompt to a mixed-modal auto-regressive language model, which outputs tokens for image generation.
- (b) Mixed-Modal Generation: Shows the flow from a start image and text prompt to a mixed-modal auto-regressive language model, which outputs text and image tokens.
