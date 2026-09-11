### MMDET.APIS

#### async mmdet.apis.async_inference_detector(model, imgs)

Async inference image(s) with the detector.

## Parameters

• model (nn.Module) – The loaded detector.

• img (str / ndarray) – Either image files or loaded images.

Returns Awaitable detection results.

mmdet.apis.get_root_logger(log_file=None, log_level=20)

Get root logger.

Parameters

• log_file (str, optional) – File path of log. Defaults to None.

• log_level (int, optional) – The level of logger. Defaults to logging.INFO.

Returns The obtained logger

Return type logging.Logger

mmdet.apis.inference_detector(model, imgs)

Inference image(s) with the detector.

## Parameters

• model (nn.Module) – The loaded detector.

• imgs(str/ndarray or list[str/ndarray] or tuple[str/ndarray]) – Either image files or loaded images.

Returns If images is a list or tuple, the same length list type results will be returned, otherwise return the detection results directly.

mmdet.apis.init_detector(config, checkpoint=None, device='cuda:0', cfg_options=None)

Initialize a detector from config file.

## Parameters

• config (str or mmcv.Config) – Config file path or the config object.

- checkpoint (str, optional) – Checkpoint path. If left as None, the model will not load any weights.

• cfg_options (dict) – Options to override some settings in the used config.

Returns The constructed detector.

Return type nn.Module