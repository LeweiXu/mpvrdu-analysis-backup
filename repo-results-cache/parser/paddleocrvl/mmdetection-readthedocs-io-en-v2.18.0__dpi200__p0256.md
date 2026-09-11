## Parameters

• brightness delta (int) – delta of brightness.

• contrast_range (tuple) – range of contrast.

• saturation_range (tuple) – range of saturation.

• hue delta (int) – delta of hue.

class mmdet.datasets.pipelines.RandomAffine(max_rotate_degree=10.0, max_translate_ratio=0.1,

(max_rotate_degree=10.0, max_translate_ratio=0.1, scaling_ratio_range=(0.5, 1.5), max_shear_degree=2.0, border=(0, 0), border_val=(114, 114, 114), min_bbox_size=2, min_area_ratio=0.2, max_aspect_ratio=20)

Random affine transform data augmentation.

This operation randomly generates affine transform matrix which including rotation, translation, shear and scaling transforms.

## Parameters

• max_rotate_degree (float) – Maximum degrees of rotation transform. Default: 10.

• max_translate_ratio(float) – Maximum ratio of translation. Default: 0.1.

• scaling_ratio_range (tuple[float]) – Min and max ratio of scaling transform. Default: (0.5, 1.5).

• max_shear_degree (float) – Maximum degrees of shear transform. Default: 2.

• border (tuple[int]) – Distance from height and width sides of input image to adjust output shape. Only used in mosaic dataset. Default:  $ (0, 0) $.

• border_val (tuple[int]) – Border padding values of 3 channels. Default: (114, 114, 114).

• min_bbox_size (float) – Width and height threshold to filter bboxes. If the height or width of a box is smaller than this value, it will be removed. Default: 2.

• min_area_ratio (float) – Threshold of area ratio between original bboxes and wrapped bboxes. If smaller than this value, the box will be removed. Default: 0.2.

• max_aspect_ratio (float) – Aspect ratio of width and height threshold to filter bboxes. If max(h/w, w/h) larger than this value, the box will be removed.

class mmdet.datasets.pipelines.RandomCenterCropPad(crop_size=None, ratios=(0.9, 1.0, 1.1),

 $$ border=128,mean=None,std=None, $$ 

 $$ to\_{r}gb=None,test\_{m}ode=False, $$ 

 $$ t e s t\_{p} a d\_{m} o d e=(^{\prime}l o g i c a l\_{o} r^{\prime},127), $$ 

 $$ test\_{p}ad\_{a}dd\_{p}ix{=}0,\\ bbox\_{c}lip\_{b}order{=}True) $$ 

Random center crop and random around padding for CornerNet.

This operation generates randomly cropped image from the original image and pads it simultaneously. Different from RandomCrop, the output shape may not equal to crop_size strictly. We choose a random value from ratios and the output shape could be larger or smaller than crop_size. The padding operation is also different from Pad, here we use around padding instead of right-bottom padding.

The relation between output image (padding image) and original image:

output image

(continues on next page)