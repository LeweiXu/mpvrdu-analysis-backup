<div style="text-align: center;"><img src="imgs/img_in_image_box_211_194_1450_867.jpg" alt="Image" width="74%" /></div>


<div style="text-align: center;">Figure 7: The architecture of our SnapNTell model. The input to the model is an image-question pair, and our model first uses retrieval augmentation to retrieve useful information regarding the entity in the image. Then, the retrieved information is combined with the question as input to the word embedding layer, where the text embeddings will be combined with image-projected embeddings as the input to LLM, which finally generates a knowledgeable answer as the output.</div>


### D.2 Entity-centric Knowledge-based Answer Generation

Following the preceding step, where we’ve gathered insightful information from diverse sources, we now proceed to the second phase: determining how to integrate the input image, the question, and the retrieved information in order to produce a knowledge-driven response.

Our approach is illustrated in Figure 7. Our strategy for improving the model’s multimodal comprehension entails pre-training a LLM using paired multimodal data, which comprises images alongside corresponding textual descriptions. To achieve this, we draw inspiration from Moon et al. (2023) and create lightweight adapters for each modality. These adapters facilitate the transformation of inputs into the text token embedding space of a designated LLM.

Our approach transforms the text token embedding space of the LLM into a unified token embedding space, where tokens can represent either textual or image content. The number of token embeddings allocated to each input modality is predetermined for each adapter, ranging from 64 to 256. Throughout the alignment training process, we keep the model parameters of the underlying LLM frozen. This approach not only accelerates convergence compared to training the model from scratch but also allows the model to inherit the reasoning capabilities of the LLM during inference. Additionally, to maximize feature compatibility, we employ an encoder denoted as  $ g(\cdot) $ for the image modality. This encoder has previously been aligned with a text embedding space, for instance, in the case of CLIP (Radford et al., 2021; Schuhmann et al., 2022). For each pair of text and image, represented as  $ (\mathbf{X}_{\text{text}}, \mathbf{X}_{\text{image}}) $, we align them using specific objectives along with a projection module, such as the Perceiver Resampler (Alayrac et al., 2022) for the vision encoder.

 $$ p(\mathbf{X}_{text}|\mathbf{X}_{image})=\prod_{i=1}^{L}p_{\theta}(\mathbf{X}_{text}^{[i]}|\mathbf{Z}_{image},\mathbf{Z}_{text}^{[1:i-1]}) $$ 

 $$ \mathbf{Z}_{\mathrm{i m a g e}}=\mathtt{P r o j}_{\theta}(h_{\mathrm{l a t e n t s}},g(\mathbf{X}_{\mathrm{i m a g e}})) $$