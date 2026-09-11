## Turn 1 — document page 18 (rank 1 of 20)

## Algorithm 1 Tree Traversal Algorithm

function TRAVERSETREE(tree, query, k)
    S_current ← tree.layer[0]
    for layer in range(tree.num_layers) do
    top_k ← []
    for node in S_current do
    score ← dot_product(query, node)
    top_k.append((node, score))
    end for
    S_layer ← sorted(top_k)[:k].nodes
    S_current ← S_layer
    end for
    return S₀ ∪ S₁ ∪ S₂ ∪ … ∪ S_k
end function

## Turn 2 — document page 4 (rank 2 of 20)

none

## Turn 3 — document page 19 (rank 3 of 20)

## Algorithm 2 Collapsed Tree Algorithm

function COLLAPSED TREE(tree, query, k, max_tokens)
    tree ← flatten(tree) ▷ Flatten tree into 1D
    top_nodes ← []
    for node in tree do
    top_nodes.append((node, dot_product(query, node))
    end for
    top_nodes ← sorted(top_nodes)
    result ← []
    total_tokens ← 0
    for node in top_nodes do
    if total_tokens + node.token.size < max_tokens then
    result.append(node)
    end if
    total_tokens ← total_tokens + node.token.size
    end for
    return result
end function

Table 12: Relevant excerpts from text retrieved by RAPTOR and DPR for the questions on the fairytale Cinderella.

## Turn 4 — document page 5 (rank 4 of 20)

## Algorithm 1 Tree Traversal Algorithm

function TRAVERSETREE(tree, query, k)
    S_current ← tree.layer[0]
    for layer in range(tree.num_layers) do
    top_k ← []
    for node in S_current do
    score ← dot_product(query, node)
    top_k.append((node, score))
    end for
    S_layer ← sorted(top_k)[:k].nodes
    S_current ← S_layer
    end for
    return S₀ ∪ S₁ ∪ S₂ ∪ … ∪ S_k
end function

## Algorithm 2 Collapsed Tree Algorithm

function COLLAPSED TREE(tree, query, k, max_tokens)
    tree ← flatten(tree) ▷ Flatten tree into 1D
    top_nodes ← []
    for node in tree do
    top_nodes.append((node, dot_product(query, node))
    end for
    top_nodes ← sorted(top_nodes)
    result ← []
    total_tokens ← 0
    for node in top_nodes do
    if total_tokens + node.token.size < max_tokens then
    result.append(node)
    end if
    total_tokens ← total_tokens + node.token.size
    end for
    return result
end function

Figure 2: Illustration of the tree traversal and collapsed tree retrieval mechanisms. Tree traversal starts at the root level of the tree and retrieves the top-k (here, top-1) node(s) based on cosine similarity to the query vector. At each level, it retrieves the top-k node(s) from the child nodes of the previous layer's top-k. Collapsed tree collapses the tree into a single layer and retrieves nodes until a threshold number of tokens is reached, based on cosine similarity to the query vector. The nodes on which cosine similarity search is performed are highlighted in both illustrations.

3. Proceed to the child nodes of the elements in set \( S_{1} \). Compute the cosine similarity between the query vector and the vector embeddings of these child nodes.
4. Select the top \( k \) child nodes with the highest cosine similarity scores to the query, forming the set \( S_{2} \).
5. Continue this process recursively for \(d\) layers, producing sets \(S_{1}, S_{2}, \ldots, S_{d}\).
6. Concatenate sets \( S_{1} \) through \( S_{d} \) to assemble the relevant context to the query.

The collapsed tree approach offers a simpler way to search for relevant information by considering all nodes in the tree simultaneously, as depicted in Figure 2. Instead of going layer-by-layer, this method flattens the multi-layered tree into a single layer, essentially bringing all the nodes onto the same level for comparison. The steps for this method are outlined below:

1. First, collapse the entire RAPTOR tree into a single layer. This new set of nodes, denoted as \( C \), contains nodes from every layer of the original tree.
2. Next, calculate the cosine similarity between the query embedding and the embeddings of all nodes present in the collapsed set \( C \).
3. Finally, pick the top-k nodes that have the highest cosine similarity scores with the query. Keep adding nodes to the result set until you reach a predefined maximum number of tokens, ensuring you don't exceed the model's input limitations.

## Turn 5 — document page 2 (rank 5 of 20)

none

## Turn 6 — document page 3 (rank 6 of 20)

none

## Turn 7 — document page 7 (rank 7 of 20)

none

## Turn 8 — document page 6 (rank 8 of 20)

none

## Turn 9 — document page 21 (rank 9 of 20)

none

## Turn 10 — document page 16 (rank 10 of 20)

none

## Turn 11 — document page 8 (rank 11 of 20)

none

## Turn 12 — document page 20 (rank 12 of 20)

none

## Turn 13 — document page 23 (rank 13 of 20)

none

## Turn 14 — document page 22 (rank 14 of 20)

none

## Turn 15 — document page 9 (rank 15 of 20)

none

## Turn 16 — document page 15 (rank 16 of 20)

none

## Turn 17 — document page 1 (rank 17 of 20)

none

## Turn 18 — document page 10 (rank 18 of 20)

none

## Turn 19 — document page 13 (rank 19 of 20)

none

## Turn 20 — document page 14 (rank 20 of 20)

none
