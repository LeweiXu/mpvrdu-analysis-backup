## Turn 1 — document page 13 (rank 1 of 20)

Table 8: Filtering statistics of the entity dataset. [1st Wiki filtering]: removing ones without wiki page. [2nd Google filtering]: removing ones without enough images via google search API. [3rd Wiki filtering]: removing entity name with ambiguous wiki pages.
| Main category | Original Entity | 1st Wiki filtering | 2nd Google filtering | 3rd Wiki filtering |
|---|---|---|---|---|
| landmark | 1595 | 1000 | 899 | 753 |
| painting | 1057 | 367 | 358 | 288 |
| sculpture | 300 | 164 | 164 | 134 |
| food | 883 | 338 | 337 | 271 |
| fruit | 361 | 236 | 233 | 180 |
| vegetable | 389 | 290 | 286 | 214 |
| mammal | 778 | 633 | 619 | 434 |
| hibian | 211 | 148 | 139 | 124 |
| insect | 366 | 179 | 176 | 145 |
| fish | 1089 | 1054 | 987 | 722 |
| bird | 739 | 546 | 545 | 480 |
| reptile | 279 | 232 | 231 | 210 |
| celebrity | 1514 | 1484 | 1466 | 732 |
| instrument | 477 | 375 | 368 | 277 |
| plant | 606 | 601 | 593 | 489 |
| electronics | 432 | 354 | 342 | 269 |
| tool | 801 | 213 | 209 | 150 |
| transportation | 334 | 296 | 290 | 227 |
| sport | 694 | 478 | 464 | 395 |
| book | 1030 | 826 | 777 | 645 |
| household | 475 | 319 | 299 | 221 |
| car | 500 | 320 | 320 | 208 |
| Summary | 22 | 14910 | 10453 | 10102 | 7568 |

Figure 6: Collecting images for building the evaluation dataset. Licenses: CC Publicdomain, CC Attribute, AA Sharealike, CC Noncommercial, or CC Nonderived licenses. Metadata: image URLs, source page URLs, renamed image names, and the corresponding Wikipedia page URL.
Knowledge retrieval via multi-source aggregation.
Semantic Region Extraction via Language-Guided Object Detection Due to the presence of entities within the image that occupy only a portion of the available space, employing a comprehensive image-level entity recognition approach may lead to a decrease in recognition performance. Instead, we opt to initially extract the image region containing the entity and utilize this specific region in subsequent recognition processes to enhance accuracy. During this phase, we leverage a language-guided object detection model, i.e., GLIP (Li et al., 2021), to extract meaningful regions from complex images. This approach helps precisely identify and extract image regions directly relevant to specific textual queries. It accomplishes this by understanding the context of the query and adjusting its object detection method to find the most

## Turn 2 — document page 1 (rank 2 of 20)

Figure 1: Comparing SnapNTell with existing methods reveals a distinctive focus. In the SnapNTell benchmark, the answers are predominantly entity-centric, characterized by a greater depth of knowledgeable information pertaining to the specific entity depicted in the image as the answer.

The figure includes a small image of the Eiffel Tower.

## Turn 3 — document page 15 (rank 3 of 20)

Figure 7: The architecture of our SnapNTell model. The input to the model is an image-question pair, and our model first uses retrieval augmentation to retrieve useful information regarding the entity in the image. Then, the retrieved information is combined with the question as input to the word embedding layer, where the text embeddings will be combined with image-projected embeddings as the input to LLM, which finally generates a knowledgeable answer as the output.

Figure 7 (diagram): Shows the SnapNTell model architecture. It includes an "Input Image" (which contains a small image of the Eiffel Tower), an "Entity Recognition Model" that outputs "Eiffel Tower", and a "Database" for "Retrieved Information". The diagram also shows "Input Question" (e.g., "What's the building in the image?"), "Retrieval Augmentation", "Word Embedding Layer", "Projection Layers", and "LLM" (Large Language Model) leading to "Answer".

D.2 Entity-centric Knowledge-based Answer Generation: The text mentions the model uses an "Entity Recognition Model" that identifies the "Eiffel Tower" from the input image. The diagram visually confirms this, showing the Eiffel Tower as the recognized entity.

## Turn 4 — document page 20 (rank 4 of 20)

This page contains two tables comparing model responses to image questions. The first table discusses "What is the name of the view in this picture?" and the second discusses "What is the age of the building now?". Neither table contains any information about the Eiffel Tower or its appearances in images. The images shown are of Lake Titicaca and the Chapel Bridge, not the Eiffel Tower.

## Turn 5 — document page 17 (rank 5 of 20)

This page contains Table 10, which lists the category statistics of the SnapNTell dataset. It shows the number of entities in each category, including "landmark" with 753 entities. The table also includes examples of images and questions from the dataset, but none of them feature the Eiffel Tower. The images shown are of Abel Tasman National Park, the Acropolis Museum, and the Saint Alexander Nevsky Cathedral.

## Turn 6 — document page 6 (rank 6 of 20)

Figure 3: Our SnapNTell model architecture takes an image-question pair as input. It begins with retrieval augmentation to source relevant information about the entity in the image. This information, along with the question, feeds into the word embedding layer. Text embeddings merge with image-projected embeddings before entering the LLM, culminating in a knowledgeable answer as the output.
The text describes the model's architecture and processes, including entity recognition via image retrieval and knowledge retrieval via multi-source aggregation. It mentions using a language-guided object detection model (GLIP) to extract regions relevant to textual queries and an image encoder (g(·)) synchronized with a text embedding space. The architecture is illustrated in Figure 3, which shows an "Input Image" and an "Entity Recognition Model" that outputs "Eiffel Tower" (as noted in previous pages). The text also references Figure 3 in the context of entity-centric knowledge-based answer generation.

## Turn 7 — document page 19 (rank 7 of 20)

This page contains Table 11 with example results and human evaluations for different models (BLIP2, MiniGPT4, Open-Flamingo, InstructBLIP, LLaVA, SnapNTell) answering questions about images. The images shown are of Abel Tasman National Park and the Acropolis Museum. None of the images on this page feature the Eiffel Tower.
