## Turn 1 — document page 5 (rank 1 of 20)

Figure 3: Sythus overview. We employ a cold-start stage to identify the optimal system message and in-context example for querying instruction-response pairs in a given dataset. Subsequently, Sythus, spanning steps 1 to 4, generates high-quality instruction-response pairs in eight languages.

The figure shows a flowchart with four steps:
- Step 1: System Message + visual annotation
- Step 2: Generate instruction-response pairs
- Step 3: Filtering
- Step 4: Translation

An arrow points from "Cold Start" to "Step 1". The "Cold Start" box is positioned above "Step 1" and has arrows pointing to it from "Step 2" and "Step 3", indicating it is a preceding stage.

## Turn 2 — document page 11 (rank 2 of 20)

none

## Turn 3 — document page 2 (rank 3 of 20)

Figure 1: MIMIC-IT overview. The MIMIC-IT dataset comprises 2.8M multi-modal instruction-response pairs spanning fundamental capabilities: perception, reasoning, and planning. Each instruction is accompanied by multi-modal conversational context, allowing VLMs trained on MIMIC-IT to demonstrate strong proficiency in interactive instruction following with zero-shot generalization.

The figure visually depicts three main branches: Perception, Reasoning, and Planning. Each branch contains example instruction-response pairs. For instance, under Perception, there are questions like "What is the difference between the two images?" and "Write a detailed description of the given image." Under Reasoning, examples include "What might be the purpose of this gathering?" and "Is it safe to walk on the floor while the woman is cleaning?" Under Planning, there are prompts like "Can you suggest any ways to brighten up the room?" and "Can you suggest any international permits that can be enjoyed within this room?"

The text below the figure states that Sythus employs system message, visual annotation, and in-context examples to direct the language model in generating instruction-response pairs based on visual context, including timestamps, captions, and object information, targeting three fundamental capabilities: perception, reasoning, and planning.

## Turn 4 — document page 7 (rank 4 of 20)

Figure 4 displays data statistics of multi-modal in-context instruction-response pairs. It includes:
- (a) Instructions: A circular plot showing root verb-noun pairs, with the inner circle representing the root verb of the output response and the outer circle representing direct nouns.
- (b) Responses: A similar circular plot for responses.
- (c) Statistics of instructions and responses, retaining 25% of Ego4D instructions for a more balanced distribution. The caption notes that “# Related instructions” denotes the number of related instructions in an instance, given the same set of visual input data.

The section “3.3.2 Egocentric View Understanding” discusses two scenarios:
- Indoor Event Planning (IEP): Uses 2D photos of rooms to generate instructions for activities, starting with creating a personality for the room owner.
- Ego4D (E4D): Uses egocentric videos to simulate AR assistant interactions, with example prompts like “What should I do now?” and responses like “Based on my observation, you can now proceed to do....”

Section “3.4 Dataset Statistics” states the dataset comprises over 2.8 million instruction-response pairs, with 2.2M unique instructions. It references Figure 4 (a) and (b) for verb-noun structure analysis.

## Turn 5 — document page 4 (rank 5 of 20)

Figure 2 visually compares LLaVA-Instruct-150K and MIMIC-IT data formats. LLaVA-Instruct-150K uses a single image with language-only in-context information (highlighted in a yellow box). MIMIC-IT, in contrast, accommodates multiple images or videos and supports multi-modal in-context information, considering both visual and language inputs.

Section 3.1 "MIMIC-IT Data Format" defines each instance as a tuple (I_q, R_q, X_q), where I_q is the instruction, R_q is the response, and X_q is a set of N images or videos. The data format includes in-context examples represented as (I_k, R_k, X_k) for k=1 to M, and the full data representation is d_q = (I_q, R_q, X_q, C_ψ(I_q, X_q)), where C_ψ is a context function that maps the query to its in-context examples.

## Turn 6 — document page 10 (rank 6 of 20)

This page contains Figure 6, which presents evaluation results for the model Otter. The figure includes three subplots:
- (a) Video understanding: A bar chart comparing accuracy of Otter against VideoChatGPT and other models on MSVD and QA captioning benchmarks.
- (b) Vision-language model alignment: A bar chart showing Elo ratings for various models, with Otter achieving the highest rating.
- (c) COCO caption: A line chart comparing CIDEr scores for different models, including Otter, OpenFlamingo, and others, across various few-shot settings.

The text discusses the evaluation metrics, including the use of ChatGPT to compare model predictions with ground truth labels. It also mentions that Otter outperforms VideoChatGPT in video understanding and OpenFlamingo in few-shot in-context learning. The page discusses human evaluation using the Elo rating system and the limitations of the current approach, such as language hallucinations from ChatGPT.
