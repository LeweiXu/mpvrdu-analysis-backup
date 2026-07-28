Baseline few-shot Prompt

You are an expert of world knowledge and physics. Your task is to solve the following question. Here are a few examples:

Question: <Question Example>

Answer: <Answer Example>

Question: <Question>

Answer:

<div style="text-align: center;">Table 14: Prompt of querying the baseline model for final answer with few-shot demonstration exemplars.</div>


### D.4 BASELINE PROMPTS

For zero-shot baseline, we simply take the question itself and query the model for answers. For standard few-shot prompting of the baseline model, we formulate the prompt using the template in Table 14 with one exemplar. Table 15 shows the baseline few-shot exemplar exemplars used in this paper.

### D.5 CHAIN OF THOUGHT (CoT)

For zero-shot CoT prompting, we simply append Let's think step by step. to the question to query the model.

For few-shot CoT prompting, we use the same template as the Baseline prompting in Sec. D.4 by replacing the few-shot examples using CoT responses, as shown in Tables 16, 17, 18, and 19.

### D.6 TAKE A DEEP BREATHE (TDB)

We study the zero-shot Take a Deep Breathe prompting found in Yang et al. (2023): we take Take a deep breath and work on this problem step-by-step., and prepend it to the question.

## E EXAMPLES OF ERROR ANALYSIS AND WINS OF STEP-BACK PROMPTING

### E.1 MMLU ERROR ANALYSIS

In Tables 20-24, we show one example for each of the 5 error categories we identified through error analysis on STEP-BACK PROMPTING.

### E.2 EXAMPLE WINS FROM STEP-BACK PROMPTING

Tables 25-27, 28 29, 30 and 31 illustrate the some successful examples of STEP-BACK PROMPTING on MMLU-Physics, MMLU-Chemistry, TimeQA, SituatedQA, and StrategyQA respectively.