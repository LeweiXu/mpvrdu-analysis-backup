<div style="text-align: center;">Figure 3-5 Video surveillance</div>


<div style="text-align: center;"><img src="imgs/img_in_image_box_394_283_1368_1047.jpg" alt="Image" width="58%" /></div>


## Backup and Archiving

## Scenario Description

OBS offers a highly reliable, inexpensive storage system featuring high concurrency and low latency. It can hold massive amounts of data, meeting the archive needs for unstructured data of applications and databases.

You can use the synchronization clients (such as OBS Browser+ and obsutil), Cloud Storage Gateway (CSG), DES, or mainstream backup software to back up your on-premises data to OBS. OBS also provides lifecycle rules to automatically transition objects between storage classes to save your money on storage. You can restore data from OBS to a DR or test host on the cloud.

- Synchronization clients: good for manual backup of a single database or program

- Backup software: applicable to automatic backup for multiple applications or hosts, delivering strong compatibility

- CSG: seamlessly compatible with on-premises backup systems

- DES: ideal for archiving massive volumes of data. It transfers data using Teleport devices and disks to cloud.

## Recommended Services

Data Express Service (DES) and Elastic Cloud Server (ECS)