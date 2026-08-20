# SnapNTell: Enhancing Entity-Centric Visual Question Answering with Retrieval Augmented Multimodal LLM

Jielin Qiu $ ^{1,2,*} $, Andrea Madotto $ ^{1} $, Zhaojiang Lin $ ^{1} $, Paul A. Crook $ ^{1} $, Yifan Ethan Xu $ ^{1} $, Xin Luna Dong $ ^{1} $, Christos Faloutsos $ ^{2} $, Lei Li $ ^{2} $, Babak Damavandi $ ^{1} $, Seungwhan Moon $ ^{1} $

 $ ^{1} $ Meta Reality Labs & FAIR, Meta  $ ^{2} $Carnegie Mellon University

{jielinq,leili,christos}@cs.cmu.edu, {andreamad8,zhaojiang,pacrook,ethanxu,lunadong,shanemoon}@meta.com

## Abstract

Vision-extended LLMs have made significant strides in Visual Question Answering (VQA). Despite these advancements, VLLMs still encounter substantial difficulties in handling queries involving long-tail entities, with a tendency to produce erroneous or hallucinated responses. In this work, we introduce a novel evaluative benchmark named SnapNTell, specifically tailored for entity-centric VQA. This task aims to test the models' capabilities in identifying entities and providing detailed, entity-specific knowledge. We have developed the SnapNTell Dataset, distinct from traditional VQA datasets: (1) It encompasses a wide range of categorized entities, each represented by images and explicitly named in the answers; (2) It features QA pairs that require extensive knowledge for accurate responses. The dataset is organized into 22 major categories, containing 7,568 unique entities in total. For each entity, we curated 10 illustrative images and crafted 10 knowledge-intensive QA pairs. To address this novel task, we devised a scalable, efficient, and transparent retrieval-augmented multimodal LLM. Our approach markedly outperforms existing methods on the SnapNTell dataset, achieving a 66.5% improvement in the BELURT score. We will soon make the dataset and the source code publicly accessible.

## 1 Introduction

Vision-extended LLMs have shown significant advancements, excelling at capturing complex semantics and context-aware attributes needed for intricate tasks. However, their abilities in factual VQA tasks, which demand accurate, concrete answers about real-world entities and phenomena, expose certain limitations. Particularly, torso-to-tail or long-tail entities, which constitute a large proportion of real-world data but appear infrequently in training datasets, pose a challenge. This scarcity

<div style="text-align: center;"><img src="imgs/img_in_image_box_876_589_1422_844.jpg" alt="Image" width="33%" /></div>


<div style="text-align: center;">Figure 1: Comparing SnapNTell with existing methods reveals a distinctive focus. In the SnapNTell benchmark, the answers are predominantly entity-centric, characterized by a greater depth of knowledgeable information pertaining to the specific entity depicted in the image as the answer.</div>


in representation often leads to VLLMs resorting to generating plausible but incorrect or imaginative content in their outputs, a problem that manifests as “hallucinations” within the context of model responses. To ensure the confident deployment of VLLMs in practical scenarios, there is an urgent need for dedicated research that not only recognizes but actively strives to tackle and reduce instances of hallucinations, especially in the context of factual queries involving these long-tail entities.

The lack of publicly available evaluation datasets specifically tailored to assess models’ ability in recognizing real-world long-tailed entities presents a notable gap in VQA. Existing datasets fall short in serving this purpose due to a narrow range of entity categories, the prevalence of overly simplistic yes/no QA pairs, and a general lack of entity specificity, often using broad terms like “Tiger” instead of more specific ones like “Siberian Tiger”. To address this gap, we introduce a novel evaluation task called SnapNTell, which focuses on entity-centric knowledge-based VQA. The SnapNTell benchmark has been designed to evaluate models’ abilities in accurately identifying entities and generating responses that showcase a deep understanding of these entities. To support this task, we have curated a new evaluation dataset that departs from existing datasets in two crucial ways: (1)