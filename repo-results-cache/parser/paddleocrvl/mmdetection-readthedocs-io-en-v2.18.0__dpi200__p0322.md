• br_heats (list [Tensor]) – Bottom-right corner heatmaps for each level with shape (N, num_classes, H, W).

• tl_offs (list[Tensor]) – Top-left corner offsets for each level with shape (N, corner_offset_channels, H, W).

• br_offs (list[Tensor]) – Bottom-right corner offsets for each level with shape (N, corner_offset_channels, H, W).

• tl_guiding_shifts (list [Tensor]) – Top-left guiding shifts for each level with shape (N, guiding_shift_channels, H, W). Useless in this function, we keep this arg because it's the raw output from CentripetalHead.

• br_guiding_shifts (list[Tensor]) – Bottom-right guiding shifts for each level with shape (N, guiding_shift_channels, H, W). Useless in this function, we keep this arg because it’s the raw output from CentripetalHead.

• tl_centripetal_shifts (list[Tensor]) – Top-left centripetal shifts for each level with shape (N, centripetal_shift_channels, H, W).

• br_centripetal_shifts (list[Tensor]) – Bottom-right centripetal shifts for each level with shape (N, centripetal_shift_channels, H, W).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• rescale (bool) – If True, return boxes in original image space. Default: False.

• with_nms (bool) – If True, do nms before return boxes. Default: True.

## init_weights()

Initialize the weights.

loss(tl_heats, br_heats, tl_offs, br_offs, tl_guiding_shifts, br_guiding_shifts, tl_centripetal_shifts,

 $ br\_centripetal\_shifts $,  $ gt\_bboxes $,  $ gt\_labels $,  $ img\_metas $,  $ gt\_bboxes\_ignore=None $

Compute losses of the head.

## Parameters

• tl_heats (list[Tensor]) – Top-left corner heatmaps for each level with shape (N, num_classes, H, W).

• br_heats (list [Tensor]) – Bottom-right corner heatmaps for each level with shape (N, num_classes, H, W).

• tl_offs (list[Tensor]) – Top-left corner offsets for each level with shape (N, corner_offset_channels, H, W).

• br_offs (list[Tensor]) – Bottom-right corner offsets for each level with shape (N, corner_offset_channels, H, W).

• tl_guiding_shifts (list [Tensor]) – Top-left guiding shifts for each level with shape (N, guiding_shift_channels, H, W).

• br_guiding_shifts (list[Tensor]) – Bottom-right guiding shifts for each level with shape (N, guiding_shift_channels, H, W).

• tl_centripetal_shifts (list[Tensor]) – Top-left centripetal shifts for each level with shape (N, centripetal_shift_channels, H, W).

• br_centripetal_shifts (list[Tensor]) – Bottom-right centripetal shifts for each level with shape (N, centripetal_shift_channels, H, W).