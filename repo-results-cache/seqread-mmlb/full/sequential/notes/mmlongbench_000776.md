## Turn 1 — document page 7 (rank 1 of 20)

In Figure 5b, we show training loss curves for Chameleon-7B with and without QK-Norm, and the latter diverges after approximately 20% of a training epoch. We found that to stabilize Chameleon-7B by controlling norm growth, it was necessary to introduce dropout after the attention and feed-forward layers, in addition to QK-norm (see Figure 5c). However, this recipe was not enough to stabilize, Chameleon-34B, which required an additional re-ordering of the norms. Specifically, we use the strategy of normalization proposed in Liu et al. (2021), within the transformer block. The benefit of the Swin transformer normalization strategy is that it bounds the norm growth of the feedforward block, which can become additionally problematic given the multiplicate nature of the SwiGLU activation function. If h represents the hidden vector at time-step t after self-attention is applied to input x, Chameleon-34B: h = x + attention_norm(attention(x)) output = h + ffn_norm(feed_forward(h)) Llama2: h = x + attention(attention_norm(x)) output = h + feed_forward(ffn_norm(h)) There was no difference in perplexity when training a model from scratch with and without the normalization re-ordering until the divergence of the LLaMa-2 parameterization. Additionally, we found that this type of normalization did not work well in combination with dropout and therefore, we train Chameleon-34B without dropout (Figure 6c). Furthermore, we retroactively found that Chameleon-7B can also be stably trained without dropout, when using norm-reordering, but QK-norm is essential in both cases. We plot training curves for the first 600k steps for both Chameleon-7B and Chameleon-34B in Figure 6a. Optimization Our training process uses the AdamW optimizer (Loshchilov and Hutter, 2017), with β₁ set to 0.9 and β₂ to 0.95, with an ε = 10⁻⁵. We use a linear warm-up of 4000 steps with an exponential decay schedule of the learning rate to 0. Additionally, we apply a weight decay of 0.1 and global gradient clipping at a threshold of 1.0. We use a dropout of 0.1 (Srivastava et al., 2014) for Chameleon-7B for training stability, but not for Chameleon-34B (see Figure 5c and 6c). The application of QK-Norm while helping the inner softmaxes within the Transformer does not solve the problem of logit shift in the final softmax. Following Chowdhery et al. (2022); Wortsman et al. (2023), we apply z-loss regularization. Specifically, we regularize the partition function Z of the softmax function σ(x)ᵢ = eˣⁱ / Z where Z = Σᵢ eˣⁱ by adding 10⁻⁵ log² Z to our loss function. For Chameleon-7B it was important to use both dropout and z-loss to achieve stability, while Chameleon-34B only required z-loss (Figure 6c). Chameleon-7B was trained with a global batch size of 2²³ (~8M) tokens and Chameleon-34B was trained with a global batch size of 3 × 2²² (~12M) tokens. We do 2.1 epochs over our full training dataset for a total

## Turn 2 — document page 6 (rank 2 of 20)

In section 2.3 Stability, the text states: "As inspired by Dehghani et al. (2023) and Wortsman et al. (2023), we first deviate from the Llama architecture by using query-key normalization (QK-Norm). QK-Norm directly controls the norm growth of input to the softmax by applying layer norm to the query and key vectors within the attention."

## Turn 3 — document page 8 (rank 3 of 20)

Table 1 shows that for LLaMa-1 (both 7B and 33B variants), the Qknorm column is marked with "×", indicating that QK-Norm was not applied.

## Turn 4 — document page 22 (rank 4 of 20)

This page contains a list of references, including papers by Wortsman et al. (2023), Yu et al. (2023), Zellers et al. (2019), Zhang and Sennrich (2019), and Zhou et al. (2023). None of these references directly address whether Llama-1 applies QK-Norm. The page does not contain any information relevant to the question about Llama-1 and QK-Norm.

## Turn 5 — document page 1 (rank 5 of 20)

This page is the introduction of the paper "Chameleon: Mixed-Modal Early-Fusion Foundation Models". It discusses the motivation for developing Chameleon, its architecture, and the challenges it addresses. It mentions "novel modifications to the transformer architecture, such as query-key normalization and revised placement of layer norms" as crucial for stable training in the mixed-modal setting. However, it does not mention Llama-1 or any specific details about whether Llama-1 applies QK-Norm.

## Turn 6 — document page 16 (rank 6 of 20)

none
