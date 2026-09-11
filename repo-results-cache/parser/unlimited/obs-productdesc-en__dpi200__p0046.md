Object Storage Service
Product Introduction
7 Restrictions and Limitations
7 Restrictions and Limitations
This section describes the restrictions on using OBS features.
Table 7-1 OBS use restrictions and limitations
<table><tr><td>Item</td><td>Description</td></tr><tr><td>Bandwidth</td><td>By default, the maximum bandwidth for read/write (GET/PUT) requests of a single Huawei Cloud account is 16 Gbit/s. If the actual bandwidth reaches the threshold, flow control will be triggered.If you require a bandwidth higher than 16 Gbit/s, submit a service ticket.</td></tr><tr><td>Queries per second (QPS)</td><td>Default maximum QPS allowed by a single Huawei Cloud account:6,000 write requests (PUT Object) per second10,000 read requests (GET Object) per second1,000 listing requests (LIST) per secondNOTEIf you use sequential prefixes (such as timestamps or alphabetical order) for object naming, object access requests may be concentrated in a specific partition, resulting in access hotspots. This limits the request rate in a hotspot partition and increases access delay.Random prefixes are recommended for naming objects so that requests are evenly distributed across partitions, achieving horizontal expansion. For details about how to name objects with random prefixes, see Optimizing the Performance.If you require a higher QPS, submit a service ticket.</td></tr></table>
Issue 26 (2024-02-28)
Copyright © Huawei Technologies Co., Ltd.
43