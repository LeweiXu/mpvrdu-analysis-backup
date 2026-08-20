Parameters policies (list[list[dict]]) – The policies of auto augmentation. Each policy in policies is a specific augmentation policy, and is composed by several augmentations (dict). When AutoAugment is called, a random policy in policies will be selected to augment images.

## Examples

>>> replace = (104, 116, 124)
>>> policies = [
>>> [
>>> dict(type='Sharpness', prob=0.0, level=8),
>>> dict(
>>> type='Shear',
>>> prob=0.4,
>>> level=0,
>>> replace=replace,
>>> axis='x')
>>> ],
>>> [
>>> dict(
>>> type='Rotate',
>>> prob=0.6,
>>> level=10,
>>> replace=replace),
>>> dict(type='Color', prob=1.0, level=6)
>>> ]
>>> augmentation = AutoAugment(policies)
>>> img = np.ones(100, 100, 3)
>>> gt_bboxes = np.ones(10, 4)
>>> results = dict(img=img, gt_bboxes=gt_bboxes)
>>> results = augmentation(results)

class mmdet.datasets.pipelines.BrightnessTransform(level, prob=0.5)

Apply Brightness transformation to image. The bboxes, masks and segmentations are not modified.

## Parameters

• level (int / float) – Should be in range [0, MAX_LEVEL].

• prob (float) – The probability for performing Brightness transformation.

class mmdet.datasets.pipelines.Collect(keys, meta_keys=('filename', 'ori_filename', 'ori_shape',

Collect data from the loader relevant to the specific task.

This is usually the last stage of the data loader pipeline. Typically keys is set to some subset of “img”, “proposals”, “gt_bboxes”, “gt_bboxes_ignore”, “gt_labels”, and/or “gt_masks”.

The “img_meta” item is always populated. The contents of the “img_meta” dictionary depend on “meta_keys”. By default this includes:

• “img_shape”: shape of the image input to the network as a tuple  $ (h, w, c) $. Note that images may be zero padded on the bottom/right if the batch tensor is larger than this shape.

• "scale factor": a float indicating the preprocessing scale