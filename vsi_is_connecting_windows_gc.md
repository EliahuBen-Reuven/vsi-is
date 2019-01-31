---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-31"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Connecting to your Windows instance

After you have created your {{site.data.keyword.vsi_is_full}} Windows instance, you can connect to it by completing these steps.
{:shortdesc}

## Before you begin

Make sure to complete the following prerequisites before you begin:

1. Ask your account administrator to grant you access to retrieve the password from your virtual server instance. For more information, review [user permissions](/docs/infrastructure/vpc/vpc-user-permissions.html).
2. Create a new security group or add a rule to the default security group to enable inbound access for the Remote Desktop default port, 3389. For more information, see [Using Security Groups in the VPC CLI and API](/docs/infrastructure/vpc-network/security-groups.html).
3. Ensure that inbound traffic over TCP/IP port 3389 is permitted on the VPC's default ACL. For more information, see [Using Network ACLs in the VPC CLI and API](/docs/infrastructure/vpc-network/using-acls.html).
4. Verify that you have OpenSSL installed. To successfully decrypt your password, you must run OpenSSL and not LibreSSL. For more information, see [OpenSSL Downloads ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.openssl.org/source/){: new_window}.

LibreSSL isn't compatible for the decryption of your password. You must run OpenSSL to decrypt your password.
{:important}

## Connecting to your Windows instance

After you create your Windows instance and complete the prerequisites, complete the following steps to connect to your Windows instance. 
  
1. Query the status of your instance by running the following command:
  ```
  $ ibmcloud is instance-status <instance id>
  ```
  {:codeblock}
  
  When the instance shows that it's `running`, you are ready to initialize the instance to get your password. 

2. Run the following command to initialize your instance:

  ```
  $ ibmcloud is instance-initialization <instance id>
  ```
  {:codeblock}
  
  After you run this command, you receive your encrypted password, which is automatically generated when you create an instance by using a Windows image.

3. You now need to decrypt your password through a manual decryption process. To decrypt your password, run the following command:

  ```
  # Decode the encrypted password
  cat ~/testpwd | base64 --decode > ~/testpwd64
  # Decrypt the decoded password using the RSA private key
  openssl pkeyutl -in testpwd64 -decrypt -inkey private.pem -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha256
  -pkeyopt rsa_mgf1_md:sha256
  ```
  {:codeblock}
  
  where `~/testpwd` is the file where you saved your encrypted password.

4. After you decrypt your password, you now need to associate a floating IP address to your Windows instance. Run the following command to associate a floating IP address to your instance:

  ```
  ibmcloud is fipc --nic <instance nic id>
  ```
  {:codeblock}

5. You now have what you need in order to connect to your Windows instance: decrypted password and floating IP address. Use your preferred Remote Desktop client to connect to your instance. To connect to your instance, provide the floating IP address and the decrypted password. The username is `Administrator` by default. 

## Next steps
After you are connected to your instance, you can [manage your instances by using the {{site.data.keyword.cloud_notm}} console](vsi_is_manage_instances.html) or [manage your instances by using the CLI](vsi_is_manage_instances_cli.html).



