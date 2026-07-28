Object Storage Service
Product Introduction
1 About OBS
- You can specify custom metadata to describe the object when you upload an object to OBS.
- Data that refers to the content of an object.
By means of secondary development based on OBS REST APIs, OBS Console, SDKs, and a variety of tools are provided for you to use OBS. You can also use OBS SDKs and APIs to develop applications customized for your business needs.
Figure 1-1 Product architecture
![](images/0.jpg)

Storage Classes
OBS offers the storage classes below to meet your requirements for storage performance and costs. You can change buckets and objects between storage classes. To learn billing for different storage classes, see Storage Space.
- Standard: The Standard storage class features low latency and high throughput. It is therefore good for storing frequently (multiple times per month) accessed files or small files (less than 1 MB). Its application scenarios include big data analytics, mobile apps, hot videos, and social apps.
- Infrequent Access: The Infrequent Access storage class is for storing data that is infrequently (less than 12 times per year) accessed, but when needed, the access has to be fast. It can be used for file synchronization, file sharing, enterprise backups, and many other scenarios. This storage class has the same durability, low latency, and high throughput as the Standard storage class, with a lower cost, but its availability is slightly lower than the Standard storage class.
- Archive: The Archive storage class is ideal for storing data that is rarely (once per year) accessed. Its application scenarios include data archive and long-term backups. This storage class is secure, durable, and inexpensive, so it can be used to replace tape libraries. To keep cost low, it may take hours to restore data from the Archive storage class.
Issue 26 (2024-02-28)
Copyright © Huawei Technologies Co., Ltd.
2