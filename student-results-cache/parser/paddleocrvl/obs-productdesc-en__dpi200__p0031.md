<div style="text-align: center;">Figure 5-1 Huawei Cloud shared security responsibility model</div>


<div style="text-align: center;"><img src="imgs/img_in_image_box_397_292_1480_905.jpg" alt="Image" width="65%" /></div>


### 5.2 Identity Authentication and Access Control

## Identity Authentication

You can use OBS Console, OBS Browser+ (a client), obsutil (a command line tool), APIs, and SDKs to access OBS. No matter which method you use, you are accessing OBS over the REST API.

OBS REST APIs support both authenticated and anonymous requests. There will usually be anonymous requests in the scenarios that require public access, for example, accessing a hosted static website. In most cases, requests for OBS resources must be authenticated. An authenticated request must include a signature. The signature is calculated based on the requester's access keys (a pair of AK and SK) that are used as the encryption factor and the specific information included in the request body. OBS uses an access key ID (AK) and a secret access key (SK) together to authenticate the identity of a requester. For more information, see Access Keys (AK/SK).

Other OBS access scenarios include:

• Accessing OBS Using Permanent Access Keys

• Accessing OBS Using Temporary Access Keys

• Accessing OBS Using a Temporary URL

• Accessing OBS Using an IAM Agency

## Access Control

OBS access control can be implemented based on IAM permissions, bucket policies, ACLs, URL validation, and CORS.