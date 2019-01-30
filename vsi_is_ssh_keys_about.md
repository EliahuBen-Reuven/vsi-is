---

copyright:
  years: 2018, 2019
lastupdated: "2018-11-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}

# SSH keys
{: #ssh-keys}

SSH keys are used by servers to identify a user or device through public-key cryptography. SSH keys are made up of an alpha-numeric combination and are unique to the device to which they are assigned. You can add, edit, or delete SSH keys by using the {{site.data.keyword.cloud}} console.
{:shortdesc}

SSH keys allow access to a device without using a password from corresponding clients for each public key that is implemented on the device. By adding an SSH key to a device, which can be done during provisioning, the device that was provided with the SSH key accesses the device for the corresponding key without the use of a password.

Logging in to your device with a password isn't supported.
{:note}

## Locating or generating your SSH key
You must have your SSH key available. To locate your SSH key or generate an SSH key, complete one of the following steps.

 * Locate an SSH key: Look for a file called `id_rsa.pub` under an `.ssh` directory under your home directory, for example, `/Users/<USERNAME>/.ssh/id_rsa.pub`. The file starts with `ssh-rsa` and ends with your email address.

* Generate an SSH key: If you do not have a public SSH key or if you forgot the password of an existing one, generate a new one by running the `ssh-keygen` command and following the prompts. For example, you can generate an SSH key on your Linux server by running the command `ssh-keygen -t rsa -C "user_ID"`. That command generates two files. The generated public key is in the `<your key>.pub` file.

For more information about creating, editing, or deleting SSH keys, see [Managing SSH keys](vsi_is_ssh_keys.html).
