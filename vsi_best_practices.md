---

copyright:
  years: 2018, 2019
lastupdated: "2018-12-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Planning for instances

When you're planning to provision {{site.data.keyword.vsi_is_full}}, you might find this configuration checklist helpful to get the most out of your virtual server deployment.
{:shortdesc}

Before you get started, make sure you have [created an {{site.data.keyword.vpc_short}}](/docs/infrastructure/vpc/getting-started.html).
{:important}

## Planning for provisioning instances 
After you have an {{site.data.keyword.vpc_short}} available, consider the following before you provision your instance.

|        Considerations|
|-------------------|
|__ 1. Make sure your account has the required [user permissions](/docs/infrastructure/vpc/vpc-vsi-permissions.html). If you have authorization as an editor or admin on an {{site.data.keyword.vpc_short}} resource, then you also inherit authorization to create, delete, and modify virtual server instances within that virtual private cloud.|
|__ 2. Check your [account limits](/docs/vsi-is//docs/vsi/vsi_is_faq.html#concurrent) for concurrent instances. |
|__ 3. Make sure your [SSH key](/docs/vsi/vsi_is_ssh_keys_about.html) is available.
|__ 4. Determine what instance location to select.|
|__ 5. Consider the popular [profile options](/docs/vsi/vsi_is_profiles.html) of vCPU and RAM combinations for your workload. Profiles contain preconfigured instances that are ready to use in a matter of minutes. It's important to ensure your instances will have the necessary resources to keep your workloads and your environment up and running.|
|__ 6. Determine what operating system image you'll select for your instance. You can choose among the current stock [images](/docs/vsi/vsi_is_images.html). |
|__ 7. Decide what port speeds you need. Port speeds are allocated to the virtual server instance and not a specific network interface. The default port speed is 100 Mbps. This option can't be modified after you create the instance. Use the speed that best balances cost versus performance for your design.|
|__ 8. Make sure you have a unique name for the instance. If you have a method to naming virtual server instances, it's much easier to filter and search on them later. |

## Next steps
When you're ready to get started, see the following resources to create your instance:
* [Creating an instance using the {{site.data.keyword.cloud_notm}} console](/docs/vsi/vsi_is_create_instance.html)
* [Creating an instance using the CLI](/docs/vsi/vsi_is_create_instance_cli.html)
