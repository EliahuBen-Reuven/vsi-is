---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-16"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}

# Networking and security on virtual servers
{: #network-security-options}

When implementing {{site.data.keyword.vsi_is_full}}, you have access to the latest features for networking and security.  
{:shortdesc}

## Using instance vNICs
A virtual network interface card (vNIC) is used to connect a virtual server to a network. When you create a VSI instance, you can use a vNIC to assign multiple IP addresses. The following list highlights how vNICs work with your instance.

* You can create and assign up to 5 vNICs to each instance. Each vNIC will be assigned a private IP from the connected subnet and you can optionally attach a floating IP and security groups.
* You can attach each vNIC to a subnet in the same zone.
* Each vNIC receives a private IP from the subnet range.
* You can associate and unassociate floating IPs to and from each vNIC.
* You can assign security groups to each vNIC.
* You can change the name of any existing vNIC.

Bandwidth is associated with the instance itself, and is not a configurable aspect of an individual vNIC. The default bandwidth for an instance is 100 Mbps, with an option to upgrade to 1 Gbps.

## Networking options

For more information about overall networking features in the {{site.data.keyword.vpc_short}} environment, see [About Networking for VPC](/docs/infrastructure/vpc-network/about-network.html).

## Security options

{{site.data.keyword.vsi_is_short}} includes built-in security options:
* Access Control Lists (ACLs) can limit traffic to and from a subnet.
* Security groups function as a virtual firewall for virtual server instances.
* SSH keys on your virtual server instance authenticate a secure channel for network communication.

For more information about these security options, see [Security in your IBM Cloud VPC](/docs/infrastructure/vpc-network/vpc-security.html) and [Managing SSH keys](/docs/vsi/vsi_is_ssh_keys.html).
