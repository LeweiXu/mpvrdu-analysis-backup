#### 30.3.1 MMCV Version

MMDetection v2.12.0 relies on the newest features in MMCV 1.3.3, including BaseModule for unified parameter initialization, model registry, and the CUDA operator MultiScaleDeformableAttn for Deformable DETR. Note that MMCV 1.3.2 already contains all the features used by MMDet but has known issues. Therefore, we recommend users to skip MMCV v1.3.2 and use v1.3.2, though v1.3.2 might work for most of the cases.

#### 30.3.2 Unified model initialization

To unify the parameter initialization in OpenMMLab projects, MMCV supports BaseModule that accepts init_cfg to allow the modules' parameters initialized in a flexible and unified manner. Now the users need to explicitly call model.init_weights() in the training script to initialize the model (as in here, previously this was handled by the detector.The downstream projects must update their model initialization accordingly to use MMDetection v2.12.0. Please refer to PR #4750 for details.

#### 30.3.3 Unified model registry

To easily use backbones implemented in other OpenMMLab projects, MMDetection v2.12.0 inherits the model registry created in MMCV (\#760). In this way, as long as the backbone is supported in an OpenMMLab project and that project also uses the registry in MMCV, users can use that backbone in MMDetection by simply modifying the config without copying the code of that backbone into MMDetection. Please refer to PR \#5059 for more details.

#### 30.3.4 Mask AP evaluation

Before PR 4898 and V2.12.0, the mask AP of small, medium, and large instances is calculated based on the bounding box area rather than the real mask area. This leads to higher APs and APm but lower AP1 but will not affect the overall mask AP. PR 4898 change it to use mask areas by deleting bbox in mask AP calculation. The new calculation does not affect the overall mask AP evaluation and is consistent with Detectron2.

#### 30.4 Compatibility with MMDetection 1.x

MMDetection 2.0 goes through a big refactoring and addresses many legacy issues. It is not compatible with the 1.x version, i.e., running inference with the same model weights in these two versions will produce different results. Thus, MMDetection 2.0 re-benchmarks all the models and provides their links and logs in the model zoo.

The major differences are in four folds: coordinate system, codebase conventions, training hyperparameters, and modular design.

#### 30.4.1 Coordinate System

The new coordinate system is consistent with Detectron2 and treats the center of the most left-top pixel as  $ (0, 0) $ rather than the left-top corner of that pixel. Accordingly, the system interprets the coordinates in COCO bounding box and segmentation annotations as coordinates in range  $ [0, \text{width}] $ or  $ [0, \text{height}] $. This modification affects all the computation related to the bbox and pixel selection, which is more natural and accurate.

• The height and width of a box with corners  $ (x_{1}, y_{1}) $ and  $ (x_{2}, y_{2}) $ in the new coordinate system is computed as width = x_{2} - x_{1} and height = y_{2} - y_{1}. In MMDetection 1.x and previous version, a “+1” was added both height and width. This modification are in three folds:

1. Box transformation and encoding/decoding in regression.