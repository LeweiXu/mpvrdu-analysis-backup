Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models
Table 4: Stats of the evaluation datasets used in this paper.
<table><tr><td>Domain</td><td>Dataset</td><td>Split</td><td>Number of Examples</td></tr><tr><td>STEM</td><td>MMLU high-school Physics MMLU high-school Chemistry</td><td>Test Test</td><td>151 203</td></tr><tr><td>Knowledge QA</td><td>TimeQA TimeQA Easy TimeQA Hard SituatedQA</td><td>Test Test Test Test</td><td>5226 2613 2613 2901</td></tr><tr><td>Multi-hop Reasoning</td><td>MuSiQue StrategyQA</td><td>Dev Dev</td><td>2417 229</td></tr></table>
Are the following two answers to the given question equivalent? Do not consider whether the answers are right or wrong, but only whether they are equivalent. Directly state "Yes" or "No".
Question: Which title was conferred to Anna Muzychuk in 2007?
Answer 1: Anna Muzychuk was conferred the title of International Master (IM) in 2007. She earned the title by scoring three norms in rapid chess tournaments.
Answer 2: International Master
Answer 1 (short): International Master
Answer 2 (short): International Master
Are the two answers equivalent? Yes
Question: What state is Seattle located in?
Answer 1: Seattle is in Washington State.
Answer 2: The answer is George Washington.
Answer 1 (short): Washington State
Answer 2 (short): George Washington
Are the two answers equivalent? No
Question: <Question>
Answer 1: <Model Output>
Answer 2: <Target Label>
Table 5: Illustration of few shot evaluation with the PaLM-2L model.
B DATASET DETAILS
Table 4 shows the split and number of examples used for evaluations in TimeQA, StrategyQA and MMLU high-school Physics.
C EVALUATION DETAILS
C.1 FEW-SHOT EXAMPLES FOR EVALUATION WITH PALM2-L
Given the model free-form outputs and the target label, we use one positive and one negative outputs as few-shot examples to teach the scoring model how to score the output. Table 5 illustrates the prompt we used for the scoring model. We parse out the “Yes” or “No” answer from the scoring model output as TRUE or FALSE score of the model output.
C.2 HYPER-PARAMETERS FOR EVALUATION WITH PALM2-L
We use PaLM-2L as the scoring model for evaluation. We experiment with different sampling temperatures, and find that T = 1 gives us a highly-accurate evaluating. For example, we sampled 100 test examples and the model predictions, and manually rated the correctness of the model scoring.
13