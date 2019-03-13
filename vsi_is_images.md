---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-16"

subcollection: virtual-servers-is

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# Images
{: #images}

When you provision {{site.data.keyword.vsi_is_full}}, you can select from the supported stock images. The image that you select determines the operating system that is provisioned for your instance. Custom images aren't supported
currently.
{:shortdesc}

## Stock images
The following operating systems are available as stock images when you create a virtual server.
* CentOS 7.x
* Ubuntu 16.04, 18.04
* Debian 8.x, 9.x
* Windows 2016, 2012 R2, 2012

When you order an instance, the images are cloud-init enabled to optimize provisioning times. With a cloud-init enabled image, you can provide user data. In the **User Data** field on the order form, you can enter optional cloud-init user data for the server. For more information about user data and automation, see [User Data](/docs/vsi-is?topic=virtual-servers-is-user-data).

## Virtualization
Instances require an image that supports Hardware Virtualization Machine (HVM) boot mode. The HVM virtualization type allows an image to run directly on a virtual server, which is required for advanced networking and GPU capabilities.
