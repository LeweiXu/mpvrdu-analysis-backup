MMLU Physics/Chemistry First-Principle Prompt
You are an expert at Physics/Chemistry. You are given a Physics/Chemistry problem. Your task is to extract the Physics/Chemistry concepts and principles involved in solving the problem. Here are a few examples:
Question: <Question Example1>
Principles Involved: <Principles Example1>
...
Question: <Question Example5>
Principles Involved: <Principles Example5>
Question: <Question>
Principles Involved:

<div style="text-align: center;">Table 6: Prompt of extracting the underlying principles involved in MMLU physics and chemistry questions.</div>


MMLU Physics/Chemistry Final Answer Prompt
You are an expert at Physics/Chemistry. You are given a Physics/Chemistry problem and a set of principles involved in solving the problem. Solve the problem step by step by following the principles. Here are a few examples:
Question: <Question Example1>
Principles: <Principles Example1>
Answer: <Answer Example1>
...
Question: <Question Example5>
Principles: <Principles Example5>
Answer: <Answer Example5>
Question: <Question>
Principles: <Principles>
Answer:

<div style="text-align: center;">Table 7: Prompt of querying the model for final answer with first principles behind the question in MMLU high-school Physics and Chemistry.</div>


We found that out of 4 trials, the model scoring agrees with human ratings 97%, 98%, 99% and 99% of the time.

## D PROMPTS AND FEW SHOT EXAMPLES

### D.1 STEM

For MMLU high-school Physics and Chemistry, we first prompt the model to generate the first principles behind the question. Using the generated first principles, we further prompt the model to generate the final answer through few-shot demonstrations. The prompt generating first principles is shown in Table 6 for MMLU high-school Physics and Chemistry.

After extracting the first principles of solving a particular question, we formulate the prompt in Table 7 to query the model for the final answer.

Tables 8-9 show one demonstration exemplar of Question-Principles-Answer triplets for MMLU high-school Physics and Chemistry, respectively.