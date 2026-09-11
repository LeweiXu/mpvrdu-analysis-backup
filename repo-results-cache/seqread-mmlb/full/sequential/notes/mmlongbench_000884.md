## Turn 1 — document page 34 (rank 1 of 20)

Figure 17: The benefits of improved task-specific tuning and ground truth early stopping stack, resulting in even higher PGR. Like Figure 10 but with ground truth early stopping based on test accuracy.
Figure 18: PGR improves when both supervisors and students have an extra generative fine-tuning step. Like Figure 10 but where “with generative finetuning” indicates that both supervisors and students have an extra generative finetuning step. In other words, for this experiment all base models have an extra generative finetuning step following pretraining.
Figure 17: Two line charts. Left chart: test accuracy (%) on y-axis vs. strong student compute (fraction of GPT4) on x-axis. Right chart: performance gap recovered (%) on y-axis vs. strong student compute (fraction of GPT4) on x-axis. Both charts have legends indicating "no generative finetuning", "with generative finetuning", and "strong ceiling performance (g.t. supervision)".
Figure 18: Two line charts. Left chart: test accuracy (%) on y-axis vs. strong student compute (fraction of GPT4) on x-axis. Right chart: performance gap recovered (%) on y-axis vs. strong student compute (fraction of GPT4) on x-axis. Both charts have legends indicating "no generative finetuning", "with generative finetuning", and "strong ceiling performance (g.t. supervision)".

## Turn 2 — document page 31 (rank 2 of 20)

Figure 13: Overfitting during training, for NLP datasets. Strong models overfit to the weak labels. (a) Ground truth test accuracy of strong students over the course of training for a subset of our NLP task. Hues indicate the gap between weak supervisor and strong student model compute. Inset numbers indicate dataset id (compare Figure 12). (b) Median best, early-stopped according to weak label agreement, and final performance gap recovered (PGR) aggregated across all supervisor-student pairs and all NLP tasks. Error bars indicate standard error of the mean (s.e.m.).
Figure 14: Chess puzzles: example datapoints. Two representative examples of an easy (a) and a hard (b) chess puzzle with corresponding prompts and target label formats.

## Turn 3 — document page 30 (rank 3 of 20)

Figure 12: Full weak-to-strong generalization results across 22 NLP datasets. Test accuracy as a function of strong student compute across our full suite of standard NLP tasks. See Table 1 for dataset details.

## Turn 4 — document page 43 (rank 4 of 20)

Figure 25: PGR for weak labels with same accuracy but different error structures. The inset number in each panel indicates the dataset (compare Figure 12). Weak-to-strong generalization and methods both depend critically on the structure of the weak supervisor errors. While it is trivial to pick error structures that generalize well (for instance, random noise), these error structures are also very disanalogous to the ultimate superalignment setting, where we want to study the structures of human errors.

## Turn 5 — document page 37 (rank 5 of 20)

Figure 20: Easy-to-hard generalization on chess puzzles. The figure contains two main sections labeled (a) and (b), each with multiple subplots. Section (a) is titled "Easy cutoff: Elo ≤ 1200" and section (b) is titled "Easy cutoff: Elo ≤ 900". Each section contains multiple charts showing test accuracy (%) on the y-axis versus puzzle elo on the x-axis. The charts compare different training regimes: "train easy", "train hard", "train all", and "zero shot". The model size is indicated in the upper-right corner of each panel as a fraction of GPT-4 compute.

## Turn 6 — document page 33 (rank 6 of 20)

Figure 16: Supervisor-student agreement decreases for stronger students on RMs. Please refer to caption of Figure 8 for detailed explanation of the plot. We reproduce the supervisor-student agreement experiment on the reward modeling data, and observe similar trends to the NLP tasks.
Figure 17: In Figure 17, we show that the PGR improvements from the generative finetuning on RM data (Section 5.2.2) and from early-stopping on ground truth test accuracy (Section 5.1.1) stack together, leading to results competitive with the NLP and chess settings.
Figure 18: In Figure 18, we report the results of an experiment similar to Figure 10, but where the weak models are also pretrained with an additional generative finetuning step on the RM data.

## Turn 7 — document page 15 (rank 7 of 20)

Figure 10: Generative finetuning on reward modeling data improves weak-to-strong performance and PGR. (a) Weak-to-strong performance on the reward modeling task, with (solid lines) and without (dashed lines) an extra step of generative finetuning for the strong student model. Solid black line shows a strong ceiling reward model that was also trained with the generative finetuning step; dashed black line shows a weak supervisor reward model trained without the generative finetuning step. (b) PGR with and without generative finetuning. For generative finetuning PGR, we use the strong ceiling performance that also had this extra generative finetuning step. Even with this ceiling adjustment, PGR is higher with an extra generative finetuning step.
