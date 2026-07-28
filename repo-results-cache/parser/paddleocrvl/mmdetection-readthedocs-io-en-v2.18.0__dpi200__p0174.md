## Bug Fixes

• Fix IOU assigners when ignore_iof_thr > 0 and there is no pred boxes. (#2135)

• Fix mAP evaluation when there are no ignored boxes. (#2116)

• Fix the empty RoI input for Deformable RoI Pooling. (#2099)

• Fix the dataset settings for multiple workflows. (#2103)

• Fix the warning related to torch.uint8 in PyTorch 1.4. (#2105)

• Fix the inference demo on devices other than gpu:0. (#2098)

• Fix Dockerfile. (#2097)

• Fix the bug that pad_val is unused in Pad transform. (#2093)

• Fix the albumentation transform when there is no ground truth bbox. (#2032)

## Improvements

• Use torch instead of numpy for random sampling. (#2094)

• Migrate to the new MMDDP implementation in MMCV v0.3. (#2090)

• Add meta information in logs. (#2086)

• Rewrite Soft NMS with pytorch extension and remove cython as a dependency. (#2056)

• Rewrite dataset evaluation. (#2042, #2087, #2114, #2128)

• Use numpy array for masks in transforms. (#2030)

## New Features

• Implement “CARAFE: Content-Aware ReAssembly of FEatures”. (#1583)

• Add worker_init_fn() in data_loader when seed is set. (#2066, #2111)

• Add logging utils. (#2035)

##### 32.22 v1.0.0 (30/1/2020)

This release mainly improves the code quality and adds more docstrings.

## Highlights

• Documentation is online now: https://mmdetection.readthedocs.io.

• Support new models: ATSS.

• DCN is now available with the api build_conv_layer and ConvModule like the normal conv layer.

• A tool to collect environment information is available for trouble shooting.

## Bug Fixes

• Fix the incompatibility of the latest numpy and pycocotools. (#2024)

• Fix the case when distributed package is unavailable, e.g., on Windows. (#1985)

• Fix the dimension issue for refine_bboxes(). (#1962)

• Fix the typo when seg_prefix is a list. (#1906)

• Add segmentation map cropping to RandomCrop. (#1880)