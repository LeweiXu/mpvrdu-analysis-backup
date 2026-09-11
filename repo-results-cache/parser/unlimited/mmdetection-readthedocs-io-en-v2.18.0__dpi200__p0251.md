MMDetection, Release 2.18.0
Parameters
- action_candidate (tuple) – Action candidates. “normal”, “horizontal”, “vertical”, “skip” are supported. Default: (‘normal’, ‘horizontal’, ‘skip’).
- action_prob (tuple) – Corresponding action probabilities. Should be the same length as action_candidate. Default: (1, 0, 0).
- scale (tuple) – (min scale, max scale). Default: (0.8, 1.2).
- dx (int) – The maximum x-axis shift will be (instance width) / dx. Default 15.
- dy (int) – The maximum y-axis shift will be (instance height) / dy. Default 15.
- theta (tuple) – (min rotation degree, max rotation degree). Default: (-1, 1).
- color_prob(float) – Probability of images for color augmentation. Default 0.5.
- heatmap_flag (bool) – Whether to use heatmap guided. Default False.
- aug_ratio(float) – Probability of applying this transformation. Default 0.5.
class mmdet.datasets.pipelines.LoadAnnotations(with_bbox=True, with_label=True, with_mask=False,
with_seg=False, poly2mask=True,
file_client_args={'backend': 'disk'}
Load multiple types of annotations.
Parameters
- with_bbox(bool) – Whether to parse and load the bbox annotation. Default: True.
- with_label(bool) – Whether to parse and load the label annotation. Default: True.
- with_mask(bool) – Whether to parse and load the mask annotation. Default: False.
- with_seg (bool) – Whether to parse and load the semantic segmentation annotation. Default: False.
- poly2mask (bool) – Whether to convert the instance masks from polygons to bitmaps. Default: True.
- file_client_args (dict) – Arguments to instantiate a FileClient. See mmcv.fileio.FileClient for details. Defaults to dict(backend='disk').
process_polygons(polygons)
Convert polygons to list of ndarray and filter invalid polygons.
Parameters polygons (list[list]) – Polygons of one instance.
Returns Processed polygons.
Return type list[numpy.ndarray]
class mmdet.datasets.pipelines.LoadImageFromFile(to_float32=False, color_type='color', file_client_args=['backend': 'disk'])
Load an image from file.
Required keys are “img_prefix” and “img_info” (a dict that must contain the key “filename”). Added or updated keys are “filename”, “img”, “img_shape”, “ori_shape” (same as img_shape), “pad_shape” (same as img_shape), “scale_factor” (1.0) and “img_norm_cfg” (means=0 and stds=1).
Parameters
- to_float32 (bool) – Whether to convert the loaded image to a float32 numpy array. If set to False, the loaded image is an uint8 array. Defaults to False.
- color_type(str) – The flag argument for mmcv.imfrombytes(). Defaults to 'color'.
244
Chapter 38. mmdet.datasets