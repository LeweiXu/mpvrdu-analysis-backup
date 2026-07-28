| Type                                | Structure                                                                                                                    | Description                                                                                                              | Prot<br>ocol          |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-----------------------|
| Static<br>website<br>domain<br>name | [Structure]<br>BucketName.obs<br>website.Endpoint<br>[Example]<br>bucketname.obs-website.ap<br>southeast-1.myhuaweicloud.com | A static website domain<br>name is a bucket domain<br>name when the bucket is<br>configured to host a static<br>website. | HTT<br>PS<br>HTT<br>P |
| User<br>defined<br>domain<br>name   | Self-owned domain name<br>registered with a domain name<br>provider                                                          | You can bind a user<br>domain name to a bucket<br>so that you can access the<br>bucket through the user<br>domain name.  | HTT<br>P              |

## **9.6 Region and AZ**

## **Concept**

A region and availability zone (AZ) identify the location of a data center. You can create resources in a specific region and AZ.

- Regions are classified based on geographical location and network latency. Public services, such as Elastic Cloud Server (ECS), Elastic Volume Service (EVS), Object Storage Service (OBS), Virtual Private Cloud (VPC), Elastic IP (EIP), and Image Management Service (IMS), are shared within the same region. Regions are classified as universal regions and dedicated regions. A universal region provides universal cloud services for common tenants. A dedicated region provides services of the same type or only provides services for specific tenants.
- An AZ contains one or more physical data centers. Each AZ has independent cooling, fire extinguishing, moisture-proofing, and electricity facilities. Within an AZ, computing, network, storage, and other resources are logically divided into multiple clusters. AZs within a region are interconnected using highspeed optical fibers to allow you to build cross-AZ high-availability systems.

**[Figure 9-2](#page-60-0)** shows the relationship between the regions and AZs.