• scale_ranges (list[tuple], optional) – Scale ranges for evaluating mAP. If not specified, all bounding boxes would be included in evaluation. Default: None.

Returns AP/recall metrics.

Return type dict[str, float]

class mmdet.datasets.WIDERFaceDataset(**kwargs)

Reader for the WIDER Face dataset in PASCAL VOC format.

Conversion scripts can be found in https://github.com/sovrasov/wider-face-pascal-voc-annotations

load_annotations(ann_file)

Load annotation from WIDERFace XML style annotation file.

Parameters ann_file(str) – Path of XML file.

Returns Annotation info from XML file.

Return type list[dict]

class mmdet.datasets.XMLDataset(min_size=None, img_subdir='JPEGImages', ann_subdir='Annotations', **kwargs)

XML dataset for detection.

## Parameters

• min_size(int | float, optional) – The minimum size of bounding boxes in the images. If the size of a bounding box is less than min_size, it would be add to ignored field.

• img_subdir(str) – Subdir where images are stored. Default: JPEGImages.

• ann_subdir(str) – Subdir where annotations are. Default: Annotations.

## get_ann_info(idx)

Get annotation from XML file by index.

Parameters idx (int) – Index of data.

Returns Annotation info of specified index.

Return type dict

get_cat_ids(idx)

Get category ids in XML file by index.

Parameters idx (int) – Index of data.

Returns All categories in the image of specified index.

Return type list[int]

## load_annotations(ann_file)

Load annotation from XML style ann file.

Parameters ann_file(str) – Path of XML file.

Returns Annotation info from XML file.

Return type list[dict]

mmdet.datasets.build_dataloader(dataset, samples_per_gpu, workers_per_gpu, num_gpus=1, dist=True, shuffle=True, seed=None, runner_type='EpochBasedRunner', **kwargs)

Build PyTorch DataLoader.

In distributed training, each GPU/process has a dataloader. In non-distributed training, there is only one dataloader for all GPUs.