## Turn 1 — document page 2 (rank 1 of 20)

Figure 1: Tree construction process: RAPTOR recursively clusters chunks of text based on their vector embeddings and generates text summaries of those clusters, constructing a tree from the bottom up. Nodes clustered together are siblings; a parent node contains the text summary of that cluster.

The figure contains a diagram of a tree structure with nodes labeled with numbers (1 through 7). The diagram shows a hierarchical clustering process. Nodes 2, 3, and 4 are shown as siblings under a parent node. Nodes 5 and 6 are shown as siblings under another parent node. Node 7 is shown as a sibling to the cluster containing nodes 2, 3, and 4. The diagram also shows a "Contents of a node" box, which indicates that a node contains the text summaries of its child nodes.

## Turn 2 — document page 7 (rank 2 of 20)

Figure 4: Querying Process: Illustration of how RAPTOR retrieves information for two questions about the Cinderella story: “What is the central theme of the story?” and “How did Cinderella find a happy ending?”. Highlighted nodes indicate RAPTOR’s selections, while arrows point to DPR’s leaf nodes. Notably, RAPTOR’s context often encompasses the information retrieved by DPR, either directly or within higher-layer summaries.

The figure shows a tree-like structure with nodes labeled with numbers (0 through 26). Nodes 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, and 26 are depicted. Some nodes are highlighted with a white square border, indicating RAPTOR’s selections. Other nodes are shown with a red square border, indicating DPR’s leaf nodes. The figure also includes arrows pointing from RAPTOR’s highlighted nodes to DPR’s red-bordered nodes.

## Turn 3 — document page 22 (rank 3 of 20)

Figure 7: Histogram showing the percentage of nodes retrieved from different layers of the RAPTOR tree across three datasets (NarrativeQA, Quality, and Qasper) using three retrievers (SBERT, BM25, and DPR). The data indicate that a substantial portion of the nodes contributing to the final retrieval comes from non-leaf layers, with a notable percentage from the first and second layers, highlighting the importance of RAPTOR's hierarchical summarization in the retrieval process.

Table 15: Performance of RAPTOR when querying different layers of the tree for Story 3.
| Layers Queried / Start Layer | Layer 0 (Leaf Nodes) | Layer 1 | Layer 2 |
| :--- | :--- | :--- | :--- |
| 1 layer | 66.6 | 61.1 | 61.1 |
| 2 layers | - | 66.6 | 66.6 |
| 3 layers | - | - | 83.3 |

Table 16: Performance of RAPTOR when querying different layers of the tree for Story 4.
| Layers Queried / Start Layer | Layer 0 (Leaf Nodes) | Layer 1 |
| :--- | :--- | :--- |
| 1 layer | 94.7 | 84.2 |
| 2 layers | - | 89.4 |

Table 17: Performance of RAPTOR when querying different layers of the tree for Story 5.
| Layers Queried / Start Layer | Layer 0 (Leaf Nodes) | Layer 1 |
| :--- | :--- | :--- |
| 1 layer | 57.9 | 47.3 |
| 2 layers | - | 68.4 |

I.2 WHICH LAYERS DO RETRIEVED NODES COME FROM ?
We further conduct an ablation study across all three datasets and across three different retrievers with RAPTOR with the collapsed tree retrieval to examine the layers from which the retrieved nodes originate. We observe that between 18.5% to 57% of the retrieved nodes come from non-leaf nodes. As illustrated in Figure 7, the retrieval pattern across layers reveals the importance of RAPTOR's multi-layered tree structure. Notably, a significant percentage of the nodes retrieved by RAPTOR using the DPR retriever for the NarrativeQA dataset come from the first and second layers of the tree, as opposed to the leaf nodes. This pattern is consistent across the other datasets and retrievers, albeit with varying percentages.

Table 18: Percentage of nodes from non-leaf nodes across different datasets and retrievers
| Dataset | DPR | SBERT | BM25 |
| :--- | :--- | :--- | :--- |
| NarrativeQA | 57.36% | 36.78% | 34.96% |
| Quality | 32.28% | 24.41% | 32.36% |
| Qasper | 22.93% | 18.49% | 22.76% |

