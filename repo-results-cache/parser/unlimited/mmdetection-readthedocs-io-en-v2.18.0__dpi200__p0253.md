MMDetection, Release 2.18.0
class mndet.datasets.pipelines.MidUp(img_scale=(640,640),ratio_range=(0.5,1.5),flip_ratio=0.5,
pad_val=114, max_iters=15, min_bbox_size=-5,
min_area_ratio=0.2, max_aspect_ratio=20)
MixUp data augmentation.
Parameters
- img_scale (Sequence[int]) – Image output size after mixup pipeline. Default: (640, 640).
- ratio_range (Sequence[float]) – Scale ratio of mixup image. Default: (0.5, 1.5).
- flip_ratio (float) – Horizontal flip ratio of mixup image. Default: 0.5.
- pad_val (int) - Pad value. Default: 114.
- max_iters(int) – The maximum number of iterations. If the number of iterations is greater than max_iters, but gt_bbox is still empty, then the iteration is terminated. Default: 15.
- min_bbox_size (float) – Width and height threshold to filter bboxes. If the height or width of a box is smaller than this value, it will be removed. Default: 5.
- min_area_ratio (float) – Threshold of area ratio between original bboxes and wrapped bboxes. If smaller than this value, the box will be removed. Default: 0.2.
- max_aspect_ratio (float) – Aspect ratio of width and height threshold to filter bboxes. If max(h/w, w/h) larger than this value, the box will be removed. Default: 20.
get_indexes(data*)
Call function to collect indexes.
Parameters dataset (MultiImageMidataset) – The dataset.
Returns indexes.
Return type list
class mmed_datasets.pipelines.Mosaic(msg_scale=(640, 640), center_ratio_range=(0.5, 1.5),
min_bbox_size=0, pad_val=1/4)
Mosaic augmentation.
Given 4 images, mosaic transform combines them into one output image. The output image is composed of the parts from each sub-image.
![](images/0.jpg)

246
Chapter 38. mmdet.datasets