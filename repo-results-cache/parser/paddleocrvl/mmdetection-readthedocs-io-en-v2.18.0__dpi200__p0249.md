• "flip": a boolean indicating if image flip transform was used

• "filename": path to the image file

• “ori_shape”: original shape of the image as a tuple (h, w, c)

• "pad shape": image shape after padding

• "img norm cfg": a dict of normalization information:

– mean - per channel mean subtraction

– std - per channel std divisor

– to_rgb - bool indicating if bgr was converted to rgb

## Parameters

• keys (Sequence $$ str $$ ) – Keys of results to be collected in data.

• meta_keys (Sequence[str], optional) – Meta keys to be converted to mmcv.DataContainer and collected in data[img_metas]. Default: ('filename', 'ori_filename', 'ori_shape', 'img_shape', 'pad_shape','scale_factor', 'flip', 'flip_direction', 'img_norm_cfg')

###### class mmdet.datasets.pipelines.ColorTransform(level, prob=0.5)

Apply Color transformation to image. The bboxes, masks, and segmentations are not modified.

## Parameters

• level (int / float) – Should be in range [0, MAX_LEVEL].

• prob (float) – The probability for performing Color transformation.

##### class mmdet.datasets.pipelines.Compose(transforms)

Compose multiple transforms sequentially.

Parameters transforms (Sequence $$ dict $$  / callable $−Sequence of transform object or config dict to be composed.

class mmdet.datasets.pipelines.ContrastTransform(level, prob=0.5)

Apply Contrast transformation to image. The bboxes, masks and segmentations are not modified.

## Parameters

• level (int / float) – Should be in range [0, MAX_LEVEL].

• prob (float) – The probability for performing Contrast transformation.

class mmdet.datasets.pipelines.CutOut(n_holes, cutout_shape=None, cutout_ratio=None, fill_in=(0, 0, 0))

CutOut operation.

Randomly drop some regions of image used in Cutout.

## Parameters

• n_holes (int / tuple[int, int]) – Number of regions to be dropped. If it is given as a list, number of holes will be randomly selected from the closed interval  $ [n_{holes}[0], n_{holes}[1]] $.

• cutout_shape (tuple[int, int] | list[tuple[int, int]]) – The candidate shape of dropped regions. It can be tuple[int, int] to use a fixed cutout shape, or list[tuple[int, int]] to randomly choose shape from the list.