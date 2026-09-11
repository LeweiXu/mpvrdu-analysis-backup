class mmdet.datasets.ConcatDataset(datasets, separate_eval=True)

A wrapper of concatenated dataset.

Same as torch.utils.data.dataset.ConcatDataset, but concat the group flag for image aspect ratio.

## Parameters

• datasets (list[Dataset]) – A list of datasets.

- separate_eval (bool) – Whether to evaluate the results separately if it is used as validation dataset. Defaults to True.

evaluate(results, logger=None, **kwargs)

Evaluate the results.

## Parameters

• results (list[list / tuple]) – Testing results of the dataset.

- logger (logging.Logger | str | None) – Logger used for printing related information during evaluation. Default: None.

Returns float]: AP results of the total dataset or each separate dataset if self.separate_eval=True.

Return type dict[str]

## get_cat_ids(idx)

Get category ids of concatenated dataset by index.

Parameters idx (int) – Index of data.

Returns All categories in the image of specified index.

Return type list[int]

class mmdet.datasets.CustomDataset(ann_file, pipeline, classes=None, data_root=None, img_prefix='', seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

Custom dataset for detection.

The annotation format is shown as follows. The  $ ann $ field is optional for testing.

{
    'filename': 'a.jpg',
    'width': 1280,
    'height': 720,
    'ann': {
        'bboxes': <np.ndarray>(n, 4) in (x1, y1, x2, y2) order.
        'labels': <np.ndarray>(n, ),
        'bboxes_ignore': <np.ndarray>(k, 4), (optional field)
        'labels_ignore': <np.ndarray>(k, 4) (optional field)
    },
   ...
]

## Parameters

• ann file (str) – Annotation file path.

• pipeline (list[dict]) – Processing pipeline.