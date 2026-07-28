## A More Details about the Dataset Building

More details about the dataset building process are shown in Figure 5.

<div style="text-align: center;"><img src="imgs/img_in_image_box_238_339_1401_1289.jpg" alt="Image" width="70%" /></div>


<div style="text-align: center;">Figure 5: The pertinent information collected during dataset building, i.e., from Wikipedia for each entity, which includes the summary of the general introduction, toponym, lococation information, and so on.</div>


## B More Details about the Filtering Process

More details about the filtering process are shown in Table 8.

## C Types of Questions

More introduction of different types of question in the SnapNTell dataset are shown Table 9.

## D Method

In this section, we will introduce the details of our proposed retrieval-augmented multimodal LLM model. The architecture of our model is shown in Figure 7. Our model can be considered twofold: (1) Retrieval augmentation. Given the input image-question pair, we retrieve useful entity-centric information within knowledge sources. (2) Entity-centric knowledge-based answer generation. The retrieved information will be combined with the image and question together to generate the answer. More details are introduced in the following sections.

### D.1 Retrieval Augmentation

The retrieval augmentation process can be subdivided into three distinct steps: (i) Semantic region extraction via language-guided object detection, (ii) Entity recognition via image retrieval, and (iii)