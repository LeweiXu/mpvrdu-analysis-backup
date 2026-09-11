(continued from previous page)

B x R

Therefore, CUDA memory runs out frequently.

Experiments on GeForce RTX 2080Ti (11019 MiB):

| dtype | M | N | Use | Real | Ideal |
|------|------|------|------|------|------|
| FP32 | 512 | 400000 | 8020 MiB | -- | -- |
| FP16 | 512 | 400000 | 4504 MiB | 3516 MiB | 3516 MiB |
| FP32 | 40 | 400000 | 1540 MiB | -- | -- |
| FP16 | 40 | 400000 | 1264 MiB | 276 MiB | 275 MiB |

2) is_aligned is True

area1: N x 1

area2: N x 1

lt: N x 2

rb: N x 2

wh: N x 2

overlap: N x 1

union: N x 1

ious: N x 1

Total memory:

S = 11 x N * 4 Byte

When using FP16, we can reduce:

R = 11 x N * 4 / 2 Byte

So do the 'giou' (large than 'iou').

Time-wise, FP16 is generally faster than FP32.

When gpu_assign_thr is not -1, it takes more time on cpu but not reduce memory.

There, we can reduce half the memory and keep the speed.

If is_aligned is False, then calculate the overlaps between each bbox of bboxes1 and bboxes2, otherwise the overlaps between each aligned pair of bboxes1 and bboxes2.

## Parameters

• bboxes1 (Tensor) – shape (B, m, 4) in  $ \langle x1, y1, x2, y2\rangle $ format or empty.

• bboxes2 (Tensor) – shape (B, n, 4) in  $ <x_{1}, y_{1}, x_{2}, y_{2}> $ format or empty. B indicates the batch dim, in shape (B1, B2,..., Bn). If is_aligned is True, then m and n must be equal.

• mode (str) – “iou” (intersection over union), “iof” (intersection over foreground) or “giou” (generalized intersection over union). Default “iou”.

• is_aligned (bool, optional) – If True, then m and n must be equal. Default False.

• eps (float, optional) – A value added to the denominator for numerical stability. Default 1e-6.

Returns shape (m, n) if is_aligned is False else shape (m,)