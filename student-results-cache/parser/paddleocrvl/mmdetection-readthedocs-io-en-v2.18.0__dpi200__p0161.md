#### 32.11.3 Bug Fixes

• Fix CPU inference bug of Cascade RPN (#4410)

• Fix NMS error of CornerNet when there is no prediction box (#4409)

• Fix TypeError in CornerNet inference (#4411)

• Fix bug of PAA when training with background images (#4391)

• Fix the error that the window data is not destroyed when out_file is not None and show==False (#4442)

• Fix order of NMS score_factor that will decrease the performance of YOLOv3 (#4473)

• Fix bug in HTC TTA when the number of detection boxes is 0 (#4516)

• Fix resize error in mask data structures (#4520)

#### 32.11.4 Improvements

• Allow to customize classes in LVIS dataset (#4382)

• Add tutorials for building new models with existing datasets (#4396)

• Add CPU compatibility information in documentation (#4405)

• Add documentation of deprecated ImageToTensor for batch inference (#4408)

• Add more details in documentation for customizing dataset (#4430)

• Switch imshow_det_bboxes visualization backend from OpenCV to Matplotlib (#4389)

• Deprecate ImageToTensor in image_demo.py (#4400)

• Move train_cfg/test_cfg into model (#4347, #4489)

• Update docstring for reg_ decoded_bbox option in bbox heads (#4467)

• Update dataset information in documentation (#4525)

• Release pre-trained R50 and R101 PAA detectors with multi-scale 3x training schedules (#4495)

• Add guidance for speed benchmark (#4537)

##### 32.12 v2.8.0 (04/01/2021)

#### 32.12.1 Highlights

• Support new methods: Cascade RPN, TridentNet