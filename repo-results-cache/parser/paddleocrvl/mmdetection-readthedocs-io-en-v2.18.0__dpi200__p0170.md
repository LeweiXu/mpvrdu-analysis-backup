• Add DetectoRS (#3064)

• Support Generalize Focal Loss (#3097)

• Support PointRend (#2752)

• Support Dynamic R-CNN (#3040)

• Add DeepFashion dataset (#2968)

• Implement FCOS training tricks (#2935)

• Use BaseDenseHead as base class for anchor-base heads (#2963)

• Add with cp for BasicBlock (#2891)

• Add stem_channels argument for ResNet (#2954)

## Improvements

• Add anchor free base head (#2867)

• Migrate to github action (#3137)

• Add docstring for datasets, pipelines, core modules and methods (#3130, #3125, #3120)

• Add VOC benchmark (#3060)

• Add concat mode in GRoI (#3098)

• Remove cmd arg autorescale-lr (#3080)

• Use len(data['img_metas']) to indicate num_samples (#3073, #3053)

• Switch to EpochBasedRunner (#2976)

##### 32.19 v2.1.0 (8/6/2020)

## Highlights

• Support new backbones: RegNetX, Res2Net

• Support new methods: NASFCOS, PISA, GRoIE

• Support new dataset: LVIS

## Bug Fixes

• Change the CLI argument --validate to --no-validate to enable validation after training epochs by default. (#2651)

• Add missing cython to docker file (#2713)

• Fix bug in nms cpu implementation (#2754)

• Fix bug when showing mask results (#2763)

• Fix gcc requirement (#2806)

• Fix bug in async test (#2820)

• Fix mask encoding-decoding bugs in test API (#2824)

• Fix bug in test time augmentation (#2858, #2921, #2944)

• Fix a typo in comment of apis/train (#2877)