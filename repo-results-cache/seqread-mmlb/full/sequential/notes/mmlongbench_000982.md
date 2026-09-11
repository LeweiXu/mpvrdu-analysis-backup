## Turn 1 — document page 11 (rank 1 of 16)

Table 4: Demonstration templates and label words. Here <S1> represents the demonstration, <S> represents the input to be predicted, and <L> represents the label word corresponding to the demonstration. To save space, we only show one demonstration for each task.
| Task     | Template                          | Label Words                 |
|----------|-----------------------------------|-----------------------------|
| SST-2    | Review: <S1> Sentiment: <L> Review: <S> Sentiment: | Positive, Negative          |
| TREC     | Question: <S1> Answer Type: <L> Question: <S> Answer Type: | Abbreviation, Entity Description, Person Location, Number |
| AGNews   | Article: <S1> Answer: <L> Article: <S> Answer: | World, Sports Business, Technology |
| EmoC     | Dialogue: <S1> Emotion: <L> Dialogue: <S> Emotion: | Others, Happy Sad, Angry    |

Appendix
A Experimental Settings
For models, we use GPT2-XL (1.5B) (Radford et al., 2019) and GPT-J (6B) (Wang and Komatsuzaki, 2021) in this paper.
For datasets, we use a sentiment analysis task, Stanford Sentiment Treebank Binary (SST-2) (Socher et al., 2013), a question type classification task, Text REtrieval Conference Question Classification (TREC) (Li and Roth, 2002; Hovy et al., 2001), a topic classification task, AG's news topic classification dataset (AGNews) (Zhang et al., 2015), and an emotion classification task, Emo-Context (EmoC) (Chatterjee et al., 2019). The ICL templates of these tasks are shown in Table 4.

B Results of  \( S_{wp} \) ,  \( S_{pq} \) , and  \( S_{ww} \)  on TREC and EmoC
Figure 7 illustrates the relative sizes of  \( S_{wp} \) ,  \( S_{pq} \) , and  \( S_{ww} \)  on TREC and EmoC, mirroring results on SST-2 and AGNews. In shallow layers,  \( S_{wp} \)  (the information flow from the text part to label words) is prominent, while  \( S_{pq} \)  (the information flow from label words to targeted positions) is less significant. However, in deeper layers,  \( S_{pq} \)  dominates. Importantly,  \( S_{wp} \)  and  \( S_{pq} \)  generally exceed  \( S_{ww} \), indicating that interactions involving label words are predominant.

## Turn 2 — document page 3 (rank 2 of 16)

In shallow layers, the information flow from the text part to label words (S_wp) is high, while the information flow from label words to the target position (S_pq) is low. In deep layers, the information flow from label words to the target position (S_pq) becomes dominant.

## Turn 3 — document page 2 (rank 3 of 16)

Figure 2: Illustration of our hypothesis. In shallow layers, label words gather information from demonstrations to form semantic representations for deeper processing, while deep layers extract and utilize this information from label words to formulate the final prediction.

The text states: "H₁: In shallow layers, label words aggregate information from demonstration examples to form semantic representations for later computations. H₂: In deep layers, the model makes predictions by extracting information from label words."

## Turn 4 — document page 4 (rank 4 of 16)

Figure 3: Relative sizes of \( S_{wp} \), \( S_{pq} \), and \( S_{ww} \) in different layers on SST-2 and AGNews. Initially, \( S_{wp} \) occupies a significant proportion, but it gradually decays over layers, while \( S_{pq} \) becomes the dominant one.

Figure 4: The impact of isolating label words versus randomly isolating non-label words within the first or last 5 layers. Isolating label words within the first 5 layers exerts the most substantial impact, highlighting the importance of shallow-layer information aggregation via label words.

Text: "Initially, \( S_{wp} \) occupies a significant proportion, but it gradually decays over layers, while \( S_{pq} \) becomes the dominant one." and "Isolating label words within the first 5 layers exerts the most substantial impact, highlighting the importance of shallow-layer information aggregation via label words."

## Turn 5 — document page 5 (rank 5 of 16)

In deeper layers, there is a strong correlation between the attention distributions on the label words of the target position and the model's final prediction. The AUC-ROC metric for deep layers approaches 0.8, indicating a strong correlation. Shallow layers show negligible cumulative contributions (R_l), with a significant increase in middle and deep layers. These results signify the crucial role of deep layers for final prediction, validating that the model extracts information from label words in deep layers to form the final prediction.

## Turn 6 — document page 1 (rank 6 of 16)

- The abstract and introduction state that label words function as anchors: semantic information aggregates into label word representations during shallow computation layers, and the consolidated information in label words serves as a reference for the model's final predictions.
- Figure 1 visualizes the information flow, showing that label words gather information from demonstrations in shallow layers, which is then extracted in deep layers for final prediction.
- Footnote 2 defines "shallow" layers as those closer to the input and "deep" layers as those closer to the output, including those around the midpoint (e.g., layers 25-48 in a 48-layer GPT2-XL).
