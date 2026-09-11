MMDetection, Release 2.18.0
- file_client_args (dict) – Arguments to instantiate a FileClient. See mmcv.fileio.FileClient for details. Defaults to dict(backend='disk').
class mmdet.datasets.pipelines.LoadImageFromWebcam(to_float32=False, color_type='color',
file_client_args={'backend': 'disk'}
Load an image from webcam.
Similar with LoadImageFromFile, but the image read from webcam is in results['img'].
class mmdet.datasets.pipelines.LoadMultiChannelImageFromFiles(to_float32=False,
color_type='unchanged',
file_client_args={'backend':
'disk'])
Load multi-channel images from a list of separate channel files.
Required keys are “img_prefix” and “img_info” (a dict that must contain the key “filename”, which is expected to be a list of filenames). Added or updated keys are “filename”, “img”, “img_shape”, “ori_shape” (same as img_shape), “pad_shape” (same as img_shape), “scale_factor” (1.0) and “img_norm_cfg” (means=0 and stds=1).
Parameters
- to_float32 (bool) – Whether to convert the loaded image to a float32 numpy array. If set to False, the loaded image is an uint8 array. Defaults to False.
- color_type(str) – The flag argument for mmcv.imfrombytes(). Defaults to 'color'.
- file_client_args (dict) – Arguments to instantiate a FileClient. See mmcv.fileio.FileClient for details. Defaults to dict(backend='disk').
class mmdet.datasets.pipelines.LoadProposals(num_max_proposals=None)
Load proposal pipeline.
Required key is “proposals”. Updated keys are “proposals”, “bbox_fields”.
Parameters num_max_proposals(int, optional) - Maximum number of proposals to load. If not specified, all proposals will be loaded.
class mmdet.datasets.pipelines.MinIoURandomCrop(min_ious=(0.1, 0.3, 0.5, 0.7, 0.9), min_crop_size=0.3, bbox_clip_border=True)
Random crop the image & bboxes, the cropped patches have minimum IoU requirement with original image & bboxes, the IoU threshold is randomly selected from min_ious.
Parameters
- min_ious (tuple) – minimum IoU threshold for all intersections with
- boxes (bounding) -
- min_crop_size (float) - minimum crop's size (i.e. h, w := a*h, a*w,
- a >= min_crop_size) (where) -
- bbox_clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.
Note: The keys for bboxes, labels and masks should be paired. That is, gt_bboxes corresponds to gt_labels and gt_masks, and gt_bboxes_ignore to gt_labels_ignore and gt_masks_ignore.
38.2. pipelines
245