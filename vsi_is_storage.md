---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-04"

subcollection: virtual-servers-is

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# Storage
{: #storage}

When you provision an {{site.data.keyword.vsi_is_full}} instance, a 100 GB, general purpose IOPS (3 IOPS/GB) block storage volume is 
automatically created as a primary boot volume and attached to the instance. You can also create secondary data volumes, which are automatically attached to the instance.
{:shortdesc}

- For more information about block storage volumes for the VPC, see [About Block Storage for VPC](/docs/infrastructure/block-storage-is?topic=block-storage-is-block-storage-about).  
- To get started creating volumes independent of virtual server instance provisioning, see [Getting Started with {{site.data.keyword.block_storage_is_short}}](/docs/infrastructure/block-storage-is?topicid=block-storage-is-block-storage-getting-started).

By default, boot and data volumes are encrypted with IBM-managed encryption. You can also encrypt your volumes using your own encyption keys, during instance provisioning or when [creating a standalone volume](/docs/infrastructure/block-storage-is?topic=block-storage-is-block-storage-encryption).  

Boot volumes are deleted when you delete the virtual server instance. By default, data volumes persist when detached from the instance; you can later attach the volume to a new instance. Alternatively, you can specify that data volumes are automatically deleted when you delete the instance.  

## Customer managed encryption for block storage  
{: #customer-managed-encryption-keys}

You can create {{site.data.keyword.vsi_is_full}} with block storage encryption and your own data encryption keys that you manage. You just need the {{site.data.keyword.keymanagementservicelong_notm}} service and your own data encryption key to get started.
{:shortdesc}

### Prerequisites
{: #byok-vsi-prereqs}

To create a virtual server instance that uses customer managed encryption for the block storage volumes, you must have a service instance of {{site.data.keyword.keymanagementserviceshort}} that includes a customer root key. You must also authorize access between Cloud Block Storage and Key Protect. When you've completed these prerequisites, you can start creating instances that use customer managed encryption for the block storage volumes. 

1. Provision the [{{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect?topic=key-protect-provision#provision) service. 
   
   Provisioning a new {{site.data.keyword.keymanagementserviceshort}} service instance ensures that it includes the most recent updates that are required for customer managed encryption of block storage volumes. 
   {: tip}
   
2. [Create](/docs/services/key-protect?topic=key-protect-create-root-keys#create-root-keys) or 
[import](/docs/services/key-protect?topic=key-protect-import-root-keys#import-root-keys) a root key (CRK) in 
{{site.data.keyword.keymanagementservicelong_notm}}.
3. From IBM {{site.data.keyword.iamshort}} (IAM), [authorize access](/docs/iam?topic=iam-serviceauth#serviceauth) between **Cloud 
Block Storage** (source service) and **{{site.data.keyword.keymanagementserviceshort}}** (target service).

### Provisioning virtual server instances with volumes that use customer managed encryption
{: #provision-byok-ui}

When you provision a virtual server instance, you can specify customer managed encryption for your boot volume and any data volumes that you want to add at provision time. If you want, you can use a combination of provider managed encryption and customer managed encryption for the volumes that are associated with your instance.

1. In [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.cloud.ibm.com/vpc), navigate to **Menu icon ![Menu icon](../icons/icon_hamburger.svg) > VPC Infrastructure > Compute > Virtual server instances**. Click **New instance** and complete the required fields. (For more information about creating instances, see [Create a virtual server instance](/docs/vsi-is?topic=virtual-servers-is-creating-virtual-servers#creating-virtual-servers).) 
2. In the **Boot volume** section, the default mode of encryption is _Provider managed_ encryption. To specify _Customer managed_ encryption, click the pencil icon in the boot volume row. On the **Edit boot volume** page, update the fields in the **Encryption** section. See the following table for more information. When your changes are complete, click **Apply**.
3. In the **Attached block storage volume** section, you can click **New block storage volume** to add a data volume and specify customer managed encryption if you choose. On the **New block storage volume** page, update the fields in the **Encryption** section. See the following table for more information. When your changes are complete, click **Attach**.

| Field | Value |
| ----- | ----- |
| Encryption | _Provider managed_ is the default encryption mode. To use customer managed encryption, select a {{site.data.keyword.keymanagementserviceshort}} instance in your account from the drop-down list. The {{site.data.keyword.keymanagementserviceshort}} instance should include the customer root key that you want to use for customer managed encryption. |
| Key name | Select the data encryption key within the {{site.data.keyword.keymanagementserviceshort}} instance that you want to use for encrypting the volume. | 
| Key ID | Displays the key ID that is associated with the data encryption key that you selected. | 
{: caption="Table 1. Values for specifying customer managed encryption of volumes" caption-side="top"}

### Using the CLI to provision instances and volumes with customer managed encryption
{: #provision-byok-cli}

To use the CLI to create a virtual server instance with volumes that use customer managed encryption, you can use the ```ibmcloud is instance-create``` command and reference a JSON to attach volumes that use customer managed encryption. 

1. Obtain the CRN of the root key in your desired {{site.data.keyword.keymanagementserviceshort}} service instance.
    
    1. If you don't already have the {{site.data.keyword.keymanagementserviceshort}} CLI plugin installed, install it by running the following command: 
       ```
       ibmcloud plugin update key-protect -r 'IBM Cloud'
       ```
       {: pre}
    
    2. List the {{site.data.keyword.keymanagementserviceshort}} service instances for your account by running the following command:
       ```
       ibmcloud resource service-instances
       ```
       {: pre}
    
       For this example, you'd see a response similar to the following output:
       ```
       Retrieving all instances of all services in resource group Default and all locations
       under account MyCompany as myuserid@mycompany.com...
       OK
       Name             Location   State    Type   
       Key Protect-17   us-south   active   service_instance
       Key Protect-60   us-south   active   service_instance
       ```
       {:screen}
         
    3. Retrieve the instance ID for the {{site.data.keyword.keymanagementserviceshort}} service instance where your customer root keys are stored by running the following command.  
       ```
       ibmcloud resource service-instance "Key Protect-17" --id
       ```
       {: pre}
    
       where _Key Protect-17_ is your desired {{site.data.keyword.keymanagementserviceshort}} service instance.
    
       For this example, you'd see a response similar to the following output:
       ```
       Retrieving service instance Key Protect-17 in resource group Default under account 
       MyCompany as myuserid@mycompany.com...
       crn:v1:bluemix:public:kms:us-south:a/abxx1c2xxxx34x567xxdex891xxx23fx:xxx4g5xx-6789-x1h2-
       ixxx-3jkl4xxxx567::7mnxxxo8-91xx-23px-q4rs-xxtuv5w6xxx7  
       ```
       {:screen}
       
       where the instance ID is the string following the final ```::``` in the CRN, ```7mnxxxo8-91xx-23px-q4rs-xxtuv5w6xxx7```. 
    
    4. List the available keys and their associated CRNs within your desired {{site.data.keyword.keymanagementserviceshort}} service instance by running the following command:
       ```
       ibmcloud kp list -c --instance-id 7mnxxxo8-91xx-23px-q4rs-xxtuv5w6xxx7
       ```
       {: pre}
       
       where _7mnxxxo8-91xx-23px-q4rs-xxtuv5w6xxx7_ is the instance ID of your desired {{site.data.keyword.keymanagementserviceshort}} service instance.
       
       For this example, you'd see a response similar to the following output:
       ```
       Retrieving keys...
              
       SUCCESS
               
       Key ID                                 Key Name               CRN   
       ef1gxxxh-ijxx-234x-56k7-xxxxlmnoxxp8   test-key               crn:v1:bluemix:public:
       kms:us-south:a/abxx1c2xxxx34x567xxdex891xxx23fx:xxx4g5xx-6789-x1h2-ixxx-3jkl4xxxx567:
       key:ef1gxxxh-ijxx-234x-56k7-xxxxlmnoxxp8   
       cdex12ef-xxxg-3hxx-i456-7xxx8jk9xl12   vsi_encrypt_root_key   crn:v1:bluemix:public:
       kms:us-south:a/abxx1c2xxxx34x567xxdex891xxx23fx:xxx4g5xx-6789-x1h2-ixxx-3jkl4xxxx567:
       key:cdex12ef-xxxg-3hxx-i456-7xxx8jk9xl12   
       c12xxxx3-45d6-7efg-xxx8-9xxx12345x6h   vsi_encrypt_key        crn:v1:bluemix:public:
       kms:us-south:a/abxx1c2xxxx34x567xxdex891xxx23fx:xxx4g5xx-6789-x1h2-ixxx-3jkl4xxxx567:
       key:c12xxxx3-45d6-7efg-xxx8-9xxx12345x6h   
       ```
       {:screen}
       
2. Use the [ibmcloud is instance-create](/docs/infrastructure-service-cli-plugin?topic=infrastructure-service-cli-vpc-reference#instance-create) command and attach the necessary JSON files that specify customer managed encryption for the boot disk and any secondary data volumes that you want to include. The ```encryption_key``` parameter must include a valid CRN for the root key in the Key Protect service. See the following JSON file examples of a boot volume JSON and secondary volume JSON. 
3. Complete virtual server provisioning with your encrypted volumes. For more information, see [Creating virtual server instances (CLI)](/docs/vsi-is?topic=virtual-servers-is-creating-virtual-servers-cli#creating-virtual-servers-cli).

#### Example boot volume JSON file
{: #boot-volume-byok-json}

```
{  
   "name":"volume-attachment-1",
   "volume":{  
      "name":"volume-1",
      "capacity":100,
      "profile":{  
         "name":"general-purpose"
      },
      "encryption_key":{  
         "crn":"crn:v1:bluemix:public:kms:us-south:a/abxx1c2xxxx34x567xxdex891xxx23fx:
         xxx4g5xx-6789-x1h2-ixxx-3jkl4xxxx567:key:cdex12ef-xxxg-3hxx-i456-7xxx8jk9xl12"
      }
   },
   "delete_volume_on_instance_delete":true
}
```
{:codeblock}

#### Example secondary volume JSON file
{: #secondary-volume-byok-json}

```
[  
   {  
      "name":"volume-attachment-2",
      "volume":{  
         "name":"volume-2",
         "capacity":200,
         "profile":{  
            "name":"general-purpose"
         },
         "encryption_key":{  
            "crn":"crn:v1:bluemix:public:kms:us-south:a/abxx1c2xxxx34x567xxdex891xxx23fx:
            xxx4g5xx-6789-x1h2-ixxx-3jkl4xxxx567:key:c12xxxx3-45d6-7efg-xxx8-9xxx12345x6h"
         }
      }
   }
]
```
{:codeblock}

