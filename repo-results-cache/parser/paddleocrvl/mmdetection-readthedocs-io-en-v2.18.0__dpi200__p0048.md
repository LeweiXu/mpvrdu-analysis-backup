# TUTORIAL 1: LEARN ABOUT CONFIGS

We incorporate modular and inheritance design into our config system, which is convenient to conduct various experiments. If you wish to inspect the config file, you may run python tools/misc/print_config.py /PATH/TO/CONFIG to see the complete config.

### 8.1 Modify config through script arguments

When submitting jobs using “tools/train.py” or “tools/test.py”, you may specify --cfg-options to in-place modify the config.

• Update config keys of dict chains.

The config options can be specified following the order of the dict keys in the original config. For example, --cfg-options model.backbone.norm_eval=False changes the all BN modules in model backbones to train mode.

• Update keys inside a list of config.

Some config dicts are composed as a list in your config. For example, the training pipeline data.train.pipeline is normally a list e.g. [dict(type='LoadImageFromFile'),...]. If you want to change 'LoadImageFromFile' to 'LoadImageFromWebcam' in the pipeline, you may specify --cfg-options data.train.pipeline.0.type=LoadImageFromWebcam.

• Update values of list/tuples.

If the value to be updated is a list or a tuple. For example, the config file normally sets workflow=[('train', 1)]. If you want to change this key, you may specify --cfg-options workflow=[((train,1), (val,1)]]. Note that the quotation mark “ is necessary to support list/tuple data types, and that NO white space is allowed inside the quotation marks in the specified value.

### 8.2 Config File Structure

There are 4 basic component types under config/_base_, dataset, model, schedule, default_runtime. Many methods could be easily constructed with one of each like Faster R-CNN, Mask R-CNN, Cascade R-CNN, RPN, SSD. The configs that are composed by components from _base_ are called primitive.

For all configs under the same folder, it is recommended to have only one primitive config. All other configs should inherit from the primitive config. In this way, the maximum of inheritance level is 3.

For easy understanding, we recommend contributors to inherit from existing methods. For example, if some modification is made based on Faster R-CNN, user may first inherit the basic Faster R-CNN structure by specifying  $ _{base} $ =../faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py, then modify the necessary fields in the config files.