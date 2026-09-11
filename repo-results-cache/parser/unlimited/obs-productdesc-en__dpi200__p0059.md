Object Storage Service
Product Introduction
9 Basic Concepts
<table><tr><td>Type</td><td>Structure</td><td>Description</td><td>Protocol</td></tr><tr><td>Static website domain name</td><td>[Structure]BucketName.obs-website.Endpoint[Example]bucketname.obs-website.asp-southeast-1.myhuaweicloud.com</td><td>A static website domain name is a bucket domain name when the bucket is configured to host a static website.</td><td>HTTPSHTP</td></tr><tr><td>User-defined domain name</td><td>Self-owned domain name registered with a domain name provider</td><td>You can bind a user domain name to a bucket so that you can access the bucket through the user domain name.</td><td>HTTP</td></tr></table>
9.6 Region and AZ
Concept
A region and availability zone (AZ) identify the location of a data center. You can create resources in a specific region and AZ.
- Regions are classified based on geographical location and network latency. Public services, such as Elastic Cloud Server (ECS), Elastic Volume Service (EVS), Object Storage Service (OBS), Virtual Private Cloud (VPC), Elastic IP (EIP), and Image Management Service (IMS), are shared within the same region. Regions are classified as universal regions and dedicated regions. A universal region provides universal cloud services for common tenants. A dedicated region provides services of the same type or only provides services for specific tenants.
- An AZ contains one or more physical data centers. Each AZ has independent cooling, fire extinguishing, moisture-proofing, and electricity facilities. Within an AZ, computing, network, storage, and other resources are logically divided into multiple clusters. AZs within a region are interconnected using high-speed optical fibers to allow you to build cross-AZ high-availability systems.
Figure 9-2 shows the relationship between the regions and AZs.
Issue 26 (2024-02-28)
Copyright © Huawei Technologies Co., Ltd.
56