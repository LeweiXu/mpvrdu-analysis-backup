<div style="text-align: center;">Figure 9-2 Regions and AZs</div>


<div style="text-align: center;"><img src="imgs/img_in_image_box_395_290_1219_689.jpg" alt="Image" width="49%" /></div>


Huawei Cloud provides services in many regions around the world. You can select a region and AZ according to your requirement. For more information, see Huawei Cloud Global Regions.

## How Do I Select a Region?

When selecting a region, consider the following factors:

• Location

Select a region close to you or your target users. This reduces network latency and improves access speed. However, Chinese mainland regions provide the same infrastructure, BGP network quality, as well as resource operations and configurations. If you or your target users are in the Chinese mainland, you do not need to consider differences in network latency when selecting a region.

If you or your target users are in the Asia Pacific region (excluding the Chinese mainland), select regions such as AP-Bangkok and AP-Singapore.

If you or your target users are in Africa, select the AF-Johannesburg region.

If you or your target users are in Europe, select the EU-Paris region.

• Resource prices

Resource prices may vary depending on different regions. For details, see Product Pricing Details.

## How Do I Select an AZ?

When determining whether to deploy resources in the same AZ, consider your applications' requirements for disaster recovery (DR) and network latency.

- For high DR capability, deploy resources in different AZs in the same region.

- For low network latency, deploy resources in the same AZ.

## Regions and Endpoints

Before using an API to call resources, you must specify its region and endpoint. For details about Huawei Cloud regions and endpoints, see Regions and Endpoints.