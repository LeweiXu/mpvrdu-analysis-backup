Object Storage Service
Product Introduction
· Deep Archive: The Deep Archive storage class (under limited beta testing) is suitable for storing data that is barely (once every few years) accessed. This storage class costs less than the Archive storage class, but takes longer time (usually several hours) to restore data.
An object uploaded to a bucket inherits the storage class of the bucket by default. You can also specify a storage class for an object when you upload it.
Changing the storage class of a bucket does not change the storage classes of existing objects in the bucket, but newly uploaded objects will inherit the new storage class.
Table 1-1 Comparison between storage classes
Compared Item Standard Infrequent Access Archive Deep Archive (Under Limited Beta Testing)
Feature Top-notch performance, high reliability and availability Reliable, inexpensive storage with real-time access Long-term retention of archived data at a low cost Lower price than the Archive storage class for long-term data archive.
Application scenarios Cloud application, data sharing, content sharing, and hot data storage Web disk applications, enterprise backup, active archiving, and data monitoring Archive, medical image storage, video material storage, and replacement of tape libraries Archiving data that is barely accessed.
Designed durability 99.99999999 99% 99.99999999 99% 99.99999999 99% Multi-AZ not supported Multi-AZ not supported
Designed durability (multi-AZ) 99.99999999 99% 99% 99% Multi-AZ not supported Multi-AZ not supported
Designed availability 99.995% 99.5% Multi-AZ not supported Multi-AZ not supported
Minimum storage duration N/A 30 days 90 days 180 days
Issue 26 (2024-02-28) Copyright © Huawei Technologies Co., Ltd.