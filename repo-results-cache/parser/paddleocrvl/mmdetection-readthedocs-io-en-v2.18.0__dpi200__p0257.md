(continued from previous page)

There are 5 main areas in the figure:

• output image: output image of this operation, also called padding image in following instruction.

• original image: input image of this operation.

• padded area: non-intersect area of output image and original image.

• cropped area: the overlap of output image and original image.

• center range: a smaller area where random center chosen from. center range is computed by border and original image’s shape to avoid our random center is too close to original image’s border.

Also this operation act differently in train and test mode, the summary pipeline is listed below.

## Train pipeline:

1. Choose a random_ratio from ratios, the shape of padding image will be random_ratio * crop_size.

2. Choose a random_center in center range.

3. Generate padding image with center matches the random\_center.

4. Initialize the padding image with pixel value equals to mean.

5. Copy the cropped area to padding image.

6. Refine annotations.

## Test pipeline:

1. Compute output shape according to test_pad_mode.

2. Generate padding image with center matches the original image center.

3. Initialize the padding image with pixel value equals to mean.

4. Copy the cropped area to padding image.

## Parameters

• crop_size (tuple / None) – expected size after crop, final size will be computed according to ratio. Requires (h, w) in train mode, and None in test mode.

• ratios (tuple) – random select a ratio from tuple and crop image to (crop_size[0] * ratio) * (crop_size[1] * ratio). Only available in train mode.

• border (int) – max distance from center select area to image border. Only available in train mode.

• mean (sequence) – Mean values of 3 channels.