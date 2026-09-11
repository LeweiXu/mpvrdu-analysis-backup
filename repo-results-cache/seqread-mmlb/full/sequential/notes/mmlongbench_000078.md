## Turn 1 — document page 8 (rank 1 of 20)

In text, retrieval granularity ranges from fine to coarse, including Token, Phrase, Sentence, Proposition, Chunks, Document. Among them, DenseX [30] proposed the concept of using propositions as retrieval units. Propositions are defined as atomic expressions in the text, each encapsulating a unique factual segment and presented in a concise, self-contained natural language format. This approach aims to enhance retrieval precision and relevance. On the Knowledge Graph (KG), retrieval granularity includes Entity, Triplet, and sub-Graph. The granularity of retrieval can also be adapted to downstream tasks, such as retrieving Item IDs [40] in recommendation tasks and Sentence pairs [38]. Detailed information is illustrated in Table I.

B. Indexing Optimization
In the Indexing phase, documents will be processed, segmented, and transformed into Embeddings to be stored in a vector database. The quality of index construction determines whether the correct context can be obtained in the retrieval phase.
1) Chunking Strategy: The most common method is to split the document into chunks on a fixed number of tokens (e.g., 100, 256, 512) [88]. Larger chunks can capture more context, but they also generate more noise, requiring longer processing time and higher costs. While smaller chunks may not fully convey the necessary context, they do have less noise. However, chunks leads to truncation within sentences, prompting the optimization of a recursive splits and sliding window methods, enabling layered retrieval by merging globally related information across multiple retrieval processes [89]. Nevertheless, these approaches still cannot strike a balance between semantic completeness and context length. Therefore, methods like Small2Big have been proposed, where sentences (small) are used as the retrieval unit, and the preceding and following sentences are provided as (big) context to LLMs [90].
2) Metadata Attachments: Chunks can be enriched with metadata information such as page number, file name, author, category timestamp. Subsequently, retrieval can be filtered based on this metadata, limiting the scope of the retrieval. Assigning different weights to document timestamps during retrieval can achieve time-aware RAG, ensuring the freshness of knowledge and avoiding outdated information.
In addition to extracting metadata from the original documents, metadata can also be artificially constructed. For example, adding summaries of paragraph, as well as introducing hypothetical questions. This method is also known as Reverse HyDE. Specifically, using LLM to generate questions that can be answered by the document, then calculating the similarity between the original question and the hypothetical question during retrieval to reduce the semantic gap between the question and the answer.
3) Structural Index: One effective method for enhancing information retrieval is to establish a hierarchical structure for the documents. By constructing In structure, RAG system can expedite the retrieval and processing of pertinent data.
Hierarchical index structure. File are arranged in parent-child relationships, with chunks linked to them. Data summaries are stored at each node, aiding in the swift traversal of data and assisting the RAG system in determining which chunks to extract. This approach can also mitigate the illusion caused by block extraction issues.
Knowledge Graph index. Utilize KG in constructing the hierarchical structure of documents contributes to maintaining consistency. It delineates the connections between different concepts and entities, markedly reducing the potential for illusions. Another advantage is the transformation of the information retrieval process into instructions that LLM can comprehend, thereby enhancing the accuracy of knowledge retrieval and enabling LLM to generate contextually coherent responses, thus improving the overall efficiency of the RAG system. To capture the logical relationship between document content and structure, KGP [91] proposed a method of building an index between multiple documents using KG. This KG consists of nodes (representing paragraphs or structures in the documents, such as pages and tables) and edges (indicating semantic/lexical similarity between paragraphs or relationships within the document structure), effectively addressing knowledge retrieval and reasoning problems in a multi-document environment.
C. Query Optimization
One of the primary challenges with Naive RAG is its direct reliance on the user's original query as the basis for retrieval. Formulating a precise and clear question is difficult, and imprudent queries result in subpar retrieval effectiveness. Sometimes, the question itself is complex, and the language is not well-organized. Another difficulty lies in language complexity ambiguity. Language models often struggle when dealing with specialized vocabulary or ambiguous abbreviations with multiple meanings. For instance, they may not discern whether “LLM” refers to large language model or a Master of Laws in a legal context.
1) Query Expansion: Expanding a single query into multiple queries enriches the content of the query, providing further context to address any lack of specific nuances, thereby ensuring the optimal relevance of the generated answers.
Multi-Query. By employing prompt engineering to expand queries via LLMs, these queries can then be executed in parallel. The expansion of queries is not random, but rather meticulously designed.
Sub-Query. The process of sub-question planning represents the generation of the necessary sub-questions to contextualize

## Turn 2 — document page 6 (rank 2 of 20)

