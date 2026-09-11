where the (misc) includes DCN and GCBlock, etc. More details are illustrated in the documentation for config

• MMDetection V2.0 uses new ResNet Caffe backbones to reduce warnings when loading pre-trained models. Most of the new backbones’ weights are the same as the former ones but do not have conv.bias, except that they use a different img_norm_cfg. Thus, the new backbone will not cause warning of unexpected keys.

#### 30.4.3 Training Hyperparameters

The change in training hyperparameters does not affect model-level compatibility but slightly improves the performance. The major ones are:

• The number of proposals after nms is changed from 2000 to 1000 by setting nms_post=1000 and max_num=1000. This slightly improves both mask AP and bbox AP by  $ \sim0.2\% $ absolute.

• The default box regression losses for Mask R-CNN, Faster R-CNN and RetinaNet are changed from smooth L1 Loss to L1 loss. This leads to an overall improvement in box AP ( $ \sim $0.6% absolute). However, using L1-loss for other methods such as Cascade R-CNN and HTC does not improve the performance, so we keep the original settings for these methods.

• The sample num of RoIAlign layer is set to be 0 for simplicity. This leads to slightly improvement on mask AP ( $ \sim0.2\% $ absolute).

• The default setting does not use gradient clipping anymore during training for faster training speed. This does not degrade performance of the most of models. For some models such as RepPoints we keep using gradient clipping to stabilize the training process and to obtain better performance.

• The default warmup ratio is changed from 1/3 to 0.001 for a more smooth warming up process since the gradient clipping is usually not used. The effect is found negligible during our re-benchmarking, though.

###### 30.4.4 Upgrade Models from 1.x to 2.0

To convert the models trained by MMDetection V1.x to MMDetection V2.0, the users can use the script tools/model_converters/upgrade_model_version.py to convert their models. The converted models can be run in MMDetection V2.0 with slightly dropped performance (less than 1% AP absolute). Details can be found in config/legacy.

### 30.5 pycocotools compatibility

mmpycocotools is the OpenMMlab's folk of official pycocotools, which works for both MMDetection and Detectron2. Before PR 4939, since pycocotools and mmpycocotool have the same package name, if users already installed pyccocotools (installed Detectron2 first under the same environment), then the setup of MMDetection will skip installing mmpycocotool. Thus MMDetection fails due to the missing mmpycocotools. If MMDetection is installed before Detectron2, they could work under the same environment. PR 4939 deprecates mmpycocotools in favor of official pycocotools. Users may install MMDetection and Detectron2 under the same environment after PR 4939, no matter what the installation order is.