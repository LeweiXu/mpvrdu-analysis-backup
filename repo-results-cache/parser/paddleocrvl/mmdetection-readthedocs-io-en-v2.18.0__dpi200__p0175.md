• Fix the return value of ga_shape_target_single(). (#1853)

• Fix the loaded shape of empty proposals. (#1819)

• Fix the mask data type when using albumentation. (#1818)

## Improvements

• Enhance AssignResult and SamplingResult. (#1995)

• Add ability to overwrite existing module in Registry. (#1982)

• Reorganize requirements and make albumentations and imagecorruptions optional. (#1969)

• Check NaN in SSDHead. (#1935)

• Encapsulate the DCN in ResNe(X)t into a ConvModule & Conv_layers. (#1894)

• Refactoring for mAP evaluation and support multiprocessing and logging. (#1889)

• Init the root logger before constructing Runner to log more information. (#1865)

• Split SegResizeFlipPadRescale into different existing transforms. (#1852)

• Move init_dist() to MMCV. (#1851)

• Documentation and docstring improvements. (#1971, #1938, #1869, #1838)

• Fix the color of the same class for mask visualization. (#1834)

• Remove the option keep_all_stages in HTC and Cascade R-CNN. (#1806)

## New Features

• Add two test-time options crop_mask and rle_mask_encode for mask heads. (#2013)

• Support loading grayscale images as single channel. (#1975)

• Implement “Bridging the Gap Between Anchor-based and Anchor-free Detection via Adaptive Training Sample Selection”. (#1872)

• Add sphinx generated docs. (#1859, #1864)

• Add GN support for flops computation. (#1850)

• Collect env info for trouble shooting. (#1812)

#### 32.23 v1.0rc1 (13/12/2019)

The RC1 release mainly focuses on improving the user experience, and fixing bugs.

## Highlights

• Support new models: FoveaBox, RepPoints and FreeAnchor.

• Add a Dockerfile.

• Add a jupyter notebook demo and a webcam demo.

• Setup the code style and CI.

• Add lots of docstrings and unit tests.

• Fix lots of bugs.

Breaking Changes