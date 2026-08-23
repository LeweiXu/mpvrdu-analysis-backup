### 9.3 Parallel File System

Parallel File System (PFS) is a high-performance semantic file system provided by OBS. It features access latency in milliseconds, TB/s-level bandwidth, and millions of IOPS, which makes it ideal for processing high-performance computing (HPC) workloads.

It also supports data read and write through obsfs, a PFS client that supports POSIX. obsfs can be deployed on a Linux ECS, and then you can use obsfs to mount a parallel file system to that server. Once mounted, PFS functions like a local file system. You can manage the PFS online, including creating, deleting, renaming files and folders, or modifying files.

For details about PFS, see the Parallel File System Feature Guide.

### 9.4 Access Keys (AK/SK)

OBS uses an access key ID (AK) and secret access key (SK) to authenticate the identity of a requester. When you use OBS APIs for secondary development and use the AK and SK for authentication, the signature must be calculated based on the algorithm defined by OBS and added to the request.

The authentication can be based on a permanent AK and SK pair, or based on a temporary AK/SK pair and security token.

## Permanent AK/SK Pair

You can create a pair of permanent AK and SK on the My Credentials page. For details, see Obtaining Access Keys (AK and SK).

- Access key ID (AK): indicates the ID of the access key. It is the unique ID associated with the SK. The AK and SK are used together to obtain an encrypted signature for a request.

- Secret access key (SK): indicates the private key used together with its associated AK to cryptographically sign requests. The AK and SK are used together to identify a request sender to prevent the request from being modified.

## Temporary AK/SK Pair

A temporary AK/SK pair and security token assigned by OBS comply with the principle of least privilege and are for temporarily accessing OBS. They are valid from 15 minutes to 24 hours, and need to be obtained again once they expire. If the security token is missing from your request, a 403 error will be returned.

- Temporary AK: indicates the ID of a temporary access key. It is the unique ID associated with the SK. The AK and SK are used together to obtain an encrypted signature for a request.

- Temporary SK: indicates the temporary private key used together with its associated temporary AK. The AK and SK are used together to identify a request sender to prevent the request from being modified.

- Security token: indicates the token used together with the temporary AK and SK to access all resources of a specified account.