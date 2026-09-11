## Turn 1 — document page 2 (rank 1 of 20)

Figure 1: An illustration of our methodology. Traditional ML focuses on the setting where humans supervise models that are weaker than humans. For the ultimate superalignment problem, humans will have to supervise models much smarter than them. We study an analogous problem today: using weak models to supervise strong models.

The figure contains three subfigures:
- Left: Traditional ML — a human supervisor supervising a smaller robot (student).
- Middle: Superalignment — a human supervisor supervising a much larger robot (student).
- Right: Our Analogy — a small robot (supervisor) supervising a larger robot (student).

The caption states: "An illustration of our methodology. Traditional ML focuses on the setting where humans supervise models that are weaker than humans. For the ultimate superalignment problem, humans will have to supervise models much smarter than them. We study an analogous problem today: using weak models to supervise strong models."

## Turn 2 — document page 12 (rank 2 of 20)

Figure 7: Strong models overfit to the weak labels. In all figures, we show data for the ChatGPT Reward Modeling task. (a) Weak-to-strong performance over the course of training. Hues indicate the student-supervisor gap. (b) Best weak-to-strong performance during training (stars) and weak-to-strong performance at the end of training (dashed). Weak performance in black. Hue indicates the size of the weak supervisor. (c) Median best and final performance gap recovered (PGR) aggregated across all supervisor-student pairs. We see overfitting to weak labels for large weak-strong gaps, even within one epoch. In these cases, the best test accuracy achieved over training can be substantially better than the test accuracy at the end of training. See Figure 13 for the corresponding analysis of a representative subset of NLP tasks.

Figure 7a: A line chart showing weak-to-strong performance over the course of training (x-axis: progress (fraction of epoch), y-axis: test accuracy (%)). Multiple colored lines represent different student-supervisor gaps (hues). The lines show performance trends for different gap sizes.

Figure 7b: A line chart showing best weak-to-strong performance during training (stars) and weak-to-strong performance at the end of training (dashed). The x-axis is the size of the weak supervisor (log scale), and the y-axis is weak-to-strong performance (%). The chart shows that performance at the end of training (dashed) is generally lower than the best performance during training (stars), especially for larger weak supervisors.

Figure 7c: A bar chart showing the median best and final performance gap recovered (PGR) aggregated across all supervisor-student pairs. The x-axis is the weak-strong gap (log scale), and the y-axis is PGR (%). The chart shows that PGR is higher for larger weak-strong gaps, indicating overfitting to weak labels.

## Turn 3 — document page 45 (rank 3 of 20)

Figure 26: Training dynamics change for different weak errors. We show teacher-student agreement for different weak error structures on three datasets. We see that the training dynamics have qualitatively different behavior for different error structures, despite all weak labelers having the same accuracy.

The figure contains three subfigures labeled [a], [b], and [c], each with multiple plots. Each plot shows "student-supervisor agreement (%)" on the y-axis and "progress (fraction of epoch)" on the x-axis. The plots compare different error structures (e.g., "weak supervisor correct", "aux. loss", "weak supervisor wrong") and different prompt lengths ("longest prompt", "shortest prompt"). The lines show how agreement evolves during training for each condition.

## Turn 4 — document page 32 (rank 4 of 20)

Figure 15: Additional results on chess. Test accuracy of (a) baseline and (b) bootstrapping (see section 4.3.1) compared to a zero-shot baseline. Zero-shot performance improves with model size, and students supervised with much weaker supervisors sometimes underperform compared to the corresponding zero-shot model. (c) Supervisor-student agreement on the chess puzzle data. Similar to Figure 8, agreement decreases as the student becomes larger. Hue of line indicates compute of weak supervisor.

Zero-shot results. In Figure 15(a, b), we compare the naive baseline and bootstrapping (see section 4.3.1) generalization to a zero-shot baseline on the chess puzzle data. Especially since the models were pretrained on chess games, zero-shot evaluation provides a strong baseline. In particular, strong students trained with much weaker supervisors underperform the zero-shot baseline for the same model size in some cases.

Supervisor-student agreement results. In Figure 15(c), we report the supervisor-student agreement on the chess puzzles. Similar to the NLP tasks (see Section 5.1.3), the agreement on chess also decreases as the student models get larger.

