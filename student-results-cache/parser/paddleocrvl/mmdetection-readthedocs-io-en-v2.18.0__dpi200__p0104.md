(continued from previous page)

--output-file checkpoints/yolo/yolov3_d53_mstrain-608_273e_coco.onnx \
--input-img demo/demo.jpg \
--test-img tests/data/color.jpg \
--shape 608 608 \
--show \
--verify \
--dynamic-export \
--cfg-options \
    model.test_cfg.deploy_nms_pre=-1 \

### 15.2 How to evaluate the exported models

We prepare a tool tools/deployment/test.py to evaluate ONNX models with ONNXRuntime and TensorRT.

#### 15.2.1 Prerequisite

• Install onnx and onnxruntime (CPU version)

pip install onnx onnxruntime==1.5.1

• If you want to run the model on GPU, please remove the CPU version before using the GPU version.

pip uninstall onnxruntime
pip install onnxruntime-gpu

Note: onnxruntime-gpu is version-dependent on CUDA and CUDNN, please ensure that your environment meets the requirements.

• Build custom operators for ONNX Runtime following How to build custom operators for ONNX Runtime

• Install TensorRT by referring to How to build TensorRT plugins in MMCV (optional)

#### 15.2.2 Usage

python tools/deployment/test.py \
${CONFIG_FILE} \
${MODEL_FILE} \
--out ${OUTPUT_FILE} \
--backend ${BACKEND} \
--format-only ${FORMAT_ONLY} \
--eval ${EVALUATION_METRICS} \
--show-dir ${SHOW_ DIRECTORY} \
----show-score-thr ${SHOW_SCORE_THRESHOLD} \
----cfg-options ${CFG_OPTIONS} \
----eval-options ${EVALUATION_OPTIONS} \