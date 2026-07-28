It includes a wide range of fine-grained and categorized entities, each accompanied by corresponding images and clear mention of the entity name within the answer sets. (2) It features QA pairs designed to prompt knowledge-intensive responses, moving beyond the binary yes/no format to challenge and assess the depth of the model's comprehension.

Furthermore, the limitations identified in factual query generation underscore the need for new solutions to address the problem of hallucinations. Recent advancements suggest that retrieval-based approaches hold significant promise in this regard (Guu et al., 2020; Srinivasan et al., 2022; Yang et al., 2023a,b). These methods enhance LLMs by integrating external knowledge sources or incorporating retrieval mechanisms to access relevant information from extensive knowledge bases. The synergy between the advanced inference capabilities of LLMs and the wealth of external knowledge has the potential to significantly reduce issues related to long-tail entities and, consequently, decrease the occurrence of hallucinatory responses.

In this work, we aim to propose an evaluation task to investigate the model’s ability to recognize real-world long-tailed entities and provide knowledge-intensive answers. We also propose a retrieval-augmented method to reduce hallucinations and enhance the precision and trustworthiness of generated responses.

Our contribution is summarized as follows:

• SnapNTell task. We propose a novel task for entity-centric VQA, specifically designed to assess the proficiency of models in accurately identifying and generating responses that exhibit a deep comprehension of these identified entities.

• SnapNTell model. We proposed a retrieval-augmented multimodal LLM, devised as a baseline model capable of undertaking the SnapNTell task, which is scalable, effective, and explainable.

• SnapNTell dataset. We collected a new evaluation dataset with distinctive characteristics, which stands out for two key features: (1) It encompasses a diverse range of fine-grained entities, each accompanied by corresponding representative images. (2) The question-answer pairs contain knowledge-intensive responses with entity names specifically mentioned in the answer sets.

• Our model demonstrates superior performance on the SnapNTell dataset, surpassing current methodologies with a 66.5% improvement in BELURT score.



## 2 Related Works

Knowledge-based VQA Research in vision-language tasks, which necessitate understanding image content to answer questions, has seen significant advancements over recent years. Beginning with datasets like FVQA (Wang et al., 2016), which extracted facts from pre-established knowledge bases, the field has progressed to more challenging ones like the OK-VQA dataset (Marino et al., 2019), encompassing diverse knowledge categories. MultiModalQA (Talmor et al., 2021) introduced complexity with questions demanding cross-modal reasoning over snippets, tables, and images. The successor of OK-VQA, AOK-VQA (Schwenk et al., 2022), raises the bar by providing questions that transcend simple knowledge base queries. ManyModalQA (Hannan et al., 2020) shifts the focus to answer modality selection, MIMOQA (Singh et al., 2021) emphasizes multimodal answer extraction, and WebQA (Chang et al., 2021) introduces real-world knowledge-seeking questions, albeit with some limitations regarding entity categorization and granularity. More comparison details can be found in Section 3.5.

Multimodal LLMs Integrating visual understanding into text-based LLM typically combines them with a visual encoder and uses image captioning datasets for alignment (Koh et al., 2023; Wu et al., 2023; Chowdhery et al., 2022). Techniques like adapter-based tuning (Alayrac et al., 2022) and prefix tuning (Tsimpoukelli et al., 2021) allow these models to process visual inputs while maintaining their linguistic capabilities, without requiring full model retraining (Yin et al., 2023).

Retrieval-augmented LLM Previous studies have explored retrieval augmentation in text-only settings or image captioning tasks. Guu et al. (2020) introduced a retriever for language models to access large corpus during various stages. Srinivasan et al. (2022) showed retrieval-augmented queries enhance LLMs' context understanding. Yasunaga et al. (2023) and Yang et al. (2023a) developed methods for integrating multimodal documents and speeding up LLM inference, respectively. Yang et al. (2023b) created a visual language model, inspired by Flamingo (Alayrac et al.,