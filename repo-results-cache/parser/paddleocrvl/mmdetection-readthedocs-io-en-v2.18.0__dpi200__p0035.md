GPUS=16./tools/slurm_train.sh dev mask_r50_1x config/mask_rcnn_r50_fpn_1x_coco.py /nfs/xxxxx/mask_rcnn_r50_fpn_1x

You can check the source code to review full arguments and environment variables.

When using Slurm, the port option need to be set in one of the following ways:

1. Set the port through --options. This is more recommended since it does not change the original config.

CUDA_VISIBLE_DEVICES=0,1,2,3 GPUS=4./tools/slurm_train.sh ${PARTITION} ${JOB_NAME} config1.py ${WORK_DIR} --options 'dist_params.port=29500' CUDA_VISIBLE_DEVICES=4,5,6,7 GPUS=4./tools/slurm_train.sh ${PARTITION} ${JOB_NAME} config2.py ${WORK_DIR} --options 'dist_params.port=29501'

2. Modify the config files to set different communication ports.

In config1.py, set

dist_params = dict(backend='nccl', port=29500)

In config2.py, set

dist_params = dict(backend='nccl', port=29501)

Then you can launch two jobs with config1.py and config2.py.

CUDA_VISIBLE_DEVICES=0,1,2,3 GPUS=4./tools/slurm_train.sh ${PARTITION} ${JOB_NAME} config1.py ${WORK_DIR}
CUDA_VISIBLE_DEVICES=4,5,6,7 GPUS=4./tools/slurm_train.sh ${PARTITION} ${JOB_NAME} config2.py ${WORK_DIR}