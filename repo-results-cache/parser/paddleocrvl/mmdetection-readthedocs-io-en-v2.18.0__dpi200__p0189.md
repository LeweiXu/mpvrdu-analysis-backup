mmdet.apis.multi_gpu_test(model, data_loader, tmpdir=None, gpu_collect=False)

## Test model with multiple gpus

This method tests model with multiple gpus and collects the results under two different modes: gpu and cpu modes. By setting 'gpu_collect=True' it encodes results to gpu tensors and use gpu communication for results collection. On cpu mode it saves the results on different gpus to 'tmpdir' and collects them by the rank 0 worker.

## Parameters

• model (nn.Module) – Model to be tested.

• data_loader (nn.Dataloader) – Pytorch data loader.

- tmpdir (str) – Path of directory to save the temporary results from different gpus under cpu mode.

• gpu_collect (bool) – Option to use either gpu or cpu to collect results.

Returns The prediction results.

Return type list

mmdet.apis.set_random_seed(seed, deterministic=False)

Set random seed.

## Parameters

• seed (int) – Seed to be used.

• deterministic (bool) – Whether to set the deterministic option for CUDNN backend, i.e., set torch.backends.cudnn.deterministic to True and torch.backends.cudnn.benchmark to False. Default: False.

mmdet.apis.show_result_pyplot(model, img, result, score_thr=0.3, title='result', wait_time=0)

Visualize the detection results on the image.

## Parameters

• model (nn.Module) – The loaded detector.

• img (str or np.ndarray) – Image filename or loaded image.

• result (tuple[list] or list) – The detection result, can be either (bbox, segm) or just bbox.

• score_thr (float) – The threshold to visualize the bboxes and masks.

• title(str) – Title of the pyplot figure.

• wait_time (float) – Value of waitKey param. Default: 0.