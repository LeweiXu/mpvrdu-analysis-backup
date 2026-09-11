## Evaluation config

The config of evaluation will be used to initialize the EvalHook. Except the key interval, other arguments such as metric will be passed to the dataset.evaluate()

evaluation = dict(interval=1, metric='bbox')