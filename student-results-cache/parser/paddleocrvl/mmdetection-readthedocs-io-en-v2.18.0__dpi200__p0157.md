##### 32.8 v2.12.0 (01/5/2021)

#### 32.8.1 Highlights

• Support new methods: AutoAssign, YOLOF, and Deformable DETR

• Stable support of exporting models to ONNX with batched images and dynamic shape ( $ #5039 $)

#### 32.8.2 Backwards Incompatible Changes

MMDetection is going through big refactoring for more general and convenient usages during the releases from v2.12.0 to v2.15.0 (maybe longer). In v2.12.0 MMDetection inevitably brings some BC-breakings, including the MMCV dependency, model initialization, model registry, and mask AP evaluation.

• MMCV version. MMDetection v2.12.0 relies on the newest features in MMCV 1.3.3, including BaseModule for unified parameter initialization, model registry, and the CUDA operator MultiScaleDeformableAttn for Deformable DETR. Note that MMCV 1.3.2 already contains all the features used by MMDet but has known issues. Therefore, we recommend users skip MMCV v1.3.2 and use v1.3.3, though v1.3.2 might work for most cases.

• Unified model initialization (#4750). To unify the parameter initialization in OpenMMLab projects, MMCV supports BaseModule that accepts init_cfg to allow the modules' parameters initialized in a flexible and unified manner. Now the users need to explicitly call model.init_weights() in the training script to initialize the model (as in here, previously this was handled by the detector. The models in MMDetection have been re-benchmarked to ensure accuracy based on PR #4750. The downstream projects should update their code accordingly to use MMDetection v2.12.0.

- Unified model registry (#5059). To easily use backbones implemented in other OpenMMLab projects, MMDetection migrates to inherit the model registry created in MMCV (#760). In this way, as long as the backbone is supported in an OpenMMLab project and that project also uses the registry in MMCV, users can use that backbone in MMDetection by simply modifying the config without copying the code of that backbone into MMDetection.

• Mask AP evaluation (#4898). Previous versions calculate the areas of masks through the bounding boxes when calculating the mask AP of small, medium, and large instances. To indeed use the areas of masks, we pop the key bbox during mask AP calculation. This change does not affect the overall mask AP evaluation and aligns the mask AP of similar models in other projects like Detectron2.

#### 32.8.3 New Features

• Support paper AutoAssign: Differentiable Label Assignment for Dense Object Detection (#4295)

• Support paper You Only Look One-level Feature (#4295)

• Support paper Deformable DETR: Deformable Transformers for End-to-End Object Detection (#4778)

• Support calculating IoU with FP16 tensor in bbox_overlaps to save memory and keep speed (#4889)

• Add __repr__ in custom dataset to count the number of instances (#4756)

• Add windows support by updating requirements.txt (#5052)

• Stable support of exporting models to ONNX with batched images and dynamic shape, including SSD, FSAF, FCOS, YOLOv3, RetinaNet, Faster R-CNN, and Mask R-CNN (#5039)