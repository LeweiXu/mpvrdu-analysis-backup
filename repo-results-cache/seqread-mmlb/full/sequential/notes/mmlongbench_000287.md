## Turn 1 — document page 10 (rank 1 of 10)

A.1 Prompts for Claim Verifier
Claim = Superdrag and Collective Soul are both rock bands.
We already know the following:
Question 1 = Is Superdrag a rock band?
Answer 1 = Yes
Can we know whether the claim is
true or false now? Yes or no?
Prediction = No, we cannot know.
Claim = Superdrag and Collective Soul are both rock bands.
We already know the following:
Question 1 = Is Superdrag a rock band?
Answer 1 = Yes
Question 2 = Is Collective Soul a rock band?
Answer 2 = Yes
Can we know whether the claim is
true or false now? Yes or no?
Prediction = Yes, we can know.
<10 demonstrations in total>
Claim = [[CLAIM]]
Claim = CLAIM
We already know the following:
[[QA_CONTEXTS]]
Can we know whether the claim is
true or false now? Yes or no?
Prediction =
A.2 Prompts for Question Generation Prompts for the initial question generation
Claim = Superdrag and Collective Soul are both rock bands.
To verify the above claim, we can
first ask a simple question:
Question = Is Superdrag a rock band?
<10 demonstrations in total>
Claim = [[CLAIM]]
To verify the above claim, we can
first ask a simple question:
Question =
Prompts for the follow-up question generation
Claim = Superdrag and Collective Soul are both rock bands.
We already know the following:
Question 1 = Is Superdrag a rock band?
Answer 1 = Yes
To verify the claim, what is the
next question we need to know the
answer to?
Question 2 = Is Collective Soul a rock band?
<10 demonstrations in total>
[EMPTY]
Claim = [[CLAIM]]
We already know the following:
[[QA_CONTEXTS]]
To verify the claim, what is the
next question we need to know the
answer to?
Question [[Q_INDEX]] =
A.3 Prompts for Validator
Claim = Superdrag and Collective Soul are
both rock bands.
We already know the following:
Question = Is Superdrag a rock band?
Answer = Yes
Now we further know:
Question = Is Collective Soul a rock band?
Answer = Yes
Does the QA pair have additional
knowledge useful for verifying the claim?
The answer: Yes
<10 demonstrations in total>
Claim = [[CLAIM]]
We already know the following:
[[QA_CONTEXTS]]
Now we further know:
[[NEW_QA_PAIR]]
Does the QA pair have additional
knowledge useful for verifying the claim?
The answer:
A.4 Prompts for Reasoner
Contexts:
Q1: When Lars Onsager won the Nobel Prize?
A1: 1968
Q2: When was Lars Onsager born?
A2: 1903
Claim = Lars Onsager won the Nobel Prize when he was 30 years old.
Is this claim true or false?
Answer:
Lars Onsager won the Nobel Prize in 1968.
Lars Onsager was born in 1903.
Therefore, the final answer is: False.
<10 demonstrations in total>
Contexts:
[[CONTEXTS]]
Claim = [[CLAIM]]
Is this claim true or false?
Answer:
Therefore, the final answer is

## Turn 2 — document page 3 (rank 2 of 10)

none

## Turn 3 — document page 6 (rank 3 of 10)

none

## Turn 4 — document page 4 (rank 4 of 10)

- The page discusses three QA module implementations: Retriever-Reader, FLAN-T5, and GPT Reciter-Reader.
- It mentions the QA Validator module, which uses ten demonstrations shown in Appendix A.3.
- The validator prompts InstructGPT with a specific instruction format involving a claim, context, and new QA pair.
- The validator ensures QA pairs are useful for verifying the claim and adds valid pairs to the context.
- The page references Appendix A.3 for the ten demonstrations used in the validator.

## Turn 5 — document page 5 (rank 5 of 10)

Figure 4 shows the QACHECK user interface with annotated functions for claim verification.
Section 3.5 describes the Reasoner module, which is called when the claim verifier determines the context is sufficient or the maximum iterations (set to 5) are reached.
The reasoner takes context C and claim c as inputs and answers “Is the claim true or false?” while outputting a rationale.
Two implementations are provided: 1) an end-to-end QA model based on FLAN-T5, and 2) the InstructGPT model with prompts from Appendix A.4.
Section 4 begins discussing performance evaluation using datasets HOVER and FEVEROUS.

## Turn 6 — document page 1 (rank 6 of 10)

none
