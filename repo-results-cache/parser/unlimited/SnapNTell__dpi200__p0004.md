Table 1: More detailed comparison with existing knowledge-based VQA datasets. Anonymity means whether the question already contains a knowledge clue related to the entity in question. (* Unclear)
<table><tr><td>Dataset</td><td>Categories</td><td>Unique Entity</td><td>QA Pairs</td><td>Images</td><td>Average Ans Length</td><td>Number of Images / Entity</td><td>Anonymity</td></tr><tr><td>ViQuAE</td><td>3</td><td>2,400</td><td>3,700</td><td>3,300</td><td>1.8</td><td>*</td><td>✕</td></tr><tr><td>Encyclopedia VQA (test)</td><td>12</td><td>*</td><td>5,750</td><td>5,750</td><td>3.2</td><td>*</td><td>✕</td></tr><tr><td>SnapNTell (Ours)</td><td>22</td><td>7,568</td><td>75,680</td><td>75,680</td><td>25.7</td><td>10</td><td>✓</td></tr></table>
Table 2: Comparison with existing VQA datasets Knowledge means the QA pairs are knowledgeable, not simple yes/no answers or selection questions. Entities means whether there are fine-grained entities specifically contained in answers. Categorization means the entities are categorized, not randomly crawled online.
<table><tr><td>Dataset</td><td>Knowledge</td><td>Entities</td><td>Categorization</td></tr><tr><td>VQA 2.0 (Goyal et al., 2016)</td><td></td><td></td><td></td></tr><tr><td>GQA (Hudson and Manning, 2019)</td><td></td><td></td><td></td></tr><tr><td>OK-VQA (Marino et al., 2019)</td><td></td><td></td><td></td></tr><tr><td>ManyModalQA (Hannan et al., 2020)</td><td>√</td><td></td><td></td></tr><tr><td>MultiModalQA (Talmor et al., 2021)</td><td>√</td><td></td><td></td></tr><tr><td>MIMOQA (Singh et al., 2021)</td><td>√</td><td></td><td></td></tr><tr><td>A-OKVQA (Schwenk et al., 2022)</td><td>√</td><td></td><td></td></tr><tr><td>WebQA (Chang et al., 2021)</td><td>√</td><td>√</td><td></td></tr><tr><td>ViQuAE (Lerner et al., 2022)</td><td>√</td><td>√</td><td>√</td></tr><tr><td>Encyclopedia VQA (Mensink et al., 2023)</td><td>√</td><td>√</td><td>√</td></tr><tr><td>SnapNTell (Ours)</td><td>√</td><td>√</td><td>√</td></tr></table>
cuses on cross-modal knowledge extraction but relies on question templates for question generation. ManyModalQA (Hannan et al., 2020) focuses on answer modality choice rather than knowledge aggregation or extraction. In MIMOQA (Singh et al., 2021), the task of extracting a multimodal answer is not necessarily knowledge-intensive. WebQA (Chang et al., 2021) does have categorization but lacks fine-grained entities in many QA pairs, resulting in more general questions and answers. Our proposed SnapNTell differs by including a wide range of fine-grained entities with representative images and explicit entity names in the answer sets. Additionally, it incorporates question-answer pairs that demand knowledge-intensive responses, going beyond simplistic binary answers. Examples of our dataset can be found in Figure 8 in Appendix F.
ViQuAE (Lerner et al., 2022) and Encyclopedic VQA (Mensink et al., 2023) both incorporate entity-level knowledge-based information along with categorization. Therefore, we performed a more in-depth analysis comparing them in Table 1. Our dataset surpasses these in terms of the variety of categories, the number of distinct entities, and the overall number of QA pairs. Additionally, our dataset boasts a higher count of images and a longer average length for answers. Specifically, our dataset is structured to include 10 images for each entity, whereas the exact number of images per entity in ViQuAE and Encyclopedic VQA remains unspecified. Most notably, our dataset's questions are highly anonymous, implying that they do not
![](images/0.jpg)

![](images/1.jpg)

Q: Is the umbrella upside down?
A: No
![](images/2.jpg)

Q: What animal is in the box?
A: Bear
![](images/3.jpg)

Q: Is the photo from the 50's or the 90's?
A: 50's
![](images/4.jpg)

Q: What is the current status of it?
A: The Mendenhall Glacier is currently experiencing a negative glacier mass balance and will likely continue to retreat.
Figure 2: Comparison with existing datasets, where previous VQA datasets mostly focus on freeform answers (such as yes/no for verification questions and choice for selection questions).
reveal any knowledge hints about the entity. This design ensures that the questions cannot be straightforwardly answered without interpreting the image data, setting our dataset apart from both ViQuAE and Encyclopedic VQA.
4 Method
In this section, we will introduce the details of our proposed retrieval-augmented multimodal LLM model. The architecture of our model is shown in Figure 3 (larger figure in Appendix D due to space limit). Our model can be considered twofold: (1) Retrieval augmentation. Given the input image-question pair, we retrieve useful entity-centric information within knowledge sources. (2) Entity-centric knowledge-based answer generation. The retrieved information will be combined with the image and question together to generate a knowledgeable answer.
4.1 Retrieval Augmentation
The retrieval augmentation process can be subdivided into: (i) Semantic region extraction via language-guided object detection, (ii) Entity recognition via image retrieval, and (iii) Knowledge retrieval via multi-source aggregation.
Semantic Region Extraction via Language-Guided Object Detection To improve recognition performance, we focus on extracting specific