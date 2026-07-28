<div style="text-align: center;">Figure 5-2 CTS</div>


<div style="text-align: center;"><img src="imgs/img_in_image_box_410_297_1473_986.jpg" alt="Image" width="64%" /></div>


## Logging

You can enable OBS logging for bucket analysis or audit. After logging is enabled for a bucket, OBS automatically logs access requests for the bucket and writes the generated log files into the specified bucket. With access logs, the bucket owner can deeply analyze the characteristics, types, or trends of requests sent to the bucket.

For the introduction and configuration of OBS logging, see Logging.

### 5.5 Resilience

OBS offers a five-level reliability architecture. It ensures data durability and reliability by leveraging cross-region replication, disaster recovery across AZs, device and data redundancy in an AZ, and detection of slow disks and bad sectors.