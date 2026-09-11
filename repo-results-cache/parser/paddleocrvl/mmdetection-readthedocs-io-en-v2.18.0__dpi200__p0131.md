### 24.4 Detectron ResNet to Pytorch

tools/model_converters/detectron2pytorch.py converts keys in the original detection pretrained ResNet models to PyTorch style.

python tools/model_converters/detectron2pytorch.py ${SRC} ${DST} ${DEPTH} [-h]

### 24.5 Prepare a model for publishing

tools/model_converters/publish_model.py helps users to prepare their model for publishing.

Before you upload a model to AWS, you may want to

1. convert model weights to CPU tensors

2. delete the optimizer states and

3. compute the hash of the checkpoint file and append the hash id to the filename.

python tools/model_converters/publish_model.py ${INPUT_FILENAME} ${OUTPUT_FILENAME}

E.g.,

python tools/model_converters/publish_model.py work_dirs/faster_rcnn/latest.pth faster_rcnn_r50_fpn_1x_20190801.pth

The final output filename will be faster_rcnn_r50_fpn_1x_20190801-{hash id}.pth.