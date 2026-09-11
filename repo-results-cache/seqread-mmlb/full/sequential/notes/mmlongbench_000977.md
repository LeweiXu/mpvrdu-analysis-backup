## Turn 1 — document page 23 (rank 1 of 20)

C.2 Illustration of the Three Rungs of the Causal Ladder
In Figure 7, we illustrate the difference among the three rungs by enumerating what actions are performed on the variables other than target variables X and Y.
![](images/0.jpg)

Figure 7: The Causal Ladder consists of three rungs: association, intervention and counterfactuals. We color in blue the treatment X and effect Y, as well as the actions on X. We color in orange words about how to get the estimand, and we use the orange circle to include all the non-descendants of X.

## Turn 2 — document page 3 (rank 2 of 20)

## 2.1 The Ladder of Causation
The Ladder of Causation, introduced by Pearl and Mackenzie [66], is a proposed taxonomy, and hierarchy, of causal inference tasks [3]. It consists of three distinct rungs.
Rung 1 (“seeing”). This describes statistical associations (“How often do I take an aspirin when I have a headache?”). Rung 1 deals with statistical dependences among random variables, and involves probabilistic reasoning about joint and conditional distributions, $ P(X = x, Y = y) $ and $ P(Y = y | X = x) $, which can be formalised through Bayesian Networks [12, 58] representing a set of variables and their conditional dependencies via a directed acyclic graph (DAG).
Rung 2 (“doing”). This enables us to formalize the concept of actively intervening in the world, and modifying it toward some end (“If I take an aspirin now, will my headache subside?”). Interventions can be formalized using the do-operator [24] and Causal Bayesian Networks [67] to represent, for example, the distribution over Y when intervening on X to set its value to x as $ P(Y = y|\text{do}(X = x)) $.
Rung 3 (“imagining”). This rung deals with counterfactual reasoning, i.e., reasoning about alternative scenarios in which the world could have been different, possibly even contradicting the factual state (“Would my headache have subsided, if I had taken an aspirin?”). Counterfactual probabilities can be written as $ P(Y_{x} = y) $, representing the probability that “Y would be y, had X been x”. Reasoning about Rung 3 quantities requires the introduction of Structural Causal Models (SCMs) [67]. SCMs are especially powerful as they enable any quantity in Rungs 1, 2, and 3 to be formulated precisely [3].

## Turn 3 — document page 2 (rank 3 of 20)

## Figure 1: Example question in our CLADDER dataset featuring an instance of Simpson's paradox [63].

The figure presents a causal question, its ground-truth answer, and a step-by-step explanation. The text below the figure clarifies that the CLADDER dataset covers causal queries across the three rungs of the Ladder of Causation: associational (Rung 1), interventional (Rung 2), and counterfactual (Rung 3).

The text explicitly states: "We compose more than 10,000 causal questions that cover a variety of causal queries across the three rungs of the Ladder of Causation [3, 66]—i.e., associational (Rung 1), interventional (Rung 2), and counterfactual (Rung 3)."

## Turn 4 — document page 4 (rank 4 of 20)

## Figure 2: The data-generating process of the CLADDER dataset.

The formal part of the question generation (top half of the figure) samples inputs for the CI Engine and derives a ground truth answer. The bottom part describes the natural language part of the question generation—i.e., its verbalization, based on multiple stories and different degrees of alignment with commonsense knowledge.

The formal part includes a box labeled "Sample a query type" which lists:
- Rung 1: Association
- Rung 2: Intervention
- Rung 3: Counterfactuals

The text below the figure states: "In the composition of our dataset, we adhere to the following design principles. First, we ensure broad coverage of all rungs of the ladder of causation."

## Turn 5 — document page 10 (rank 5 of 20)

This page discusses the CLADDER benchmark and its coverage of causal inference across the three rungs of the Ladder of Causation. It mentions that the dataset covers "all three rungs" and specifically references "Rung 1: Association", "Rung 2: Intervention", and "Rung 3: Counterfactuals" in the context of query type sampling. The text also notes that the work covers "commonly studied causal queries spanning all three rungs" and that future work may extend to other queries. However, this page does not provide any new information that contradicts or corrects the previous answer.

## Turn 6 — document page 5 (rank 6 of 20)

## 3.1 Formal Part of the Question Formulation

### Selecting Query Types
The text explicitly lists query types for each rung:
- For Rung 1: probability distributions such as marginal and conditional probabilities.
- For Rung 2: average treatment effects (ATE) (“how will Y change if X changes from x to x’?”), or what constitutes a valid adjustment set.
- For Rung 3: counterfactuals (“what would happen to Y had X been x’ instead of x?”), average treatment effect on the treated (ATT), natural direct effect (NDE), and natural indirect effect (NIE).

The text also states: “For Rung 2 questions, we can enquire average treatment effects (ATE) (“how will Y change if X changes from x to x’?”), or what constitutes a valid adjustment set that can block all backdoor spurious correlations between X and Y.”
