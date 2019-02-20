---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# Storage

After you provision an {{site.data.keyword.vsi_is_full}} instance, a 100 GB block storage volume is 
automatically created as a primary boot volume and attached to the instance.
{:shortdesc}

The boot volume provides 3 IOPS/GB performance and exists within the virtual server instance lifecycle.  When you delete the instance, 
the boot volume is also deleted.

## Customer managed encryption for block storage  
{: #customer-managed-encryption-keys}

You can create {{site.data.keyword.vsi_is_full}} with block storage encryption and your own data encryption keys that you manage. You just need the {{site.data.keyword.keymanagementservicelong_notm}} service and your own data encryption key to get started.
{:shortdesc}

### Prerequisites
{: #byok-vsi-prereqs}

To create a virtual server instance that uses customer managed encryption for the block storage volumes, you must have a service instance of {{site.data.keyword.keymanagementserviceshort}} that includes a customer root key. You must also authorize access between Cloud Block Storage and Key Protect. When you've completed these prerequisites, you can start creating instances that use customer managed encryption for the block storage volumes. 

1. Provision the [{{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect?topic=key-protect-provision#provision) service. 
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

1. Obtain the CRN of the root key in the {{site.data.keyword.iamshort}} service. From the **New virtual server for VPC** page in {{site.data.keyword.cloud_notm}} console, you can specify the customer managed encryption parameters that you want to use. Then, click **Create with REST API </>**. From the resulting code, you can copy the CRN for the root key in {{site.data.keyword.iamshort}}. The CRN is required for the ```encryption_key``` parameter in the JSON file.
2. Use the [ibmcloud is instance-create](/docs/infrastructure-service-cli-plugin?topic=infrastructure-service-cli-vpc-reference#instance-create) command and attach the necessary JSON files that specify customer managed encryption for the boot disk and any secondary data volumes that you want to include. The ```encryption_key``` parameter must include a valid CRN for the root key in the Key Protect service. See the following JSON file examples of a boot volume JSON and secondary volume JSON. 
3. For more information, see [Creating virtual server instances (CLI)](/docs/vsi-is?topic=virtual-servers-is-creating-virtual-servers-cli#creating-virtual-servers-cli).

#### Example boot volume JSON file
{: #boot-volume-byok-json}

```
{  
   "name":"<your unique name>",
   "volume":{  
      "name":"<your unique name>",
      "capacity":100,
      "profile":{  
         "name":""
      },
      "encryption_key":{  
         "crn":"crn:v1:bluemix:public:kms:us-south:a/12a3bc4def567g891h12i3jkl45m6n7o:p8912345-6q78-9123-4567-891r23st4u5:key:6789v123-4xyz-5678-ab91-23456cd78e9"
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
      "name":"<your unique name",
      "volume":{  
         "name":"<your unique name",
         "capacity":200,
         "profile":{  
            "name":"general-purpose"
         },
         "encryption_key":{  
            "crn":"crn:v1:bluemix:public:kms:us-south:a/12a3bc4def567g891h12i3jkl45m6n7o:p8912345-6q78-9123-4567-891r23st4u5:key:6789v123-4xyz-5678-ab91-23456cd78e9"
         }
      }
   }
]
```
{:codeblock}

