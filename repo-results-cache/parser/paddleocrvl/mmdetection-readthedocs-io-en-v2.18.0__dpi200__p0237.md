load_annotations(ann_file)

Load annotation from COCO style annotation file.

Parameters ann_file(str) – Path of annotation file.

Returns Annotation info from COCO api.

Return type list[dict]

## results2json(results, outfile_prefix)

Dump the detection results to a COCO style json file.

There are 3 types of results: proposals, bbox predictions, mask predictions, and they have different data types. This method will automatically recognize the type, and dump them to json files.

## Parameters

• results (list[list / tuple / ndarray]) – Testing results of the dataset.

• outfile_prefix (str) – The filename prefix of the json files. If the prefix is “somepath/xxx”, the json files will be named “somepath/xxx.bbox.json”, “somepath/xxx.segm.json”, “somepath/xxx.proposal.json”.

Returns str]: Possible keys are “bbox”, “segm”, “proposal”, and values are corresponding file-names.

Return type dict[str

## xyxy2xywh(bbox)

Convert xyxy style bounding boxes to xywh style for COCO evaluation.

Parameters bbox (numpy.ndarray) – The bounding boxes, shape (4, ), in xyy order.

Returns The converted bounding boxes, in xywh order.

Return type list[float]

class mmdet.datasets.CocoPanopticDataset(ann_file, pipeline, classes=None, data_root=None, img_prefix='', seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

Coco dataset for Panoptic segmentation.

The annotation format is shown as follows. The  $ ann $ field is optional for testing.

{
    'filename': f'_{image_id:012}.png',
    'image_id': 9
   'segments_info': {
        [
            {
                'id': 8345037, (segment_id in panoptic png,
                                   convert from rgb)
                                   'category_id': 51,
                                   'iscrowd': 0,
                                   'bbox': (x1, y1, w, h),
                                   'area': 24315,
                                  'segmentation': list, (coded mask)
            }
        ]
    }
}

(continues on next page)