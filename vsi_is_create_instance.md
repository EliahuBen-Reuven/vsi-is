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
{:important: .important}
{:table: .aria-labeledby="caption"}

# Creating virtual server instances
{: #creating-virtual-servers}

You can create {{site.data.keyword.vsi_is_full}} from the *Virtual server instances* page in {{site.data.keyword.cloud_notm}} console.
{:shortdesc}

Before you get started, make sure you have [created an IBM Cloud VPC](/docs/infrastructure/vpc/getting-started.html).
{:important}

To create an instance, select the following instance details.
1. In [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.cloud.ibm.com/vpc), navigate to **Menu icon ![Menu icon](../icons/icon_hamburger.svg) > VPC Infrastructure > Compute > Virtual server instances**.
2. Click **New instance** and enter the following information:

    <table>
    <CAPTION>Table 1. Instance provisioning selections</CAPTION>
    <THEAD>
    <TR>
    <th>Field</th>
    <th>Value</th>
    </TR>
    </THEAD>
    <TBODY>
    <tr>
    <td>Name </td>
    <td>A name is required for your virtual server instance.</td>
    </tr>
    <tr>
    <td>Virtual private cloud</td>
    <td>Specify the IBM Cloud VPC where you want to create your instance.</td>
    </tr>
    <tr>
    <td>Location</td>
    <td>Locations are composed of regions (specific geographic areas) and zones (fault tolerant data centers within a region). Select the location where you want your virtual server instance to be created.</td>
    </tr>
    <tr>
    <td>Profile</td>
    <td><p>
    Select from popular profiles or all available vCPU and RAM combinations. The following families are supported:
    <ul>
    <li>Balanced</li>
    <li>Compute</li>
    <li>Memory</li>
    </ul>
    </p>
    <p>Each physical core on the server is hyper-threaded and presented as two virtual CPUs (vCPUs). The virtual server offering provides 2.0 GHz or better per vCPU with up to 48 vCPU available on a single virtual server.</p>

    <p>For memory, an instance can have up to 256 GB of fully dedicated RAM.</p>
    <p><note>Note: Maximum values vary by family.</note></p>
    <p>For more information, see [Profiles](/docs/vsi/vsi_is_profiles.html).</p>
    </td>
    </tr>
    <tr>
    <td>Image</td>
    <td><p>All images use cloud-init, which allows you to enter user metadata associated with the instance for post provisioning scripts.</p>
    <p>For more information, see [Images](/docs/vsi/vsi_is_images.html).</p>
    </td>
    </tr>
    <td>SSH Key</td>
    <td>
    <p>You must select an existing SSH key or upload a new SSH key to use before you can create the instance. SSH keys are used to securely connect to the instance after it's running.</p>
    <p>Note: Alpha-numeric combinations are limited to 100 characters.</p>
    <p>For more information, see [SSH keys](/docs/vsi/vsi_is_ssh_keys_about.html).</p></td>
    </tr>
    <tr>
    <td>User data</td>
    <td>
    <p>You can add user data that automatically performs common configuration tasks or runs scripts. <p>For more information, see [User data](/docs/vsi/vsi_is_provisioning_scripts.html).</p>
    </td>
    </tr>
    <tr>
    <td>Boot volume</td>
    <td>The default boot volume size for all profiles is 100 GB. For more information, see [Storage](/docs/vsi/vsi_is_storage.html).</td>
    </tr>
    <tr>
    <td>Network interfaces</td>
    <td>Assign networking options to connect into the IBM Cloud VPC. You can create and assign up to 5 network interface cards to each instance. For more information, see [Multiple IP addresses](/docs/vsi/vsi_is_network_security_options.html).</td>
    </tr>
    </TBODY>
    </table>

    Your *Cost summary* displays on the right side of the *New virtual server instance* page.

3. Click **Create virtual server instance** when you are ready to provision.

Do you prefer to create an instance using the CLI? For more information, see [Creating an instance using the CLI](/docs/vsi/vsi_is_create_instance_cli.html).
{: tip}

## Next steps
A series of emails are sent to your administrator: acknowledgment of the virtual server instance order, order approval and processing, and a message stating the instance is created.

After the server is created, associate a floating IP address to the instance. Then you can connect to your instance. For more information, see [Connecting to your Linux instance](/docs/vsi/vsi_is_connecting_linux_gc.html) or [Connecting to your Windows instance](/docs/vsi/vsi_is_connecting_windows_gc.html).
