## Turn 1 — document page 7 (rank 1 of 20)

Figure 4: Querying Process: Illustration of how RAPTOR retrieves information for two questions about the Cinderella story: “What is the central theme of the story?” and “How did Cinderella find a happy ending?”. Highlighted nodes indicate RAPTOR’s selections, while arrows point to DPR’s leaf nodes. Notably, RAPTOR’s context often encompasses the information retrieved by DPR, either directly or within higher-layer summaries.

The figure shows a diagram with nodes labeled 0 through 26. Nodes 16, 17, 18, 19, 20, 21, 22 are highlighted with a red box and labeled "RAPTOR retrieved for Question 1". Nodes 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 are highlighted with a red box and labeled "RAPTOR retrieved for Question 2". Arrows point from the RAPTOR-retrieved nodes to corresponding DPR-retrieved nodes (e.g., from node 16 to node 0, from node 17 to node 1, etc.).

## Turn 2 — document page 6 (rank 2 of 20)

This page discusses the experimental setup and qualitative study of RAPTOR, mentioning Figure 4 in the context of a qualitative analysis comparing RAPTOR's retrieval process to DPR methods. It references Figure 4 as illustrating RAPTOR's ability to choose nodes from different tree layers for thematic, multi-hop questions using a 1500-word Cinderella fairytale. However, it does not contain the specific details of which nodes are retrieved for each question or any information about common nodes between the two questions.

## Turn 3 — document page 18 (rank 3 of 20)

This page discusses hallucinations in summarization and the impact on QA tasks, and provides pseudocode for RAPTOR's tree traversal algorithm. It references Figure 4 in the main paper for qualitative analysis of RAPTOR's retrieval process on Cinderella questions. However, it does not contain any new information about which specific nodes are retrieved by RAPTOR for each question or any information about common nodes between the two questions. The page does not contradict or add to the previous answer.

## Turn 4 — document page 19 (rank 4 of 20)

The current page contains Table 12, which shows relevant excerpts from text retrieved by RAPTOR and DPR for the two questions about Cinderella. The table provides the textual content retrieved by RAPTOR for each question, but it does not list the specific node identifiers (e.g., 16, 17, etc.) that were selected by RAPTOR. The table only shows the textual summaries generated from the retrieved nodes. The page also discusses the qualitative differences between RAPTOR and DPR retrieval, noting that RAPTOR's context is more comprehensive for multi-hop questions, but it does not provide any information about the node IDs for the second question or any overlap between the two sets of retrieved nodes.

## Turn 5 — document page 22 (rank 5 of 20)

This page contains Figure 7, which shows a histogram of the percentage of nodes retrieved from different layers of the RAPTOR tree across three datasets (NarrativeQA, Quality, and Qasper) using three retrievers (SBERT, BM25, and DPR). It also includes Tables 15, 16, and 17, which show the performance of RAPTOR when querying different layers of the tree for Stories 3, 4, and 5, respectively. Table 18 shows the percentage of nodes from non-leaf nodes across different datasets and retrievers. However, none of this content provides specific information about which nodes (e.g., 16, 17, etc.) were retrieved by RAPTOR for the two questions in Figure 4, nor does it provide any information about common nodes between the two sets. The page discusses the layer distribution of retrieved nodes but does not address the specific node IDs for the Cinderella questions.

## Turn 6 — document page 5 (rank 6 of 20)

This page contains Figure 2, which illustrates the tree traversal and collapsed tree retrieval mechanisms of RAPTOR. It explains the algorithmic steps for both methods, including how cosine similarity is used to select top-k nodes at each layer for tree traversal, and how the collapsed tree approach flattens the tree into a single layer for simultaneous retrieval. The page discusses the performance comparison between the two methods on the QASPER dataset and argues that collapsed tree retrieval is more flexible and effective. However, this page does not contain any information about Figure 4, the specific nodes retrieved by RAPTOR for the two Cinderella questions, or any information about common nodes between the two sets.
