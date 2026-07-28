When using the following tools to access OBS resources, you need to use the AK/SK pair for security authentication.

<div style="text-align: center;">Table 9-1 OBS resource management tools</div>



<table border=1 style='margin: auto; word-wrap: break-word;'><tr><td style='text-align: center; word-wrap: break-word;'>Tool</td><td style='text-align: center; word-wrap: break-word;'>AK/SK Configuration</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>OBS Browser+</td><td style='text-align: center; word-wrap: break-word;'>Configure the AK and SK during login account configuration. For details, see Logging In to OBS Browser+.</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>obsutil</td><td style='text-align: center; word-wrap: break-word;'>Configure the AK and SK when initializing the configuration. For details, see Performing the Initial Configuration.</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>obsfs</td><td style='text-align: center; word-wrap: break-word;'>Configure the AK and SK when initializing the configuration. For details, see Initializing obsfs.</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>SDKs</td><td style='text-align: center; word-wrap: break-word;'>Configure the AK and SK in the initialization phase. For details, see the SDK Reference.</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>APIs</td><td style='text-align: center; word-wrap: break-word;'>Add the AK/SK pair to the request when computing the signature. For details, see User Signature Authentication.</td></tr></table>

## References

For details about how to obtain a permanent AK/SK pair, see Obtaining Access Keys (AK and SK).

For details about how to obtain a temporary AK/SK pair and security token, see Obtaining a Temporary Access Key Pair and Security Token.

### 9.5 Endpoints and Domain Names

Endpoint: OBS provides an endpoint for each region. An endpoint is considered a domain name to access OBS in a region and is used to process requests of that region. For details about regions and endpoints, see Regions and Endpoints.

Bucket domain name: Each bucket in OBS has a domain name. A domain name is the address of a bucket and can be used to access the bucket over the Internet. It is applicable to cloud application development and data sharing.

An OBS bucket domain name is in the format of BucketName.Endpoint, where BucketName indicates the name of the bucket, and Endpoint indicates the domain name of the region where the bucket is located.

Table 9-2 lists the bucket domain name and other domain names in OBS, including their structure and protocols.