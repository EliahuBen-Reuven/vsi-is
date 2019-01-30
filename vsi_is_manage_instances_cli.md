---



copyright:
  years: 2018, 2019
lastupdated: "2018-01-21"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# Managing virtual server instances (CLI)
{: #managing-virtual-servers-cli}

You can view and manage your {{site.data.keyword.vsi_is_full}} instances by using the command line interface (CLI).
{:shortdesc}

## Before you begin
1. Ensure you have downloaded, installed, and initialized the following CLI plug-ins:
    * {{site.data.keyword.cloud_notm}} CLI
    * The infrastructure-service plugin

   For more information, see [IBM Cloud CLI for VPC Reference](/docs/infrastructure-service-cli-plugin/vpc-cli-reference.html).
2. Make sure you have already [created an {{site.data.keyword.vpc_short}}](/docs/infrastructure/vpc/getting-started.html).

## Viewing instance actions
To view the management actions that are performed on your instance, run the following command:

```
ibmcloud is instance-actions <server-ID>
```
{:codeblock}

You will see a list similar to the following output:

```
ID                                     Type     Status      Created       Started            Completed   
123xxxx4-123x-1234-56x7-80xx37xx1234   delete   Completed   6 hours ago   a long while ago   a long while ago         
```
{:screen}

## Managing your instances
Need a little help? Run the `ibmcloud is help` command to view commands at anytime.

Common management actions

|              Instance action          |  Command              |  What happens next           |
| ---------------------------------------| --------------------------|----------------------------- |
| Restart          |`ibmcloud is instance-reboot`   | The instance is immediately powered off and then powered back on again.      | 
| Stop / Start     | `ibmcloud is instance-start` or `ibmcloud is instance-stop`  | If the instance is stopped, the instance remains in the stopped state and must be started manually. Billing is [suspended](/docs/infrastructure/vpc/vpc-vsi-pricing.html#suspend-billing) for some compute resources while the instance is stopped. You cannot interact with an instance if it is stopped. If the device is started, normal interaction continues.    |
| Update          | `ibmcloud is instance-update`  | After you rename the device, the name automatically updates. |
| Delete         | `ibmcloud is instance-delete` | After you confirm the delete action, the process to delete the instance and its associated vNIC, boot volume, and data begins. The delete action can take up to 30 minutes, but when the process is complete, the instance no longer appears on the Virtual server instances page. The floating IP address that is associated to the virtual server instance is unassociated, but remains on your account.    |
{: caption="Table 1. Management actions for your instances" caption-side="top"}

If you prefer to manage instances by using the {{site.data.keyword.cloud}} console, see [Managing an instance](vsi_is_manage_instances.html).
{: tip}
