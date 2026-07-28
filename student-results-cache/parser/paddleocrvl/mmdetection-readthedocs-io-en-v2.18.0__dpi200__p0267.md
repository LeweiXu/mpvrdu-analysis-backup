forward_train(imgs, img_metas, **kwargs)

## Parameters

• img (list[Tensor]) – List of tensors of shape (1, C, H, W). Typically these should be mean centered and std scaled.

• img_metas (list[dict]) – List of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys, see mmdet.datasets.pipelines.Collect.

• kwargs (keyword arguments) – Specific to concrete implementation.

show_result(img, result, score_thr=0.3, bbox_color=(72, 101, 241), text_color=(72, 101, 241),

mask_color=None, thickness=2, font_size=13, win_name="", show=False, wait_time=0, out_file=None)

Draw result over img.

## Parameters

• img (str or Tensor) – The image to be displayed.

• result (Tensor or tuple) – The results to draw over img bbox_result or (bbox_result, segm_result).

• score_thr (float, optional) – Minimum score of bboxes to be shown. Default: 0.3.

• bbox_color (str or tuple(int) or Color) – Color of bbox lines. The tuple of color should be in BGR order. Default: ‘green’

• text_color (str or tuple(int) or Color) – Color of texts. The tuple of color should be in BGR order. Default: ‘green’

• mask_color (None or str or tuple(int) or Color) – Color of masks. The tuple of color should be in BGR order. Default: None

• thickness (int) – Thickness of lines. Default: 2

• font_size(int) – Font size of texts. Default: 13

• win_name (str) – The window name. Default: "

• wait_time (float) – Value of waitKey param. Default: 0.

• show (bool) – Whether to show the image. Default: False.

• out_file (str or None) – The filename to write the image. Default: None.

Returns Only if not show or out file

Return type img (Tensor)

## train_step(data, optimizer)

The iteration step during training.

This method defines an iteration step during training, except for the back propagation and optimizer updating, which are done in an optimizer hook. Note that in some complicated cases or models, the whole process including back propagation and optimizer updating is also defined in this method, such as GAN.

## Parameters

• data (dict) – The output of dataloader.