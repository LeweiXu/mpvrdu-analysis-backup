• cutout_ratio(tuple[float, float] | list[tuple[float, float]]) – The candidate ratio of dropped regions. It can be tuple[float, float] to use a fixed ratio or list[tuple[float, float]] to randomly choose ratio from the list. Please note that cutout_shape and cutout_ratio cannot be both given at the same time.

• fill_in(tuple[float, float, float] | tuple[int, int, int])—The value of pixel to fill in the dropped regions. Default:  $ (0, 0, 0) $.

##### class mmdet.datasets.pipelines.DefaultFormatBundle

Default formatting bundle.

It simplifies the pipeline of formatting common fields, including “img”, “proposals”, “gt_bboxes”, “gt_labels”, “gt_masks” and “gt_semantic_seg”. These fields are formatted as follows.

• img: (1) transpose, (2) to tensor, (3) to DataContainer (stack=True)

• proposals: (1) to tensor, (2) to DataContainer

• gt_bboxes: (1) to tensor, (2) to DataContainer

• gt_bboxes_ignore: (1) to tensor, (2) to DataContainer

• gt labels: (1) to tensor, (2) to DataContainer

• gt_masks: (1) to tensor, (2) to DataContainer (cpu_only=True)

• gt_semantic_seg: (1)unsqueeze dim-0 (2)to tensor, (3)to DataContainer (stack=True)

class mmdet.datasets.pipelines.EqualizeTransform(prob=0.5)

Apply Equalize transformation to image. The bboxes, masks and segmentations are not modified.

Parameters prob (float) – The probability for performing Equalize transformation.

class mmdet.datasets.pipelines.Expand(mean=(0, 0, 0), to_rgb=True, ratio_range=(1, 4),

 $$ s e g_{-}i g n o r e\_{l} a b e l{=N o n e,p r o b=0.5)} $$ 

Random expand the image & bboxes.

Randomly place the original image on a canvas of ‘ratio’ x original image size filled with mean values. The ratio is in the range of ratio_range.

## Parameters

• mean (tuple) – mean value of dataset.

• to_rgb (bool) – if need to convert the order of mean to align with RGB.

• ratio_range (tuple) – range of expand ratio.

• prob (float) – probability of applying this transformation

##### class mmdet.datasets.pipelines.ImageToTensor(keys)

Convert image to torch.Tensor by given keys.

The dimension order of input image is (H, W, C). The pipeline will convert it to (C, H, W). If only 2 dimension (H, W) is given, the output would be (1, H, W).

Parameters keys (Sequence[str]) – Key of images to be converted to Tensor.

class mmdet.datasets.pipelines.InstaBoost(action_candidate=('normal', 'horizontal','skip'),

 $$ action\_{p}rob=(1,\;0,\;0),\;scale=(0.8,\;1.2),\;dx=15,\;dy=15, $$ 

 $$ theta=(-1,1),color\_{p}rob=0.5,hflag=False,aug\_{r}atio=0.5) $$ 

Data augmentation method in InstaBoost: Boosting Instance Segmentation Via Probability Map Guided Copy-Pasting.

Refer to https://github.com/GothicAi/Instaboost for implementation details.