## Turn 4 — document page 16 (rank 4 of 20)

none

## Turn 5 — document page 5 (rank 5 of 20)

Figure 2: Illustration of the tree traversal and collapsed tree retrieval mechanisms. Tree traversal starts at the root level of the tree and retrieves the top-k (here, top-1) node(s) based on cosine similarity to the query vector. At each level, it retrieves the top-k node(s) from the child nodes of the previous layer's top-k. Collapsed tree collapses the tree into a single layer and retrieves nodes until a threshold number of tokens is reached, based on cosine similarity to the query vector. The nodes on which cosine similarity search is performed are highlighted in both illustrations.

The figure contains two diagrams labeled A. Tree Traversal Retrieval and B. Collapsed Tree Retrieval. In both diagrams, nodes are represented as colored rectangles. In diagram A, the nodes are colored in shades of blue and gray. In diagram B, the nodes are colored in shades of purple and gray. The text states that the nodes on which cosine similarity search is performed are highlighted in both illustrations.

## Turn 6 — document page 4 (rank 6 of 20)

none

## Turn 7 — document page 18 (rank 7 of 20)

none

## Turn 8 — document page 6 (rank 8 of 20)

Figure 3: Comparison of querying methods. Results on 20 stories from the QASPER dataset using tree traversal with different top-k values, and collapsed tree with different context lengths. Collapsed tree with 2000 tokens produces the best results, so we use this querying strategy for our main results.
The figure is a line chart with "Context Length" on the x-axis (in tokens, ranging from 500 to 2500) and "F1" on the y-axis (ranging from 0 to 1). It shows three lines: "Top 3", "Top 7", and "Top 9" for tree traversal, and "Collapsed tree" for the collapsed tree method. The "Collapsed tree" line is the highest, peaking at 1.0 F1 at 2000 tokens. The "Top 9" line is the second highest, followed by "Top 7" and then "Top 3". The chart indicates that collapsed tree with 2000 tokens produces the best results.

## Turn 9 — document page 23 (rank 9 of 20)

Table 19: Percentage of nodes from different layers with DPR as the retriever
| Layer | NarrativeQA | Quality | Qasper |
| :--- | :--- | :--- | :--- |
| 0 | 42.64% | 67.71% | 77.07% |
| 1 | 45.00% | 29.43% | 21.88% |
| 2 | 10.57% | 2.85% | 1.05% |
| 3 | 1.78% | - | - |
| 4 | 0.003% | - | - |

Table 20: Percentage of nodes from different layers with SBERT as the retriever
| Layer | NarrativeQA | Quality | Qasper |
| :--- | :--- | :--- | :--- |
| 0 | 63.22% | 75.59% | 81.51% |
| 1 | 31.51% | 22.78% | 17.84% |
| 2 | 4.85% | 1.63% | 0.65% |
| 3 | 0.42% | - | - |

Table 21: Percentage of nodes from different layers with BM25 as the retriever
| Layer | NarrativeQA | Quality | Qasper |
| :--- | :--- | :--- | :--- |
| 0 | 65.04% | 67.64% | 77.24% |
| 1 | 28.79% | 28.85% | 21.57% |
| 2 | 5.36% | 3.51% | 1.19% |
| 3 | 0.81% | - | - |

## Turn 10 — document page 15 (rank 10 of 20)

none

## Turn 11 — document page 1 (rank 11 of 20)

none

## Turn 12 — document page 3 (rank 12 of 20)

none

## Turn 13 — document page 17 (rank 13 of 20)

none

## Turn 14 — document page 19 (rank 14 of 20)

none

## Turn 15 — document page 9 (rank 15 of 20)

none

## Turn 16 — document page 8 (rank 16 of 20)

none

## Turn 17 — document page 21 (rank 17 of 20)

none

## Turn 18 — document page 20 (rank 18 of 20)

none

## Turn 19 — document page 10 (rank 19 of 20)

none

## Turn 20 — document page 13 (rank 20 of 20)

none
