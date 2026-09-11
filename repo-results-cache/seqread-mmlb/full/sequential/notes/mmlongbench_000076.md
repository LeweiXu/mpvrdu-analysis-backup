## Turn 1 — document page 2 (rank 1 of 20)

Fig. 1. Technology tree of RAG research. The stages of involving RAG mainly include pre-training, fine-tuning, and inference. With the emergence of LLMs, research on RAG initially focused on leveraging the powerful in context learning abilities of LLMs, primarily concentrating on the inference stage. Subsequent research has delved deeper, gradually integrating more with the fine-tuning of LLMs. Researchers have also been exploring ways to enhance language models in the pre-training stage through retrieval-augmented techniques.

The figure is a tree diagram with three main branches: "Pre-training", "Fine-tuning", and "Inference". Each branch has sub-branches with specific RAG methods listed. The "Pre-training" branch is orange, the "Fine-tuning" branch is green, and the "Inference" branch is blue. The tree spans from 2020 to 2024, with specific RAG methods listed under each year.

## Turn 2 — document page 11 (rank 2 of 20)

Fig. 5. In addition to the most common once retrieval, RAG also includes three types of retrieval augmentation processes. (left) Iterative retrieval involves alternating between retrieval and generation, allowing for richer and more targeted context from the knowledge base at each step. (Middle) Recursive retrieval involves gradually refining the user query and breaking down the problem into sub-problems, then continuously solving complex problems through retrieval and generation. (Right) Adaptive retrieval focuses on enabling the RAG system to autonomously determine whether external knowledge retrieval is necessary and when to stop retrieval and generation, often utilizing LLM-generated special tokens for control.

The figure displays three distinct diagrams, each representing a type of retrieval augmentation process:
- Left: Iterative retrieval. It shows a loop where "Query" leads to "Retrieve", then "Generate", then "Judge", and back to "Retrieve" up to a "Max Times / Threshold". The output is "Response".
- Middle: Recursive retrieval. It shows a loop where "Query" leads to "Retrieve", then "Generate", then "Judge", then "Query Transformation / Decomposition", then back to "Retrieve". The output is "Response". It includes a "Max Depth (Tree) / Threshold".
- Right: Adaptive retrieval. It shows a decision point "Judge" after "Query", which can lead to "Retrieve On Demand" or directly to "Generate". The "Generate" step can lead to "Query Transformation / Decomposition" and back to "Retrieve", or to "Response". It includes a "Generate Special Token / Threshold".

## Turn 3 — document page 18 (rank 3 of 20)

none

## Turn 4 — document page 7 (rank 4 of 20)

Fig. 4. RAG compared with other model optimization methods in the aspects of “External Knowledge Required” and “Model Adaption Required”. Prompt Engineering requires low modifications to the model and external knowledge, focusing on harnessing the capabilities of LLMs themselves. Fine-tuning, on the other hand, involves further training the model. In the early stages of RAG (Naive RAG), there is a low demand for model modifications. As research progresses, Modular RAG has become more integrated with fine-tuning techniques.

The figure is a two-dimensional diagram with axes labeled “External Knowledge Required” (vertical, from Low to High) and “Model Adaption Required” (horizontal, from Low to High). The diagram shows a tree-like structure with a central node labeled “RAG”. From this central node, branches extend to different RAG methods and related techniques.

The branch labeled “Naive RAG” is positioned in the lower-left quadrant, indicating low requirements for both external knowledge and model adaptation. From “Naive RAG”, there is a branch labeled “XoT Prompt e.g. CoT, ToT” and another labeled “Few-shot Prompt”, both pointing to “Standard Prompt” which is connected to “Prompt Engineering”.

From “RAG”, there is a branch labeled “Advanced RAG” which includes “Index/pre-retrieval/post-retrieval optimization”. Another branch from “RAG” leads to “All of the above”, which connects to “Collaborative Fine-tuning” and “Generator Fine-tuning”. A third branch from “RAG” leads to “Retriever-Fine-tuning”.

