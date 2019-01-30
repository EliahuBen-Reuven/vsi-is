---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-28"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}

# Profiles
{: #profiles}

When you provision {{site.data.keyword.vsi_is_full}}, you can select from three families of profiles: Balanced, Compute, and Memory. A profile is a combination of vCPU and RAM that can be instantiated quickly to start a virtual server instance. In the {{site.data.keyword.Bluemix_notm}} console, you can choose from popular profile configurations or select from a list of profiles that best fit your needs.
{: shortdesc}

The following families are available:

| Families | Description |
| -------- | ----------- |
| [Balanced](vsi_is_profiles_balanced.html) | Best for common cloud workloads that require a balance of performance and scalability. The balanced profiles (with network-attached storage) provide higher performance, since resources are not oversubscribed. |
| [Compute](virtual-servers-is-compute.html)  | Best for moderate to high web traffic workloads. Compute profiles are best for workloads with intensive CPU demands, such as high web traffic workloads, production batch processing, and front-end web servers. |
| [Memory](virtual-servers-is-memory.html) | Best for memory caching and real-time analytics workloads. Memory profiles are best for memory intensive workloads, such as large caching workloads, intensive database applications, or in-memory analytics workloads. |
{: caption="Table 1. Virtual server family selections" caption-side="top"}

## Viewing profile configurations
{: #popularprofiles}

You can view available profile configurations using the {{site.data.keyword.cloud_notm}} console or the CLI. In the {{site.data.keyword.cloud_notm}} console, you can select from popular profile configurations that support most common use cases.

### Using the IBM Cloud console
1. In the {{site.data.keyword.cloud_notm}} console, navigate to **Menu icon ![Menu icon](../icons/icon_hamburger.svg) > VPC Infrastructure > Compute > Virtual server instances**.
2. From this page, click **New instance**.
3. You can either select a profile configuration from **Popular profiles** or click **All profiles** to view additional configurations.

### Using the CLI
To view the list of available profiles using the CLI, run the following command:
```
$ ibmcloud is instance-profiles
```
{:codeblock}

When using the command line, the following information describes what the output represents. The profile sizes have different ratios of CPU to memory, designed for different workloads:

*  "b" is balanced, which is a 1:2 or 1:4 ratio
*  "c" is compute (higher on the CPUs) , which is a 1:1 ratio
*  “m” is memory (higher on the memory), which is a 1:8 ratio
