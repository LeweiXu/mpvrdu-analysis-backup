Knowledge QA Step-Back Prompt
You are an expert at world knowledge. Your task is to step back and paraphrase a question to a more generic step-back question, which is easier to answer. Here are a few examples:
Original Question: <Original Question Example1>
Stepback Question: <Stepback Question Example1>
...
Original Question: <Original Question Example5>
Stepback Question: <Stepback Question Example5>
Original Question: <Original Question>
Stepback Question:

<div style="text-align: center;">Table 10: Prompt of asking step-back question in Knowledge QA tasks.</div>



<table border=1 style='margin: auto; word-wrap: break-word;'><tr><td style='text-align: center; word-wrap: break-word;'>dataset</td><td style='text-align: center; word-wrap: break-word;'>Original Question</td><td style='text-align: center; word-wrap: break-word;'>Step-back Question</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>TimeQA</td><td style='text-align: center; word-wrap: break-word;'>Which position did Knox Cunningham hold from May 1955 to April 1956?</td><td style='text-align: center; word-wrap: break-word;'>Which positions have Knox Cunningham held in his career?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>TimeQA</td><td style='text-align: center; word-wrap: break-word;'>Who was the spouse of Anna Karina from 1968 to 1974?</td><td style='text-align: center; word-wrap: break-word;'>Who were the spouses of Anna Karina?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>TimeQA</td><td style='text-align: center; word-wrap: break-word;'>Which team did Thierry Audel play for from 2007 to 2008?</td><td style='text-align: center; word-wrap: break-word;'>Which teams did Thierry Audel play for in his career?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>TimeQA</td><td style='text-align: center; word-wrap: break-word;'>What was the operator of GCR Class 11E from 1913 to December 1922?</td><td style='text-align: center; word-wrap: break-word;'>What were the operators of GCR Class 11E in history?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>TimeQA</td><td style='text-align: center; word-wrap: break-word;'>Which country did Sokolovsko belong to from 1392 to 1525?</td><td style='text-align: center; word-wrap: break-word;'>Which countries did Sokolovsko belong to in history?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>SituatedQA</td><td style='text-align: center; word-wrap: break-word;'>When was the last time a team from Canada won the Stanley Cup as of 2002?</td><td style='text-align: center; word-wrap: break-word;'>When years did a team from Canada win the Stanley Cup as of 2002?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>SituatedQA</td><td style='text-align: center; word-wrap: break-word;'>When did England last get to the semi final in a world cup as of 2019?</td><td style='text-align: center; word-wrap: break-word;'>When years did England get to the semi final in a world cup as of 2019?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>SituatedQA</td><td style='text-align: center; word-wrap: break-word;'>What is the biggest hotel in Las Vegas as of November 28, 1993?</td><td style='text-align: center; word-wrap: break-word;'>What is the size of the hotel in Las Vegas as of November 28, 1993?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>SituatedQA</td><td style='text-align: center; word-wrap: break-word;'>Who has scored most runs in the 2017 matches as of 2017?</td><td style='text-align: center; word-wrap: break-word;'>What are the runs of players in the 2017 matches as of 2017?</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>SituatedQA</td><td style='text-align: center; word-wrap: break-word;'>Who is the highest paid player in the NBA this season as of 2017?</td><td style='text-align: center; word-wrap: break-word;'>What is the salary of the high paid players in the NBA this season as of 2017?</td></tr></table>

<div style="text-align: center;">Table 11: Few-shot demonstration exemplars for asking step-back questions in TimeQA and SituatedQA.</div>


### D.2 KNOWLEDGE QA

We use the following prompting in Table 10 to teach the LLM to ask a step-back question for TimeQA and SituatedQA including up to 5 exemplar demonstrations of pairs of Original Question and Step-back Question.

Table 11 shows 5 exemplars from the Train split of TimeQA and SituatedQA as demonstrations of asking step-back questions.

The step-back question is extracted from the model output using the prompt. Using the step-back question, we do retrieval augmentation. Using both the retrieval augmentations from the original question and the step-back question, we formulate the final prompt to query the model for the final answer, as shown in Table 12.