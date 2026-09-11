## Turn 1 — document page 15 (rank 1 of 20)

Figure 7: The architecture of our SnapNTell model. The input to the model is an image-question pair, and our model first uses retrieval augmentation to retrieve useful information regarding the entity in the image. Then, the retrieved information is combined with the question as input to the word embedding layer, where the text embeddings will be combined with image-projected embeddings as the input to LLM, which finally generates a knowledgeable answer as the output.

D.2 Entity-centric Knowledge-based Answer Generation
Following the preceding step, where we've gathered insightful information from diverse sources, we now proceed to the second phase: determining how to integrate the input image, the question, and the retrieved information in order to produce a knowledge-driven response.
Our approach is illustrated in Figure 7. Our strategy for improving the model's multimodal comprehension entails pre-training a LLM using paired multimodal data, which comprises images alongside corresponding textual descriptions. To achieve this, we draw inspiration from Moon et al. (2023) and create lightweight adapters for each modality. These adapters facilitate the transformation of inputs into the text token embedding space of a designated LLM.
Our approach transforms the text token embedding space of the LLM into a unified token embedding space, where tokens can represent either textual or image content. The number of token embeddings allocated to each input modality is predetermined for each adapter, ranging from 64 to 256. Throughout the alignment training process, we keep the model parameters of the underlying LLM frozen. This approach not only accelerates convergence compared to training the model from scratch but also allows the model to inherit the reasoning capabilities of the LLM during inference. Additionally, to maximize feature compatibility, we employ an encoder denoted as \( g(\cdot) \) for the image modality. This encoder has previously been aligned with a text embedding space, for instance, in the case of CLIP (Radford et al., 2021; Schuhmann et al., 2022). For each pair of text and image, represented as \( (\mathbf{X}_{\mathrm{text}}, \mathbf{X}_{\mathrm{image}}) \), we align them using specific objectives along with a projection module, such as the Perceiver Resampler (Alayrac et al., 2022) for the vision encoder.

\[
p (\mathbf {X} _ {\text { text }} | \mathbf {X} _ {\text { image }}) = \prod_ {i = 1} ^ {L} p _ {\theta} (\mathbf {X} _ {\text { text }} ^ {[ i ]} | \mathbf {Z} _ {\text { image }}, \mathbf {Z} _ {\text { text }} ^ {[ 1: i - 1 ]}) \tag {3}
\]

\[
\mathbf {Z} _ {\text { image }} = \operatorname{Proj} _ {\theta} (h _ {\text { latents }}, g (\mathbf {X} _ {\text { image }})) \tag {4}
\]

Figure 7: The architecture of our SnapNTell model. The input to the model is an image-question pair, and our model first uses retrieval augmentation to retrieve useful information regarding the entity in the image. Then, the retrieved information is combined with the question as input to the word embedding layer, where the text embeddings will be combined with image-projected embeddings as the input to LLM, which finally generates a knowledgeable answer as the output.

D.2 Entity-centric Knowledge-based Answer Generation
Following the preceding step, where we've gathered insightful information from diverse sources, we now proceed to the second phase: determining how to integrate the input image, the question, and the retrieved information in order to produce a knowledge-driven response.
Our approach is illustrated in Figure 7. Our strategy for improving the model's multimodal comprehension entails pre-training a LLM using paired multimodal data, which comprises images alongside corresponding textual descriptions. To achieve this, we draw inspiration from Moon et al. (2023) and create lightweight adapters for each modality. These adapters facilitate the transformation of inputs into the text token embedding space of a designated LLM.
Our approach transforms the text token embedding space of the LLM into a unified token embedding space, where tokens can represent either textual or image content. The number of token embeddings allocated to each input modality is predetermined for each adapter, ranging from 64 to 256. Throughout the alignment training process, we keep the model parameters of the underlying LLM frozen. This approach not only accelerates convergence compared to training the model from scratch but also allows the model to inherit the reasoning capabilities of the LLM during inference. Additionally, to maximize feature compatibility, we employ an encoder denoted as \( g(\cdot) \) for the image modality. This encoder has previously been aligned with a text embedding space,

## Turn 2 — document page 1 (rank 2 of 20)

![](images/0.jpg)

Figure 1: Comparing SnapNTell with existing methods reveals a distinctive focus. In the SnapNTell benchmark, the answers are predominantly entity-centric, characterized by a greater depth of knowledgeable information pertaining to the specific entity depicted in the image as the answer.

## Turn 3 — document page 6 (rank 3 of 20)

none

## Turn 4 — document page 12 (rank 4 of 20)

Figure 5 shows the pertinent information collected during dataset building from Wikipedia for the entity "Yosemite National Park". The figure displays a Wikipedia article page for Yosemite National Park, with sections for "General intro", "Toponym", and "Location" highlighted. The entity is explicitly labeled as "Yosemite National Park".

## Turn 5 — document page 5 (rank 5 of 20)

Figure 2: Comparison with existing datasets, where previous VQA datasets mostly focus on freeform answers (such as yes/no for verification questions and choice for selection questions).

The figure displays three example question-answer pairs:
- Q: Is the umbrella upside down? A: No
- Q: What animal is in the box? A: Bear
- Q: Is the photo from the 50's or the 90's? A: 50's

Below these, a fourth example is shown:
- Q: What is the current status of it? A: The Mendenhall Glacier is currently experiencing a negative glacier mass balance and will likely continue to retreat.

## Turn 6 — document page 17 (rank 6 of 20)

Figure 8 displays three example image-question-answer pairs from the SnapNTell dataset. The images shown are:
1. Abel Tasman National Park (with the question "Where is it located?")
2. The Acropolis Museum (with the question "What date did the it open to the public?")
3. The Saint Alexander Nevsky Cathedral (with the question "What is the architectural style of it?")

## Turn 7 — document page 19 (rank 7 of 20)

Table 11 shows example results from different models, including SnapNTell (M6). The first example image is labeled as "Abel Tasman National Park" and the question is "Where is the attraction located?". The SnapNTell answer correctly identifies the location as Abel Tasman National Park in the South Island of New Zealand. The second example image is labeled as "The Acropolis Museum" with the question "What date did it open to the public?". The SnapNTell answer correctly identifies the opening date as June 20, 2009.
