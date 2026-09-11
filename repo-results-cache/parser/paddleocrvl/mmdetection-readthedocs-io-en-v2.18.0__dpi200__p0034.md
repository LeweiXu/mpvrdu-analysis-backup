This tool accepts several optional arguments, including:

• --no-validate (not suggested): Disable evaluation during training.

• --work-dir ${WORK_DIR}: Override the working directory.

• --resume-from ${CHECKPOINT_FILE}: Resume from a previous checkpoint file.

• --options 'Key=value': Overrides other settings in the used config.

## Note:

Difference between resume-from and load-from:

resume-from loads both the model weights and optimizer status, and the epoch is also inherited from the specified checkpoint. It is usually used for resuming the training process that is interrupted accidentally. load-from only loads the model weights and the training epoch starts from 0. It is usually used for finetuning.

#### 5.3.3 Training on multiple GPUs

We provide tools/dist_train.sh to launch training on multiple GPUs. The basic usage is as follows.

bash./tools/dist_train.sh \
${CONFIG_FILE} \
${GPU_NUM} \
[optional arguments]

Optional arguments remain the same as stated above.

## Launch multiple jobs simultaneously

If you would like to launch multiple jobs on a single machine, e.g., 2 jobs of 4-GPU training on a machine with 8 GPUs, you need to specify different ports (29500 by default) for each job to avoid communication conflict.

If you use dist_train.sh to launch training jobs, you can set the port in commands.

CUDA_VISIBLE_DEVICES=0,1,2,3 PORT=29500./tools/dist_train.sh ${CONFIG_FILE} 4
CUDA_VISIBLE_DEVICES=4,5,6,7 PORT=29501./tools/dist_train.sh ${CONFIG_FILE} 4

#### 5.3.4 Training on multiple nodes

MMDetection relies on torch.distributed package for distributed training. Thus, as a basic usage, one can launch distributed training via PyTorch's launch utility.

#### 5.3.5 Manage jobs with Slurm

Slurm is a good job scheduling system for computing clusters. On a cluster managed by Slurm, you can use slurm_train.sh to spawn training jobs. It supports both single-node and multi-node training.

The basic usage is as follows.

[GPUS=${GPUS}]./tools/slurm_train.sh ${PARTITION} ${JOB_NAME} ${CONFIG_FILE} ${WORK_DIR}

Below is an example of using 16 GPUs to train Mask R-CNN on a Slurm partition named dev, and set the work-dir to some shared file systems.