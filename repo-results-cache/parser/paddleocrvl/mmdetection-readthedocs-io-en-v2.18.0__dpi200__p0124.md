## MODEL SERVING

In order to serve an MMDetection model with TorchServe, you can follow the steps:

#### 22.1 1. Convert model from MMDetection to TorchServe

python tools/deployment/mmdet2torchserve.py ${CONFIG_FILE} ${CHECKPOINT_FILE} \
--output-folder ${MODEL_STORE} \
--model-name ${MODEL_NAME}

Note:  $ \\{MODEL\_STORE\} $ needs to be an absolute path to a folder.

#### 22.2 2. Build mmdet-serve docker image

docker build -t mmdet-serve:latest docker/serve/

#### 22.3 3. Run mmdet-serve

Check the official docs for running TorchServe with docker.

In order to run in GPU, you need to install nvidia-docker. You can omit the --gpus argument in order to run in CPU.

Example:

docker run --rm \
--cpus 8 \
--gpus device=0 \
-p8080:8080 -p8081:8081 -p8082:8082 \
--mount type=bind,source=$MODEL_STORE,target=/home/model-server/model-store \
mmdet-serve:latest

Read the docs about the Inference (8080), Management (8081) and Metrics (8082) APis