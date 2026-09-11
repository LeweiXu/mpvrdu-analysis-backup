class mmdet.datasets.pipelines.MixUp(img_scale=(640, 640), ratio_range=(0.5, 1.5), flip_ratio=0.5, pad_val=114, max_iters=15, min_bbox_size=5, min_area_ratio=0.2, max_aspect_ratio=20)

MixUp data augmentation.

## Parameters

• img_scale (Sequence[int]) – Image output size after mixup pipeline. Default: (640, 640).

• ratio_range (Sequence $$ float $$ ) – Scale ratio of mixup image. Default: (0.5, 1.5).

• flip_ratio (float) – Horizontal flip ratio of mixup image. Default: 0.5.

• pad_val (int) – Pad value. Default: 114.

• max_iters(int) – The maximum number of iterations. If the number of iterations is greater than max_iters, but gt_bbox is still empty, then the iteration is terminated. Default: 15.

• min_bbox_size (float) – Width and height threshold to filter bboxes. If the height or width of a box is smaller than this value, it will be removed. Default: 5.

• min_area_ratio (float) – Threshold of area ratio between original bboxes and wrapped bboxes. If smaller than this value, the box will be removed. Default: 0.2.

• max_aspect_ratio (float) – Aspect ratio of width and height threshold to filter bboxes. If max(h/w, w/h) larger than this value, the box will be removed. Default: 20.

## get_indexes(dataset)

Call function to collect indexes.

Parameters dataset (MultiImageMixDataset) – The dataset.

Returns indexes.

Return type list

class mmdet.datasets.pipelines.Mosaic(img_scale=(640, 640), center_ratio_range=(0.5, 1.5),

 $$ min\_{b}box\_{s}ize{=}0,pad\_{v}al{=}114) $$ 

Mosaic augmentation.

Given 4 images, mosaic transform combines them into one output image. The output image is composed of the parts from each sub-image.

<div style="text-align: center;"><img src="imgs/img_in_image_box_421_1401_897_1939.jpg" alt="Image" width="28%" /></div>


(continues on next page)