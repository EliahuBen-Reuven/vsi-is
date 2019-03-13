---

copyright:
  years: 2018, 2019
lastupdated: "2018-11-07"

subcollection: virtual-servers-is

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Troubleshooting your Virtual Servers for VPC
{: #troubleshooting-your-virtual-servers-for-vpc}

If you experience difficulties with your {{site.data.keyword.vsi_is_full}} instances, review the following possible causes.

## Permissions not set up in IBM Cloud

Before you can create {{site.data.keyword.vsi_is_short}}, you need the correct permissions to be set up in {{site.data.keyword.cloud_notm}} console. If your permissions are not correct, you can create a server and it shows `Pending` status, which quickly turns into `Failed` status. Make sure that the master of the account assigns you the correct [permissions](/docs/infrastructure/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).

## Servers are all in Unknown status

Most likely you do not have adequate permissions to view the server status. Make sure that you have the correct [permissions](/docs/infrastructure/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).

The Unknown status also might be caused by an expired IMS token. Run `bx sl init` again and rebuild the `ims_subject` with the new token. Make sure that you are passing in the `X-Subject-Token:$ims_subject` parameter in the request header.

## Different instance ID is returned

**Problem:** I post a request to create an instance, and the returned instance ID is `bce0c60d-20ef-42d1-b282-4eabd0c7bdd6`. Then, I get the instance, but the instance ID is changed to `2409a6ac-518c-47ff-ac51-ee8783e98f9a`.

**Answer:** Now RIAS compute supports two kinds of ID: `RIAS UUID` and `GUID(softlayer globalIdentifier)`. When you create a server, it returns the `RIAS UUID`. After the instance receives the GUID from Softlayer, RIAS compute updates the instance ID to `GUID`. You can use either  `RIAS UUID`  or `GUID` to manage the instance.

## Error: 409 Conflict when creating an instance action

You can't create certain instance actions if the status of your instance is in conflict with another action. For example, if your instance status is `stopped`, and you try to create a `reboot` action, the system returns a 409 error.

| Status      | Action     | Conflict |
| ----------- | ---------- | -------- |
| Running     | start      | yes      |
| Stopped     | not start  | yes      |
| Not running | pause      | yes      |
| Not running | reboot     | yes      |
| Not paused  | resume     | yes      |
| Paused      | not resume | yes      |
