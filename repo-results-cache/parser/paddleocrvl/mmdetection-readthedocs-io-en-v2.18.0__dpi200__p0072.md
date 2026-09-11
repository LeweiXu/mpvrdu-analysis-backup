(continued from previous page)

'id':8345037, # One-to-one correspondence with the id in the annotation
map.
'category_id': 51,
'iscrowd': 0,
'bbox': (x1, y1, w, h), # The bbox of the background is the outer_
'rectangle of its mask.
'area': 24315
},
...
],
...
]
'categories': [ # including both foreground categories and background categories
{'id': 0, 'name': 'person'},
...
]

Moreover, the seg_prefix must be set to the path of the panoptic annotation images.

data = dict(
    type='CocoPanopticDataset',
    train=dict(
        seg_prefix = 'path/to/your/train/panoptic/image_annotation_data'
    ),
    val=dict(
        seg_prefix = 'path/to/your/train/panoptic/image_annotation_data'
    )
)