(2022), for image captioning with external database retrieval. Similarly, Gui et al. (2021) combined implicit and explicit knowledge in an encoder-decoder setup to improve answer generation.

Open-domain visual entity recognition Hu et al. (2023) developed OVEN for associating images with Wikipedia entities via text queries, while Chen et al. (2023) introduced INFOSEEK, a dataset for Visual Question Answering focused on informational queries. While OVEN is proficient in entity recognition using a knowledge base, INFOSEEK mainly supplies factual responses. Our study seeks to merge these strengths, creating detailed paragraphs that provide context for a more comprehensive understanding beyond basic facts. More related work can be found in Appendix E.

## 3 SnapNTell Dataset

### 3.1 Entity Categorization

To tackle the challenge of the new SnapNTell task, the first step involves creating a comprehensive dataset that represents a wide array of real-world entities. Our dataset creation methodology entails selecting a diverse set of entity names from various categories that mirror the diversity of the real world. This selection encompasses both commonly encountered entities and less frequently encountered ones. We have identified 22 categories that adequately represent a cross-section of entities one might encounter in daily life. These categories include landmark, painting, sculpture, food, fruit, vegetable, mammal, amphibian, insect, fish, bird, reptile, celebrity, instrument, plant, electronics, tool, transportation, sport, book, household, and car. More details about the categories can be referred to Table 10 in the Appendix.

To populate each category with specific entities, we leveraged Wikipedia as a primary resource due to its extensive and detailed entries. (See Appendix A for more details.) Our selection criteria are heavily biased towards specificity; for instance, in the category of mammals, we deliberately opted for precise names such as “German Shepherd” or “Alaskan Malamute” instead of the generic “Dog”. This level of specificity is critical as it enables the model to demonstrate its capacity for fine-grained recognition and its ability to generate detailed, accurate information about each entity. This dataset-building approach is what distinguishes our dataset from existing VQA datasets, which often lack fine-grained entities and specificity.

### 3.2 Image collection

The dataset comprises 22 primary categories, encapsulating a total of 7,568 unique entities. For each individual entity, a set of 10 images has been curated, where the statistic of the entity list is shown in Table 10 in the Appendix.

Filtering Initially, a comprehensive list of entities, encompassing 22 primary categories, was compiled, in a total of 14,910 diverse entities. Then the entity list underwent filtering by cross-referencing each entry with its corresponding Wikipedia page. Entities lacking valid Wikipedia pages were subsequently removed from the list. For each corresponding entity, images were sourced from Creative Commons (CC). Further filtering was conducted by removing entities that didn’t have a sufficient number of images obtained via Google Image Search engine. The collected metadata was stored in a CSV file containing essential information such as image URLs, source page URLs, renamed image names, and the corresponding Wikipedia page URLs. After filtering, the final number of entities in the SnapNTell dataset is 7,568. (More filtering details can be found in Appendix B.)

### 3.3 Knowledge-intensive Question-Answer Pairs

In our SnapNTell dataset, we considered five types of questions:

• Static facts (absolute facts, discrete facts). These are objective facts that are concrete and are not contingent on other conditions. They can usually be answered with a unique answer. i.e., “When was he (Barack Obama) born?”

• Narrative facts. These facts encompass comprehension of larger contexts (e.g., song lyrics, movie plot). They are factual in the sense that the content of the narrative should accurately reflect the source material or events, but a correct answer is usually not unique, as they can vary in their level of detail and focus. i.e., "What is the plot of that ('The Godfather')?"

• Dynamic facts. These are facts that are subject to change over time. i.e., “What is the Yelp customer rating of it (the Eleven Madison Park restaurant) in NYC?”

• Procedural facts. These are usually answers to “how” questions, outlining a sequence of steps to accomplish a task. While the steps may not be unique and could be subjective,