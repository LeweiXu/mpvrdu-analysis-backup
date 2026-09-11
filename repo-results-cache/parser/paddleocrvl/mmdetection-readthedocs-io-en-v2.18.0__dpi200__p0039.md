(continued from previous page)

'size': 1115004}

The annotation is a JSON file where each key indicates an image’s all annotations. The code to convert the balloon dataset into coco format is as below.

import os.path as osp

def convert_balloon_to_coco(ann_file, out_file, image_prefix):
    data_Infos = mmcv.load(ann_file)

    annotations = []
    images = []
    obj_count = 0

    for idx, v in enumerate(mmcv.track_iter_progress(data_Infos.values)):
        filename = v['filename']
        img_path = osp.join(image_prefix, filename)
        height, width = mmcv.imread(img_path).shape[:2]

        images.append(dict(
            id=idx,
            file_name=filename,
            height=height,
            width=width))

    bboxes = []
    labels = []
    masks = []

    for_, obj in v['regions'].items():
        assert not obj['region_attributes']
        obj = obj['shape_attributes']
        px = obj['all_points_x']
        py = obj['all_points_y']
        poly = [(x + 0.5, y + 0.5) for x, y in zip(px, py)]
        poly = [p for x in poly for p in x]

        x_min, y_min, x_max, y_max = (
            min(px), min(py), max(px), max(py)
        )

        data_anno = dict(
            image_id=idx,
            id=obj_count,
            category_id=0,
            bbox=[x_min, y_min, x_max - x_min, y_max - y_min],
            area=(x_max - x_min) * (y_max - y_min),
            segmentation=[poly],
            iscrowd=0)
            annotations.append(data_anno)
            obj_count += 1

coco_format_json = dict(
    images=images,
    image_path=image_path
)

(continues on next page)