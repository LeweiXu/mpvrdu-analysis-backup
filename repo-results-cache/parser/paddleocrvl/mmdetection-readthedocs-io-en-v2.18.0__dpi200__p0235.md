• results (list) – Testing results of the dataset.

- txtfile_prefix (str / None) – The prefix of txt files. It includes the file path and the prefix of filename, e.g., “a/b/prefix”. If not specified, a temp file will be created. Default: None.

Returns (result_files, tmp_dir), result_files is a dict containing the json filepaths, tmp_dir is the temporal directory created for saving txt/png files when txtfile_prefix is not specified.

Return type tuple

results2txt(results, outfile_prefix)

Dump the detection results to a txt file.

## Parameters

• results (list[list / tuple]) – Testing results of the dataset.

• outfile_prefix (str) – The filename prefix of the json files. If the prefix is “somepath/xxx”, the txt files will be named “somepath/xxx.txt”.

Returns Result txt files which contains corresponding instance segmentation images.

Return type list[str]

#### class mmdet.datasets.ClassBalancedDataset(dataset, oversample_thr, filter_empty_gt=True)

A wrapper of repeated dataset with repeat factor.

Suitable for training on class imbalanced datasets like LVIS. Following the sampling strategy in the paper, in each epoch, an image may appear multiple times based on its “repeat factor”. The repeat factor for an image is a function of the frequency the rarest category labeled in that image. The “frequency of category c” in  $ [0, 1] $ is defined by the fraction of images in the training set (without repeats) in which category c appears. The dataset needs to instantiate self.get_cat_ids() to support ClassBalancedDataset.

The repeat factor is computed as followed.

1. For each category c, compute the fraction # of images that contain it:  $ f(c) $

2. For each category c, compute the category-level repeat factor:  $  r(c) = \max(1, \sqrt{qrt(t/f(c))})  $

3. For each image I, compute the image-level repeat factor:  $  r(I) = \max_{c \in I} r(c)  $

## Parameters

• dataset (CustomDataset) – The dataset to be repeated.

• oversample_thr (float) – frequency threshold below which data is repeated. For categories with  $ f_{c} \geq $ oversample_thr, there is no oversampling. For categories with  $ f_{c} < $ oversample_thr, the degree of oversampling following the square-root inverse frequency heuristic above.

• filter_empty_gt (bool, optional) – If set true, images without bounding boxes will not be oversampled. Otherwise, they will be categorized as the pure background class and involved into the oversampling. Default: True.

class mmdet.datasets.CocoDataset(ann_file, pipeline, classes=None, data_root=None, img_prefix="", seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

evaluate(results, metric='bbox', logger=None, jsonfile_prefix=None, classwise=False, proposal_nums=(100, 300, 1000), iou_thrs=None, metric_items=None)

Evaluation in COCO protocol.