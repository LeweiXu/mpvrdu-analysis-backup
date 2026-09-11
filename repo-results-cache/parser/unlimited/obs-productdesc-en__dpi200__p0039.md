Object Storage Service
Product Introduction
6 Permissions Management
![](images/0.jpg)

NOTE
Due to data caching, a role and policy involving OBS actions will take effect 10 to 15 minutes after it is attached to a user, an enterprise project, and a user group.
Table 6-1 lists all system permissions of OBS.
Table 6-1 OBS system permissions
<table><tr><td>Role/Policy Name</td><td>Description</td><td>Type</td><td>Depend ency</td></tr><tr><td>Tenant Administrator</td><td>Allows you to perform all operations on all services except IAM.</td><td>System-defined role</td><td>None</td></tr><tr><td>Tenant Guest</td><td>Allows you to perform read-only operations on all services except IAM.</td><td>System-defined role</td><td>None</td></tr><tr><td>OBS Administrator</td><td>Allows you to perform any operation on all OBS resources under the account.</td><td>System-defined policy</td><td>None</td></tr><tr><td>OBS Buckets Viewer</td><td>Allows you to list buckets, and obtain basic bucket information and bucket metadata.</td><td>System-defined role</td><td>None</td></tr><tr><td>OBS ReadOnlyAccess</td><td>Allows you to list buckets, obtain basic bucket information and bucket metadata, and list objects (excluding versioned objects).NOTEIf a user with this permission fails to list objects on OBS Console, there may be multiple versions of objects in the bucket. In this case, you need to grant the user the obs:bucket:ListBucketVersions permission so that the user can view different versions of objects on OBS Console.</td><td>System-defined policy</td><td>None</td></tr><tr><td>OBS OperateAccess</td><td>Allows you to perform all operations defined in OBS ReadOnlyAccess and to perform basic object operations, such as uploading objects, downloading objects, deleting objects, and obtaining object ACLs.NOTEIf a user with this permission fails to list objects on OBS Console, there may be multiple versions of objects in the bucket. In this case, you need to grant the user the obs:bucket:ListBucketVersions permission so that the user can view different versions of objects on OBS Console.</td><td>System-defined policy</td><td>None</td></tr></table>
Issue 26 (2024-02-28)
Copyright © Huawei Technologies Co., Ltd.
36