| Method | Retrieval Source | Retrieval Data Type | Retrieval Granularity | Augmentation Stage | Retrieval process |
|---|---|---|---|---|---|
| CoG [29] | Wikipedia | Text | Phrase | Pre-training | Iterative |
| DenseX [30] | FactoidWiki | Text | Proposition | Inference | Once |
| EAR [31] | Dataset-base | Text | Sentence | Tuning | Once |
| ... | ... | ... | ... | ... | ... |
| PaperQA [53] | Arxiv, Online Database, PubMed | Text | Chunk | Inference | Iterative |
| NoiseRAG [54] | FactoidWiki | Text | Chunk | Inference | Once |
| IAG [55] | Search Engine, Wikipedia | Text | Chunk | Inference | Once |
| NoMIRACL [56] | Wikipedia | Text | Chunk | Inference | Once |
| ToC [57] | Search Engine, Wikipedia | Text | Chunk | Inference | Recursive |
| SKR [58] | Dataset-base, Wikipedia | Text | Chunk | Inference | Adaptive |
| ITRG [59] | Wikipedia | Text | Chunk | Inference | Iterative |
| RAG-LongContext [60] | Dataset-base | Text | Chunk | Inference | Once |
| ITER-RETGEN [14] | Wikipedia | Text | Chunk | Inference | Iterative |
| IRCALM [64] | Pile, Wikipedia | Text | Chunk | Inference | Iterative |
| Retrieve-and-Sample [65] | Dataset-base | Text | Doc | Tuning | Once |
| Zemi [66] | C4 | Text | Doc | Tuning | Once |
| CRAG [67] | Arxiv | Text | Doc | Inference | Once |
| 1-PAGER [68] | Wikipedia | Text | Doc | Inference | Iterative |
| PRCA [69] | Dataset-base | Text | Doc | Inference | Once |
| QLM-Doc-ranking [70] | Wikipedia | Text | Doc | Inference | Once |
| Recomp [71] | Wikipedia | Text | Doc | Inference | Once |
| DSP [23] | Wikipedia | Text | Doc | Inference | Iterative |
| RePLUG [72] | Pile | Text | Doc | Inference | Once |
| ARM-RAG [73] | Dataset-base | Text | Doc | Inference | Iterative |
| GenRead [13] | LLMs | Text | Doc | Inference | Iterative |
| UniMS-RAG [74] | Dataset-base | Text | Multi | Tuning | Once |
| CREA-ICL [19] | Dataset-base | Crosslingual,Text | Sentence | Inference | Once |
| PKG [75] | LLM | Tabular,Text | Chunk | Inference | Once |
| SANTA [76] | Dataset-base | Code,Text | Item | Pre-training | Once |
| SURGE [77] | Freebase | KG | Sub-Graph | Tuning | Once |
| MK-ToD [78] | Dataset-base | KG | Entity | Tuning | Once |
| Dual-Feedback-ToD [79] | Dataset-base | KG | Entity Sequence | Tuning | Once |
| KnowledgeGPT [15] | Dataset-base | KG | Triplet | Inference | Multi-time |
| FABULA [80] | Dataset-base,Graph | KG | Entity | Inference | Once |
| HyKGE [81] | CMeKG | KG | Entity | Inference | Once |
| KALMV [82] | Wikipedia | KG | Triplet | Inference | Iterative |
| RoG [83] | Freebase | KG | Triplet | Inference | Iterative |
| G-Retriever [84] | Dataset-base | TextGraph | Sub-Graph | Inference | Once |

## Turn 3 — document page 7 (rank 3 of 20)

- The current page discusses retrieval granularity and mentions CoG [29] in the context of legal domains.
- It references CoG [29] as an example of a method that works with domain-specific data, specifically legal domains.
- The page does not provide the full title of the paper proposing CoG, only the citation [29].

## Turn 4 — document page 1 (rank 4 of 20)

The current page is the title page of a survey paper titled "Retrieval-Augmented Generation for Large Language Models: A Survey". It lists the authors and their affiliations. The abstract and introduction are also visible, discussing the purpose of the paper, which is to provide a comprehensive review of RAG methods, paradigms, and evaluation frameworks. The paper is identified by the arXiv identifier arXiv:2312.10997v5 [cs.CL] and dated 27 Mar 2024.

## Turn 5 — document page 16 (rank 5 of 20)

This page contains Figure 6, a summary diagram of the RAG ecosystem, and the conclusion section of the paper. It discusses the evolution of RAG, its integration with other AI methodologies, and its expansion into multimodal domains. It mentions specific methods like RA-CM3, BLIP-2, GSS, UEOP, Vid2Seq, RBPS, and CoK, but does not provide the full title of any paper proposing a method with phrase-level retrieval granularity. The page also reiterates the paper's conclusion that RAG enhances LLMs by integrating external knowledge, and outlines its three developmental paradigms: Naive, Advanced, and Modular RAG.

## Turn 6 — document page 2 (rank 6 of 20)

- The current page (page 2) contains Figure 1, a technology tree of RAG research, and the beginning of Section II, "OVERVIEW OF RAG".
- It outlines the three main paradigms of RAG: Naive RAG, Advanced RAG, and Modular RAG.
- It mentions that research initially focused on the inference stage and has since expanded to include fine-tuning and pre-training.
- The page does not contain any information about a paper proposing a method with phrase-level retrieval granularity.

## Turn 7 — document page 5 (rank 7 of 20)

- The current page discusses retrieval granularity and mentions methods like CoG [29], DenseX [30], EAR [31], PaperQA [53], etc., in the context of RAG.
- It references CoG [29] as an example of a method that works with domain-specific data, specifically legal domains.
- The page does not provide the full title of the paper proposing CoG, only the citation [29].
- The page also mentions DenseX [30] which uses propositions as retrieval units, but does not provide the full title of the paper proposing DenseX.
- The page discusses various RAG methods and their retrieval granularity, including phrase-level retrieval, but does not explicitly state which paper proposes a method with phrase-level retrieval granularity.
