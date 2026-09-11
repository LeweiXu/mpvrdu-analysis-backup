# install mmdetection
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -r requirements/build.txt
pip install -v -e.

(continued from previous page)

### 2.6 Developing with multiple MMDetection versions

The train and test scripts already modify the PYTHONPATH to ensure the script uses the MMDetection in the current directory.

To use the default MMDetection installed in the environment rather than that you are working with, you can remove the following line in those scripts

PYTHONPATH="$(dirname $0)/..": PYTHONPATH