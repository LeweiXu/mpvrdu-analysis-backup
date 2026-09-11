# FREQUENTLY ASKED QUESTIONS

We list some common troubles faced by many users and their corresponding solutions here. Feel free to enrich the list if you find any frequent issues and have ways to help others to solve them. If the contents here do not cover your issue, please create an issue using the provided templates and make sure you fill in all required information in the template.

### 33.1 MMCV Installation

• Compatibility issue between MMCV and MMDetection; “ConvWS is already registered in conv layer”; “AssertionError: MMCV==xxx is used but incompatible. Please install mmcv>=xxx, <=xxx.”

Please install the correct version of MMCV for the version of your MMDetection following the installation instruction.

• "No module named'mmcv.ops'"; "No module named'mmcv.ext'".

1. Uninstall existing mmcv in the environment using pip uninstall mmcv.

2. Install mmcv-full following the installation instruction.

### 33.2 PyTorch/CUDA Environment

• "RTX 30 series card fails when building MMCV or MMDet"

1. Temporary work-around: do MMCV_WITH_OPS=1 MMCV_CUDA_ARGS='-gencode=arch=compute_80,code=sm_80' pip install -e.. The common issue is nvcc fatal: unsupported gpu architecture 'compute_86'. This means that the compiler should optimize for sm_86, i.e., nvidia 30 series card, but such optimizations have not been supported by CUDA toolkit 11.0. This work-around modifies the compile flag by adding MMCV_CUDA_ARGS='-gencode=arch=compute_80,code=sm_80', which tells nvcc to optimize for sm_80, i.e., Nvidia A100. Although A100 is different from the 30 series card, they use similar ampere architecture. This may hurt the performance but it works.

2. PyTorch developers have updated that the default compiler flags should be fixed by pytorch/pytorch#47585\. So using PyTorch-nightly may also be able to solve the problem, though we have not tested it yet.

• “invalid device function” or “no kernel image is available for execution”.

1. Check if your cuda runtime version (under /usr/local/), nvcc --version and conda list cudatoolkit version match.

2. Run python mmdet/utils/collect_env.py to check whether PyTorch, torchvision, and MMCV are built for the correct GPU architecture. You may need to set TORCH_CUDA_ARCH_LIST to reinstall MMCV. The GPU arch table could be found here, i.e. run TORCH_CUDA_ARCH_LIST=7.0 pip install