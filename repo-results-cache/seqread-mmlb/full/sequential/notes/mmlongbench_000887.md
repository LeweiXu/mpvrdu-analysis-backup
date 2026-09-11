## Turn 1 — document page 28 (rank 1 of 20)

- In Appendix A, we provide additional details on our setup and experiments.
- A FURTHER EXPERIMENTAL DETAILS section begins on this page, detailing the experiment setup.
- Under A.1 NLP TASKS, the section covers:
  - Data preprocessing: describes how datasets are obfuscated, grouped, converted to binary classification, and balanced.
  - Models: describes replacing the un-embedding layer with a linear classification head and initializing weights.
  - Training hyperparameters: specifies finetuning for 2 epochs, batch size of 32, early stopping, and hyperparameter tuning scope.
  - Weak labels: explains splitting the dataset, training a weak supervisor, and using its predictions.
  - Evaluation: describes reporting accuracy on a balanced test set.

## Turn 2 — document page 40 (rank 2 of 20)

## D OTHER WEAK-TO-STRONG SETTINGS
### D.1 SELF-SUPERVISED VISION MODELS
- Describes an experiment using a pretrained AlexNet model as a weak supervisor to generate weak labels on ImageNet.
- Uses linear probing on frozen representations from DINO models (ResNet-50 and ViT-B/8) as strong students.
- Details training setup: 40k datapoints for training, 10k for evaluation, batch size 128, Adam optimizer, learning rate 10⁻³, 20 epochs for ResNet-50, 5 epochs for ViT-B/8.
- Mentions that DINO models were pretrained unsupervised without direct ImageNet supervision.
- Notes this setup avoids the pretraining leakage disanalogy discussed in Section 6.1.
- States results show strong students outperform weak supervisors, achieving PGR around 50%.
- Concludes this experiment generalizes to other domains and tasks with latent knowledge.

## Turn 3 — document page 42 (rank 3 of 20)

## E.1 SYNTHETIC EXPERIMENTS ON SIMULATION DIFFICULTY
- Describes a synthetic experiment on simulation difficulty in a linear probing setting.
- Uses a representation X ∈ R^(n×d) from the SciQ dataset using a model of intermediate size in the GPT-4 family.
- Considers a family of linear models M_k where k ≤ d, trained on the first k features.
- For k1 ≥ k2, model M_k1 can perfectly simulate M_k2 by construction.
- Follows the standard weak-to-strong generalization experiment setup described in Section 3.
- Trains weak supervisor models on 10k datapoints and produces hard weak labels on the remaining 13k datapoints.
- Reports results in Figure 24(a,d).
- In the perfectly simulatable setting, strong student models do not show substantial improvements over the supervisor.
- Test agreement values are substantially higher than weak model accuracy, indicating overfitting to supervisor errors.
- In the completely unsimulatable setting (random noise applied to ground truth), strong students achieve substantially higher accuracy than weak labels.
- Notes that if weak supervisor errors are completely unpredictable (random) for the student, with enough data, good generalization can be recovered, substantially exceeding the supervisor's performance.
- Uses logistic regression with default sklearn parameters for training.

## Turn 4 — document page 44 (rank 4 of 20)

## E.2 DIFFERENT WEAK ERROR STRUCTURE MEANS DIFFERENT GENERALIZATION
- Describes creating synthetic weak label sets with identical error rates but different error structures.
- Targets error structures: pure noise, easy-to-model bias, hard-to-model bias, adversarial bias.
- Lists six specific weak labeler types:
  1. weak supervisor: baseline, labels generated as in the rest of the paper.
  2. random: flip labels of random datapoints.
  3. longest prompt: flip labels of longest datapoints by characters.
  4. shortest prompt: flip labels of shortest datapoints by characters.
  5. strong g.t. model unconfident: flip labels of datapoints the strong ceiling model is most unconfident on.
  6. strong g.t. model confidently correct: flip labels of datapoints the strong ceiling model is most confidently correct on.
- Notes that despite identical weak accuracy, generalization varies wildly with error structure.
- Reports results in Figure 25.
- Discusses dynamics of supervisor-student agreement (Figure 26): initial generalization, followed by overfitting to weak errors, mitigated by confidence auxiliary loss.
- Notes that for easy-to-fit errors (e.g., longest prompt), overfitting is faster; for random noise, generalization improves throughout.

## E.3 MAKING IMITATION TRIVIAL
- Addresses a disanalogy in the setup (discussed in Section 6.1): models are not good at imitating the weak model, but superhuman models may be.
- Proposes a synthetic setting where the strong model can trivially imitate the weak model.
- Method: append “I think this is {weak_label}. What do you think?” to every prompt, where weak_label is “correct” or “incorrect” based on the weak model prediction.
- In this setting, the hardened weak label is present in-context, making simulation trivial.
- Footnote 11: Also known as learning the “human simulator” in the terminology of Christiano et al. (2022).

## Turn 5 — document page 46 (rank 5 of 20)

- Figure 27: Generalization when emulating weak labels is trivial. Shows average PGR across tasks is 0.002 ± 0.003 for baseline, and 0.046 ± 0.108 for aux loss, compared to around 0.2 and 0.8 respectively for the original tasks.
- Section F: HOW SHOULD WE EMPIRICALLY STUDY SUPERALIGNMENT, METHODOLOGICALLY?
  - Discusses criteria for a good setup: tractability, ease of study, and being analogous to the superalignment problem.
  - Mentions that the main evaluation setup (introduced in Section 3) is intended to be more analogous to the superalignment problem.
  - Notes that disanalogies with the setup are enumerated in Section 6.1.
  - Recommends enumerating key assumptions (in Section 6.1 and Appendix G.3) and conducting sensitivity analysis (in Appendix E).
  - Advises avoiding techniques that rely on assumptions likely to break down for future models.

## Turn 6 — document page 41 (rank 6 of 20)

- Section D.2 LINEAR PROBING discusses the experiment setup for weak-to-strong generalization in the linear probing setting.
- Details include: freezing weak and strong model parameters, training new linear classification heads with ground truth or weak labels, using Adam optimizer, learning rate 10⁻³, batch size 128, no weight decay, training for 200 epochs, and early stopping based on validation set agreement to weak labels.
- Mentions that results are shown in Figure 23.
- Notes that linear probing is useful for quickly iterating on methods, datasets, and ideas, and that qualitative trends are similar to full finetuning.
