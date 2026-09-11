## CHANGELOG

##### 32.1 v2.18.0 (27/10/2021)

#### 32.1.1 Highlights

• Support QueryInst (#6050)

• Refactor dense heads to decouple onnx export logics from get_bboxes and speed up inference (#5317, #6003, #6369, #6268, #6315)

#### 32.1.2 New Features

• Support QueryInst (#6050)

• Support infinite sampler (#5996)

#### 32.1.3 Bug Fixes

• Fix init_weight in fcn_mask_head (#6378)

• Fix type error in imshow\_bboxes of RPN (#6386)

• Fix broken colab link in MMDetection Tutorial (#6382)

• Make sure the device and dtype of scale_factor are the same as bboxes (#6374)

• Remove sampling hardcode (#6317)

• Fix RandomAffine bbox coordinate recorrection (#6293)

• Fix init bug of final cls/reg layer in convfc head (#6279)

• Fix img_shape broken in auto_augment (#6259)

• Fix kwargs parameter missing error in two_stage (#6256)