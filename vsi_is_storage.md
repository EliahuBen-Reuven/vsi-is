---

copyright:
  years: 2018, 2019
lastupdated: "2018-11-01"

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

Secondary block storage data volumes and portable storage are not supported.
