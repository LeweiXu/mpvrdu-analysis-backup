## Turn 1 — document page 5 (rank 1 of 20)

<table>
<tr>
<th>Method</th>
<th>Feedback</th>
<th>Format</th>
<th>Strategy</th>
<th>Learning</th>
<th>Application</th>
</tr>
<tr>
<td colspan="6">Training-Time Correction</td>
</tr>
<tr>
<td>RLHF (Ouyang et al., 2022)</td>
<td>Reward Model</td>
<td>Scalar</td>
<td>RLHF</td>
<td>RL</td>
<td>Multiple Tasks</td>
</tr>
<tr>
<td>Fine-Grained RLHF (Wu et al., 2023a)</td>
<td>Reward Model</td>
<td>Scalar</td>
<td>RLHF</td>
<td>RL</td>
<td>Detoxification, Long-form QA</td>
</tr>
<tr>
<td>HH-RLHF (Bai et al., 2022a)</td>
<td>Reward Model</td>
<td>Scalar</td>
<td>RLHF</td>
<td>SL &amp; RL</td>
<td>Helpfulness, Harmlessness</td>
</tr>
<tr>
<td>Moral RLHF (Ganguli et al., 2023)</td>
<td>Reward Model</td>
<td>Scalar</td>
<td>RLHF</td>
<td>RL</td>
<td>Moral Correction</td>
</tr>
<tr>
<td>Sparrow (Glaese et al., 2022)</td>
<td>Reward Model</td>
<td>NL</td>
<td>RLHF</td>
<td>SL &amp; RL</td>
<td>Dialogue</td>
</tr>
<tr>
<td>ILF (Scheurer et al., 2023)</td>
<td>Human Feedback</td>
<td>NL</td>
<td>Fine-tuning</td>
<td>SL</td>
<td>Summarization</td>
</tr>
<tr>
<td>ILF-Code (Chen et al., 2023a)</td>
<td>Human Feedback</td>
<td>NL</td>
<td>Fine-tuning</td>
<td>SL</td>
<td>Code Generation</td>
</tr>
<tr>
<td>SLT (Yuan et al., 2023)</td>
<td>Human Feedback</td>
<td>NL</td>
<td>Fine-tuning</td>
<td>SL</td>
<td>Response Generation</td>
</tr>
<tr>
<td>Chain-of-Hindsight (Liu et al., 2023a)</td>
<td>Human Feedback</td>
<td>NL</td>
<td>Fine-tuning</td>
<td>SL</td>
<td>Multiple Tasks</td>
</tr>
<tr>
<td>Crystal (Liu et al., 2023b)</td>
<td>Language Model</td>
<td>Scalar</td>
<td>Fine-Tuning</td>
<td>SL &amp; RL</td>
<td>Commonsense Reasoning</td>
</tr>
<tr>
<td>STaR (Zelikman et al., 2022)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Training</td>
<td>SL</td>
<td>QA, Reasoning</td>
</tr>
<tr>
<td>RLAIF (Bai et al., 2022b)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Training</td>
<td>SL &amp; RL</td>
<td>Dialogue</td>
</tr>
<tr>
<td>SIRLC (Pang et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Training</td>
<td>RL</td>
<td>Reasoning, Translation, Summary</td>
</tr>
<tr>
<td>Self-Improve (Huang et al., 2022)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Training</td>
<td>SL</td>
<td>QA, Reasoning, NLI</td>
</tr>
<tr>
<td>AlpacaFarm (Dubois et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Training</td>
<td>SL &amp; RL</td>
<td>None (Intrinsic Evaluation)</td>
</tr>
<tr>
<td>ReST (Gulcehre et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Training</

## Turn 2 — document page 4 (rank 2 of 20)

- Section 2.4 "When to Correct the Model?" defines three correction strategies: Training-time Correction, Generation-time Correction, and Post-hoc Correction.
- Training-time Correction: Feedback is used to directly optimize model parameters during training. Human feedback is typically used, exemplified by RLHF (Ouyang et al., 2022). Self-training is a common strategy for automated feedback.
- Generation-time Correction: Feedback is used to guide the LLM to correct errors during the generation process. Example: proof generation using feedback from intermediate reasoning steps (Yang et al., 2022a; Lightman et al., 2023).
- Post-hoc Correction: Feedback is used to refine the model output after generation, without updating model parameters. It involves an iterative process of generating, receiving feedback, and refining output. It is more flexible and can incorporate natural language feedback.

## Turn 3 — document page 6 (rank 3 of 20)

<table>
<tr>
<th>Method</th>
<th>Feedback</th>
<th>Format</th>
<th>Strategy</th>
<th>Learning</th>
<th>Iter.</th>
<th>Application</th>
</tr>
<tr>
<td>Self-Refine (Madaan et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>√</td>
<td>Multiple Tasks</td>
</tr>
<tr>
<td>Clinical SV (Gero et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>✕</td>
<td>Information Extraction</td>
</tr>
<tr>
<td>Reflexion (Shinn et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>RL</td>
<td>√</td>
<td>QA, Code Generation</td>
</tr>
<tr>
<td>IterRefinement (Chen et al., 2023d)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>√</td>
<td>Machine Translation</td>
</tr>
<tr>
<td>Auto-Post-Editing (Raunak et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>✕</td>
<td>Machine Translation</td>
</tr>
<tr>
<td>RCI (Kim et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>√</td>
<td>Computer Tasks</td>
</tr>
<tr>
<td>SelfFee (Ye et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>SL</td>
<td>√</td>
<td>Dialogue</td>
</tr>
<tr>
<td>SelfCheckGPT (Manakul et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>✕</td>
<td>Hallucination Detection</td>
</tr>
<tr>
<td>LLM Self Defense (Helbling et al., 2023)</td>
<td>Language Model</td>
<td>NL</td>
<td>Self-Refine</td>
<td>ICL</td>
<td>✕</td>
<td>Harmful Text Correction</td>
</tr>
<tr>
<td>Re3 (Yang et al., 2022b)</td>
<td>Trained Model</td>
<td>Scalar</td>
<td>External Feedback</td>
<td>SL &amp; ICL</td>
<td>√</td>
<td>Story Generation</td>
</tr>
<tr>
<td>CodeRL (Le et al., 2022)</td>
<td>Trained Model</td>
<td>Scalar</td>
<td>External Feedback</td>
<td>RL</td>
<td>✕</td>
<td>Code Generation</td>
</tr>
<tr>
<td>FLIRT (Mehrabi et al., 2023)</td>
<td>Trained Model</td>
<td>Scalar</td>
<td>External Feedback</td>
<td>ICL</td>
<td>√</td>
<td>Adversarial Prompt Generation</td>
</tr>
<tr>
<td>REFINER (Paul et al., 2023)</td>
<td>Trained Model</td>
<td>NL</td>
<td>External Feedback</td>
<td>SL &amp; ICL</td>
<td>√</td>
<td>Reasoning, Moral Story</td>
</tr>
<tr>
<td>RL4F (Akyürek et al., 2023)</td>
<td>Trained Model</td>
<td>NL</td>
<td>External Feedback</td>
<td>SL &amp; RL</td>
<td>√</td>
<td>Planning, Summarization</td>
</tr>
<tr>
<td>Yan et al. (2023)</td>
<td>Trained Model</td>
<td>NL</

## Turn 4 — document page 10 (rank 4 of 20)

- The text discusses REFINER (Paul et al., 2023) and RL4F (Akyürek et al., 2023) as examples of post-hoc correction, where a critic model provides feedback to refine the output without updating model parameters.
- It mentions FLIRT (Mehrabi et al., 2023) as another example of post-hoc correction, using feedback from content filters to guide generation.
- The text notes that in machine translation, post-hoc self-correction is called Automatic Post-Editing (APE) and has a long history.
- It states that in summarization, both training-time correction (imposing factuality constraints during training) and post-hoc correction (post-editing summaries) are mainstream methods.
- The text also mentions that recent work has investigated using RL to refine models guided by automated feedback from either reward models (Akyürek et al., 2023) or language models (Pang et al., 2023), which falls under post-hoc correction.

## Turn 5 — document page 2 (rank 5 of 20)

Figure 1 presents a conceptual framework for correcting LLMs with automated feedback, identifying three key parties: Language Model (Patient), Critic Model (Doctor & Diagnosis), and Refine Model (Treatment). The framework categorizes correction strategies into three main types: Training-time, Generation-time, and Post-hoc correction. The text explicitly states that the paper will discuss these three major techniques, categorized as training-time, generation-time, and post-hoc correction. The figure also shows "Post-hoc Revision" as one of the strategies under the "Refine Model" box.

## Turn 6 — document page 1 (rank 6 of 20)

This page is the title page and introduction of the survey paper. It establishes the context: the paper reviews recent advances in correcting LLMs with automated feedback, categorizing them into three main types: training-time, generation-time, and post-hoc correction. The abstract and introduction confirm that the survey will cover these three strategies. However, this page does not provide any specific data or evidence to compare the number of representative papers for each strategy. The comparison of which strategy has the most representative papers requires evidence from the body of the paper, which is not present on this page.

## Turn 7 — document page 11 (rank 7 of 20)

- The page discusses "Post-hoc correction" in the context of open-ended text generation, citing examples like correcting toxic outputs, enhancing narrative quality in story generation, and refining response generation in dialogues (Wang et al., 2017; Holtzman et al., 2018; Sagarkar et al., 2018).
- It mentions that post-hoc correction is often adopted for these tasks, implying a significant body of work exists for this strategy.
- The page also notes that intrinsic self-correction (a form of self-training) has generally shown disappointing results, which contrasts with the more promising outcomes for external feedback methods, including post-hoc correction.
- The page does not provide a direct count or comparison of the number of representative papers for each strategy, but the discussion of post-hoc correction in multiple contexts (semantic parsing, proof generation, open-ended generation) suggests it is well-represented in the survey.

## Turn 8 — document page 8 (rank 8 of 20)

## Section 3.3: Post-hoc Correction

This section introduces post-hoc correction as a strategy where both the critic and refinement models operate *after* the complete output is generated. It contrasts this with generation-time correction, noting that providing precise feedback for intermediate outputs is challenging in holistic NLP tasks like summarization, which motivates the use of post-hoc methods.

The section categorizes key post-hoc correction strategies into three types:
1.  Self-Correction
2.  Correction with External Feedback
3.  Multi-Agent Debate

The text states that post-hoc correction allows for more diverse natural language feedback, ranging from specific diagnostic reports to broader writing suggestions. It also references Figure 4 for a visual categorization of these strategies.

## Turn 9 — document page 9 (rank 9 of 20)

Figure 4 illustrates three post-hoc correction strategies: self-correction (a), external feedback (b), and multi-agent debate (c). The text details "Self-Correction," where a single LLM generates and then refines its output iteratively, citing Self-Refine (Madaan et al., 2023), Clinical Self-Verification (Gero et al., 2023), and Reflexion (Shinn et al., 2023) as examples. It also discusses "Models/Tools as Feedback," which includes code interpreters (e.g., Self-Edit, Self-Debug, ALGO), logic reasoners (e.g., Logic-LM, Baldur), external knowledge (e.g., RARR, REFEED, LLM-Augmenter, FACTOOL), and trained models (e.g., CodeRL). The page provides numerous specific examples and references for each sub-strategy under post-hoc correction.