Figure 15(a): A line chart showing test accuracy (%) on the y-axis versus strong student compute (fraction of GPT4) on the x-axis (log scale). It compares the naive baseline (solid lines) and bootstrapping (dashed lines) against a zero-shot baseline (dotted line). The chart shows that zero-shot performance improves with model size, and that students supervised with much weaker supervisors (indicated by different line styles) sometimes underperform compared to the corresponding zero-shot model for the same model size.

Figure 15(b): A line chart showing test accuracy (%) on the y-axis versus strong student compute (fraction of GPT4) on the x-axis (log scale). It compares the naive baseline (solid lines) and bootstrapping (dashed lines) against a zero-shot baseline (dotted line). The chart shows that zero-shot performance improves with model size, and that students supervised with much weaker supervisors (indicated by different line styles) sometimes underperform compared to the corresponding zero-shot model for the same model size.

Figure 15(c): A line chart showing supervisor-student agreement (%) on the y-axis versus strong student compute (fraction of GPT4) on the x-axis (log scale). The hue of the line indicates the compute of the weak supervisor. The chart shows that agreement decreases as the student models get larger.

## Turn 5 — document page 33 (rank 5 of 20)

Figure 16: Supervisor-student agreement decreases for stronger students on RMs. The figure contains three subfigures labeled (a), (b), and (c), each showing a line chart with "supervisor-student agreement (%)" on the y-axis and "strong student compute (fraction of GPT4)" on the x-axis (log scale). The hue of the lines indicates the compute of the weak supervisor.

Subfigure (a): Shows agreement for "supervisor correct" (weak supervisor correct). The agreement is high for small student compute and decreases as student compute increases.

Subfigure (b): Shows agreement for "weak-to-strong performance" (weak supervisor correct). The agreement is high for small student compute and decreases as student compute increases.

Subfigure (c): Shows agreement for "supervisor mistakes" (weak supervisor wrong). The agreement is high for small student compute and decreases as student compute increases.

## Turn 6 — document page 31 (rank 6 of 20)

This page contains Figure 13 and Figure 14. Figure 13 shows overfitting during training for NLP datasets, with subfigures (a) and (b). Figure 14 shows example chess puzzles. Neither figure contains subfigures labeled "first" and "second" as referenced in the question. The question specifically refers to "Figure 1", but Figure 1 is not present on this page. The content on this page does not provide any information to compare the first and second subfigures of Figure 1 regarding the supervisor-student relationship.

## Turn 7 — document page 13 (rank 7 of 20)

Figure 8: Student-supervisor agreement decreases with larger student-supervisor gaps; the confidence loss reduces imitation of supervisor mistakes. (a) Student-supervisor agreement as a function of strong student size on NLP tasks, (b) a but only on samples where the supervisor is correct, (c) a but only on samples where the supervisor is mistaken. Dotted lines indicate naive finetuning on weak labels, and triangles indicate results with the auxiliary confidence loss results (see Section 4.3). Hue of line indicates size of weak supervisor. For results on reward models, see Figure 16.

The text below the figure states: "Next, we study student-supervisor agreement as a function strong model size (see Figure 8 and Figure 16). Surprisingly, we find inverse scaling (McKenzie et al., 2023): larger student models consistently agree less with the errors of the supervisor than smaller student models, despite being trained to imitate the supervisor, not using early stopping, and having larger capacity than smaller student models."

The text further clarifies: "This trend is especially strong if we evaluate agreement only on datapoints where the supervisor is wrong (Figure 8c), and the trend persists if looking at cross entropy loss instead of accuracy."

## Turn 8 — document page 9 (rank 8 of 20)

None

## Turn 9 — document page 10 (rank 9 of 20)

Figure 5: Substantially improved generalization on NLP datasets with a simple auxiliary loss. (a) Test accuracy as a function of strong student size. Accuracy of a student trained with ground truth in black, accuracy of students naively trained with weak supervision shown with dotted lines. Accuracies of students trained with auxiliary confidence loss shown with colored triangles. Median computed across 22 NLP tasks (hue indicates size of weak supervisor), see Figure 6 for individual datasets. (b) Same as a with PGR. The confidence loss can improve generalization drastically, especially for large supervisor-student gaps.

The text below the figure states: "In Figure 5, we plot accuracy and PGR curves with this method on our NLP tasks. We find that while it performs slightly worse than the naive baseline for smaller strong students, it dramatically improves generalization for large gaps in compute between weak and strong models. With the smallest weak supervisor and largest strong student, the confidence loss increases median PGR from about 25% to nearly 80%."

## Turn 10 — document page 34 (rank 10 of 20)

None
