---

copyright:
  years: 2018, 2019
lastupdated: "2018-01-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:table: .aria-labeledby="caption"}

# Managing SSH keys
{: #managing-ssh-keys}

## Before you Begin
To access {{site.data.keyword.vsi_is_full}} instances, you must have an SSH key available to use. You can manage SSH keys in {{site.data.keyword.cloud_notm}} console and by using the CLI. 

For more information about locating or generating an SSH key, see [SSH Keys](/docs/vsi/vsi_is_ssh_keys_about.html).
{: tip}

## Managing SSH keys with IBM Cloud console

When you provision a virtual server, you can select from available SSH keys or upload a new one. You cannot generate SSH keys in the console.
{:shortdesc}

You can manage and delete SSH keys by using the {{site.data.keyword.cloud_notm}} console.
1. In [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.cloud.ibm.com/vpc), navigate to **Menu icon ![Menu icon](../icons/icon_hamburger.svg) > VPC Infrastructure > Compute > SSH keys**.
2. From here, you can add or delete an SSH Key.

## Managing SSH keys by using the CLI

You can also manage your SSH keys by using the CLI.

| Action           | Command                     | What happens next |
| ---------------- | --------------------------- | ----------------- |
| Create SSH key   | `ibmcloud is key-create`    | After you create an SSH key, it is added to the list of keys. |
| View key details | `ibmcloud is key`           | You can view the name of the key and the ID of the key. |
| List keys        | `ibmcloud is keys`          | You can view all of your existing SSH keys. |
| Update key       | `ibmcloud is key-update`    | After you update an existing key, the key is renamed immediately. |
| Delete key       | `ibmcloud is key-delete`    | After you remove an SSH key, it no longer exists. The key can no longer be used when you provision a new device or when you perform an OS reload on an existing device. When you delete a key, you can also no longer access existing provisions by using that key. |
{: caption="Table 1. SSH key actions" caption-side="top"}
