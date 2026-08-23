Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models
A ADDITIONAL ERROR ANALYSIS
A.1 TIMEQA ERROR ANALYSIS
We conduct error analysis to understand where STEP-BACK PROMPTING fixes the errors the baseline models make. Figure 6 shows that compared to the predictions of baseline PaLM-2L, STEP-BACK PROMPTING is able to fix 39.9% of the predictions where the baseline prediction is wrong, while causing 5.6% errors. Furthermore, Step-Back + RAG fixes 21.6% errors coming from RAG. The % of errors introduced by STEP-BACK PROMPTING to RAG is still relatively low (6.3%). Together, this shows that the STEP-BACK PROMPTING is helpful most of the time, signifying the need and effectiveness of doing Abstraction before directly addressing the original question.


Figure 6: Error Analysis of Step-Back Prompting on TimeQA. Left: Step-Back + RAG vs Baseline predictions. Right: Step-Back RAG vs RAG predictions. Step-Back + RAG is able to fix 39.9% of the predictions where the baseline prediction is wrong, while causing 5.6% errors. Furthermore, Step-Back + RAG fixes 21.6% errors coming from RAG. The % of errors introduced by STEP-BACK PROMPTING to RAG is still relatively low (6.3%).
A.2 STRATEGYQA ERROR ANALYSIS
Figure 7 shows the error analysis of StrategyQA on the predictions of Step-Back + RAG against the baseline model and the raw retrieval augmentation variant of PaLM-2L. Compared to the baseline, Step-Back + RAG is able to turn 15.4% wrong predictions into correct predictions, while leading to 6.1% errors the other way around. Furthermore, Step-Back + RAG fixes 12.7% errors coming from RAG. The errors introduced to RAG by Step-Back is just 4.4%.
![](images/0.jpg)

![](images/1.jpg)

Figure 7: Error Analysis of Step-Back Prompting on StrategyQA. Left: Step-Back + RAG vs Baseline predictions. Right: Step-Back + RAG vs RAG predictions. Step-Back + RAG is able to turn 15.4% wrong predictions into correct predictions, while leading to 6.1% errors the other way around. Furthermore, Step-Back + RAG fixes 12.7% errors coming from RAG. The errors introduced to RAG by Step-Back is just 4.4%.
12