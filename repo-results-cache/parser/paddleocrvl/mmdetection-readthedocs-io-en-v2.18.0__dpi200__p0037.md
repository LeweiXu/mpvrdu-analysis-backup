(continued from previous page)

"file_name": str,
}

annotation = {
    "id": int,
    "image_id": int,
    "category_id": int,
    "segmentation": RLE or [polygon],
    "area": float,
    "bbox": [x, y, width, height],
    "iscrowd": 0 or 1,
}

categories = [
    "id": int,
    "name": str,
    "supercategorical": str,
]

Assume we use the balloon dataset. After downloading the data, we need to implement a function to convert the annotation format into the COCO format. Then we can use implemented COCODataset to load the data and perform training and evaluation.

If you take a look at the dataset, you will find the dataset format is as below:

{'base64_img_data': "",
'file_attributes': {}
'filename': '34020010494_e5cb88e1c4_k.jpg',
'fileref': "",
'regions': {
'0': {
'region_attributes': {}
'shape_attributes': {
'all_points_x': [1020,
1000,
994,
1003,
1023,
1050,
1089,
1134,
1190,
1265,
1321,
1361,
1403,
1428,
1442,
1445,
1441,
1427,
1400,
1361,
1316,
1269,
1228,
}
}

(continues on next page)