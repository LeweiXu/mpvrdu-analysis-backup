Object Storage Service
Product Introduction
6 Permissions Management
Permissions Required for OBS Console Operations
Table 6-3 Roles or policies that are required for performing operations on OBS Console
<table><tr><td>OBS Console Operation</td><td>Dependency</td><td>Role/Policy Required</td></tr><tr><td>Listing existing domain names (required when you configure a user-defined domain name or an acceleration domain name)</td><td>Domain Name Service (DNS)</td><td>Domains:domains:getDetails</td></tr><tr><td>Configuring mirroring back-to-source rules</td><td>Object Storage Service (OBS)</td><td>Tenant Administratorobs:object:HeadObject and obs:object:PutObject assigned by the IAM agency for OBS to pull data from its origin serverkms:cmk:get, kms:cmk:list, kms:cmk:create, kms:dek:create, kms:dek:crypto, and kms:dek:crypto configured for the agency of OBS when SSE-KMS is enabled for a bucket</td></tr><tr><td>Obtaining mirroring back-to-source rules</td><td>Object Storage Service (OBS)</td><td>Tenant Administrator</td></tr><tr><td>Deleting mirroring back-to-source rules</td><td>Object Storage Service (OBS)</td><td>Tenant Administrator</td></tr><tr><td>Configuring online decompression policies</td><td>Object Storage Service (OBS)</td><td>Tenant Administrator</td></tr><tr><td>Obtaining online decompression policies</td><td>Object Storage Service (OBS)</td><td>Tenant Administrator</td></tr><tr><td>Deleting online decompression policies</td><td>Object Storage Service (OBS)</td><td>Tenant Administrator</td></tr></table>
Issue 26 (2024-02-28)
Copyright © Huawei Technologies Co., Ltd.
41