The “Fine-tuning” branch is shown as a separate entity on the right side of the diagram, connected to “All of the above” and “Generator Fine-tuning”.

## Turn 5 — document page 1 (rank 5 of 20)

This page introduces the paper "Retrieval-Augmented Generation for Large Language Models: A Survey" and provides an overview of RAG's development. It mentions that the technology tree summarizing related research is shown in Figure 1. The text describes the evolution of RAG, starting with its inception coinciding with the rise of the Transformer architecture and focusing on enhancing language models through Pre-Training Models (PTM). It notes that after the arrival of ChatGPT, RAG research shifted towards the inference stage. The paper also states that RAG research has progressed to incorporate more with LLM fine-tuning techniques. The paper outlines its goal to map out the RAG process and chart its evolution, summarizing three main research paradigms: naive RAG, advanced RAG, and modular RAG.

## Turn 6 — document page 4 (rank 6 of 20)

Fig. 3. Comparison between the three paradigms of RAG. (Left) Naive RAG mainly consists of three parts: indexing, retrieval and generation. (Middle) Advanced RAG proposes multiple optimization strategies around pre-retrieval and post-retrieval, with a process similar to the Naive RAG, still following a chain-like structure. (Right) Modular RAG inherits and develops from the previous paradigm, showcasing greater flexibility overall. This is evident in the introduction of multiple specific functional modules and the replacement of existing modules. The overall process is not limited to sequential retrieval and generation; it includes methods such as iterative and adaptive retrieval.

The figure visually depicts three RAG paradigms as distinct branches of a tree:
- Left: Naive RAG, shown as a simple linear flow: User Query → Indexing → Retrieval → Prompt → Frozen LLM → Output.
- Middle: Advanced RAG, shown with a more complex flow including "Pre-Retrieval" and "Post-Retrieval" stages, with optimization modules like "Rewrite" and "Rerank" integrated.
- Right: Modular RAG, shown as a network of interconnected modules including "Search", "Retrieve", "Read", "Predict", "Fusion", "Memory", and "Rewrite", indicating a more flexible, non-sequential architecture.

The text below the figure states: "The modular RAG architecture advances beyond the former two RAG paradigms, offering enhanced adaptability and versatility." and "Despite its distinctiveness, Modular RAG builds upon the foundational principles of Advanced and Naive RAG, illustrating a progression and refinement within the RAG family."

## Turn 7 — document page 16 (rank 7 of 20)

Fig. 6. Summary of RAG ecosystem
- The figure is a diagram that summarizes the RAG ecosystem, divided into three main sections: "The RAG Paradigm", "Key Issues of RAG", and "Evaluation of RAG".
- Under "The RAG Paradigm", three paradigms are shown as branches: "Naive RAG", "Advanced RAG", and "Modular RAG", arranged from left to right, indicating a progression.
- "Key Issues of RAG" includes boxes for "What to retrieve", "When to retrieve", and "How to retrieve".
- "Evaluation of RAG" includes "Evaluation Target" (Retrieval Quality, Generation Quality), "Evaluation Aspects" (Answer Relevance, Context Relevance, etc.), and "Evaluation Framework" (CRUD, ROB, RECALL, ARES).

## Turn 8 — document page 3 (rank 8 of 20)

Fig. 2 illustrates the RAG process applied to question answering, showing three main steps: Indexing, Retrieval, and Generation. The diagram visually depicts the flow from "User Query" to "Relevant Documents" via "Indexing" and "Retrieval", and finally to "Generation" using an LLM to produce an "Answer". The figure also contrasts "without RAG" and "with RAG" outputs, highlighting the improvement in answer quality with RAG.

## Turn 9 — document page 8 (rank 9 of 20)

This page discusses indexing and query optimization techniques for RAG systems, but does not contain any figure or tree diagram that would allow identification of a branch with the least leaves. It details retrieval granularity, chunking strategies, metadata attachments, structural indexes, and query optimization methods like query expansion and sub-query planning, but none of these are presented in a tree structure relevant to the question.
