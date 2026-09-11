mmcv-full to build MMCV for Volta GPUs. The compatibility issue could happen when using old GPUS, e.g., Tesla K80 (3.7) on colab.

3. Check whether the running environment is the same as that when mmcv/mmdet has compiled. For example, you may compile mmcv using CUDA 10.0 but run it on CUDA 9.0 environments.

• “undefined symbol” or “cannot open xxx.so”.

1. If those symbols are CUDA/C++ symbols (e.g., libcudart.so or GLIBCXX), check whether the CUDA/GCC runtimes are the same as those used for compiling mmcv, i.e. run python mmdet/utils/collect_env.py to see if "MMCV Compiler"/"MMCV CUDA Compiler" is the same as "GCC"/"CUDA_HOME".

2. If those symbols are PyTorch symbols (e.g., symbols containing caffe, aten, and TH), check whether the PyTorch version is the same as that used for compiling mmcv.

3. Run python mmdet/utils/collect_env.py to check whether PyTorch, torchvision, and MMCV are built by and running on the same environment.

- setuptools.sandbox.UnpickleableException: DistutilsSetupError("each element of 'ext_modules' option must be an Extension instance or 2-tuple")

1. If you are using miniconda rather than anaconda, check whether Cython is installed as indicated in #3379. You need to manually install Cython first and then run command pip install -r requirements.txt.

2. You may also need to check the compatibility between the setuptools, Cython, and PyTorch in your environment.

• "Segmentation fault".

1. Check you GCC version and use GCC 5.4. This usually caused by the incompatibility between PyTorch and the environment (e.g., GCC < 4.9 for PyTorch). We also recommend the users to avoid using GCC 5.5 because many feedbacks report that GCC 5.5 will cause “segmentation fault” and simply changing it to GCC 5.4 could solve the problem.

2. Check whether PyTorch is correctly installed and could use CUDA op, e.g. type the following command in your terminal.

python -c 'import torch; print(torch.cuda.is_available())'

And see whether they could correctly output results.

3. If Pytorch is correctly installed, check whether MMCV is correctly installed.

python -c 'import mmcv; import mmcv.ops'

If MMCV is correctly installed, then there will be no issue of the above two commands.

4. If MMCV and Pytorch is correctly installed, you can use ipdb, pdb to set breakpoints or directly add 'print' in mmdetection code and see which part leads the segmentation fault.

### 33.3 Training

• "Loss goes Nan"

1. Check if the dataset annotations are valid: zero-size bounding boxes will cause the regression loss to be Nan due to the commonly used transformation for box regression. Some small size (width or height are smaller than 1) boxes will also cause this problem after data augmentation (e.g., instaboost). So check the data and try to filter out those zero-size boxes and skip some risky augmentations on the small-size boxes when you face the problem.