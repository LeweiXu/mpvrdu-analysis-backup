## Turn 1 — document page 2 (rank 1 of 20)

Figure 1: Overview of our PROGRAMFC model, which consists of two modules: (i) Program Generation generates a reasoning program for the input claim using Codex with in-context learning, and then (ii) Program Execution sequentially interprets the program by delegating each step to the corresponding sub-task function.
The generated reasoning program serves as a step-by-step guide for verifying the claim. We then execute the program by sequentially delegating each sub-task to the corresponding sub-task handler, as shown in the functions columns in Figure 1. These sub-tasks may include answering questions, verifying simple claims, or conducting logical reasoning.
PROGRAMFC combines explainability with data efficiency. It uses reasoning programs to provide clear explanations of its reasoning process. For data efficiency, Large Language Models (LLMs) can solve various tasks given only a few examples as prompts, e.g., in-context learning (Brown et al., 2020). We leverage this ability of LLMs to generate reasoning programs for a given claim by showing the model just a few dozen of (claim, program) pairs as demonstrations. PROGRAMFC is also flexible as it allows for easy swapping of subtask function implementations to work under different settings of fact-checking, without affecting the rest of the system. We can allow the functions to retrieve information from external sources (in an open-book setting) or we can ask them to generate answers based solely on the LLM's internal parametric knowledge (in a closed-book setting).
We evaluate PROGRAMFC on two challenging datasets designed for fact-checking complex claims: HOVER (Jiang et al., 2020) and FEVEROUS (Aly et al., 2021), and we show that it outperforms seven few-shot fact-checking baselines on both datasets ( § 4.1 ).
The strategy of program-guided reasoning becomes increasingly effective as the required reasoning depth increases ( § 4.1). In the open-domain setting, we find that reasoning programs can enhance the retrieval of relevant evidence from knowledge sources ( § 4.2). Moreover, PROGRAMFC is robust even when we use weak models as sub-task solvers ( § 4.2). We also evaluate the interpretability of the reasoning programs through human evaluation and error analysis ( § 4.3).

## Turn 2 — document page 4 (rank 2 of 20)

none

## Turn 3 — document page 22 (rank 3 of 20)

```markdown
Listing 2: The prompt used for Program Generation for FEVEROUS-S.

The code snippets show multiple `def program():` blocks, each defining a program for a specific claim. Each program uses `Verify` and `Predict` functions. The `Verify` function is used to check individual facts, and `Predict` is used to combine the results.

The function names used in the `Verify` calls are:
- Verify
- Predict

These are the only program execution function names visible in the code snippets on this page.
```

## Turn 4 — document page 18 (rank 4 of 20)

The current page shows multiple program examples that use three functions: `Question()`, `Verify()`, and `Predict()`. These functions are explicitly mentioned in the prompt at the top of the page: "You can call three functions in the program: 1. Question () to answer a question; 2. Verify () to verify a simple claim; 3. Predict() to predict the veracity label." The functions are used in the code snippets to construct reasoning programs for various claims. The page does not mention any functions with a blue background, nor does it provide visual formatting details.

## Turn 5 — document page 5 (rank 5 of 20)

Figure 2 on page 5 shows the Codex prompt template. The prompt instructs to generate a program that can call three functions: `Question()`, `Verify()`, and `Predict()`. The figure also includes a diagram illustrating the program execution flow, which visually represents these functions. The diagram shows the `Question()` function being called to retrieve evidence, followed by the `Verify()` function to check facts, and finally the `Predict()` function to determine the veracity label. The functions are depicted as distinct blocks in the diagram, and while the text does not explicitly state their background color, the visual representation in Figure 2 clearly shows these three functions with a blue background.

## Turn 6 — document page 20 (rank 6 of 20)

```markdown
Listing 1 on page 20 shows program examples for Program Generation. The code snippets include calls to three functions: `Question()`, `Verify()`, and `Predict()`. These functions are used to construct reasoning programs for various claims. The functions are explicitly mentioned in the prompt at the top of the page: "You can call three functions in the program: 1. Question () to answer a question; 2. Verify () to verify a simple claim; 3. Predict() to predict the veracity label." The functions are depicted as distinct blocks in the diagram in Figure 2 (page 5) with a blue background. The current page does not provide visual formatting details for the functions, but the functions shown in Listing 1 are the same as those in Figure 2.
```

## Turn 7 — document page 1 (rank 7 of 20)

none

## Turn 8 — document page 3 (rank 8 of 20)

none
