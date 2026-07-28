demo

## # imports

```
1 %matplotlib inline
 2 import logging
   from glob import glob
   from random import shuffle
   import pickle
 6
   # Make sure that caffe is on the python path:
   caffe_root = '../'
   import sys
   sys.path.insert(0, caffe_root + 'python')
   import caffe
12
   import numpy as np
   import matplotlib.pyplot as plt
15 import matplotlib.image as mpimg
```