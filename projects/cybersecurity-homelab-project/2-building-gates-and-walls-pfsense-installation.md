---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 2 - Building gates and walls: pfSense installation

pfSense is an open-source firewall and router software distribution that provides a powerful and flexible platform for network security. It offers features such as traffic filtering, VPN support, load balancing, and more. It can be installed on physical hardware or used as a virtual machine, making it an excellent choice for home labs like ours.

### Download pfSense

Go to [pfSense Download link](https://atxfiles.netgate.com/mirror/downloads/) and download the **am64** version ISO of the latest version available. In my case, latest version available is 2.7.2.

<figure><img src="../../.gitbook/assets/image (25).png" alt="" width="481"><figcaption></figcaption></figure>

Use a decompression tool to extract the ISO file.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### Create the VM

I will use VirtualBox to create the VM that will run the pfSense service. Launch VirtualBox and click on New in the toolbar.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Give a name to the VM and using the folder option choose where do you want to save it, I recommend to create a directory just for storing all the elements of this project, take into account that, by the end of the project, near 200GB of space will be consumed.

For the ISO Image I will use the downloaded .iso file. **Type** will be **BSD** and **Version** will be **FreeBSD (64-bit)** option. Click Next.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

For the amount of RAM and CPU I will keep the default configuration. Click Next.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

Lastly, I will set **20GB** as Disk Size value. Leave the other options untouched. Click Next.

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

Verify that the configuration is complete. Click Finish.

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

#### Optional: Create a VM group for the project

I recommend creating a VM machine group to have everything tidy and sorted.

For doing this, right-click on the VM and select **Move to Group > \[New]**.&#x20;

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

Now right-click on the New group and click Rename Group.

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

You can also create subgroups inside the main one, so you can divide the components by type or function if you want.

### Configure pfSense VM

We need to make a few fast changes. Click on **Settings**.

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

#### System Configuration

First, select **System > Motherboard** and, in the **Boot Order** section, place the **Hard Disk** option as first, followed by **Optical** and uncheck **Floppy**.

<figure><img src="../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

#### Deactivating Audio and USB

Go to the **Audio** section and uncheck the **Enable Audio** option. Since the VM purpose is to act as a router we don't need audio.

<figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

Make the same change in the **USB** section, uncheck **Enable USB Controller**, we will not need USB support.

<figure><img src="../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

#### Network configuration

Select the **Network** section in the left menu of the Settings tab.

<figure><img src="../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

Here, we are going to configure four virtual network adapters that emulate the physical devices. Each VirtualBox VM can use up to eight virtual network adapters, however just four virtual network adapters can be configured in the VirtualBox GUI (graphical user interface).

More information plus configuration explanations can be found in this [link](https://www.nakivo.com/blog/virtualbox-network-setting-guide/).

Let's go for the **Adapter 1**. For **Attached to** field choose **NAT**, then expand the **Advanced** section and choose **Paravirtualized Network (virtio-net)** as the **Adapter Type**.

<figure><img src="../../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

For **Adapter 2**, check the **Enable Network Adapter** box. Select **Internal Network** for the **Attached to** field. As Name, write **LAN 0**. In the **Advanced** section, choose **Paravirtualized Network (virtio-net)** as the **Adapter Type**.

<figure><img src="../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

For **Adapter 3**, repeat the same configuration, except for the **Name**, in this case we will use **LAN 1**.

<figure><img src="../../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

Last but not least, configure the **Adapter 4** in the same way, but name it **LAN 2**.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

### Installing pfSense

Let's start the VM that we created. Select your VM and click on the **Start** button.

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

A screen with psSense name will appear followed with a lot of text, wait until you see this screen and prees **Enter** to Accept the copyright agreement.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

In the next screen, press again **Enter** to start the installation.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Press again **Enter** to select the **Auto (ZFS)** partition option.

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

In the next screen, use **Enter** again to select **Proceed with Installation**.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Press **Enter** again to select the first option: **Stripe - No Redundancy**.

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

In the next screen press one time **Spacebar** key to check the **asa0** hard drive option (a \* will appear), then press **Enter** to continue.

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

With the **left arrow** move to **YES** and press **Enter** to continue.

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Wait for the installation to complete and then press **Enter** to reboot the VM.

<figure><img src="../../.gitbook/assets/image (35).png" alt="" width="540"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (36).png" alt="" width="540"><figcaption></figcaption></figure>

### Configuring pfSense

When the machine reboots we are going to onboard the network adapters that we configured before in the virtual machine settings. This screen will appear first, wait until the countdown finishes and the autoboot starts.

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

First we will answer to the question: "_Should VLANs be set up now?_" Type `n` and press **Enter**, we will configure the interfaces manually.

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Now give the following answers to the next **five** questions to configure the WAN interface, after typing each answer press **Enter** to advance to the next question.

```
Enter the WAN interface name: vtnet0
Enter the LAN interface name: vtnet1
Enter the Optional 1 interface name: vtnet2
Enter the Optional 2 interface name: vtnet3
Do you want to proceed?: y
```

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

We are going to assign static IPv4 addresses to the **LAN**, **OPT1** and **OPT2** interfaces, so they do not change their IP addresses on boot.

#### Configure the LAN (vtnet1)

Now, you will see this screen. The WAN is configured, next one is the LAN, type `2` to select the option **Set interface(s) IP address** and press **Enter**.

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Enter `2` again to select the **LAN** interface and answer the following three questions like this:

```
Configure IPv4 address LAN interface via DHCP?: n
Enter the new LAN IPv4 address: 10.0.0.1
Enter the new LAN IPv4 subnet bit count: 24
```

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

For the next question directly press **Enter** without typing anything.

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Then, answer the following six questions like this:

```
Configure IPv6 address LAN interface via DHCP6: n
For the new LAN IPv6 address question press Enter
Do you want to enable the DHCP server on LAN?: y
Enter the start address of the IPv4 client address range: 10.0.0.11
Enter the end address of the IPv4 client address range: 10.0.0.243
Do you want to revert to HTTP as the webConfigurator protocol?: n
```

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

Press **Enter** and the **LAN** interface configuration will be done.

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

Now we will see our changes applied to the LAN in the main menu.

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

#### Configure the OPT1 (vtnet2)

Enter `2` in the main menu to select **Set interface(s) IP address**. Then, enter `3` to select the **OPT1** interface. Answer the next three questions like this:

```
Configure IPv4 address OPT1 interface via DHCP?: n
Enter the new OPT1 IPv4 address: 10.6.6.1
Enter the new OPT1 IPv4 subnet bit count: 24
```

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Same as before, for the next question directly press **Enter**.

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

Now answer the next six questions like this:

```
Configure IPv6 address OPT1 interface via DHCP6: n
For the new OPT1 IPv6 address question press Enter
Do you want to enable the DHCP server on OPT1?: y
Enter the start address of the IPv4 client address range: 10.6.6.11
Enter the end address of the IPv4 client address range: 10.6.6.243
Do you want to revert to HTTP as the webConfigurator protocol?: n
```

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Press **Enter** to save changes and you will return to the main menu.

#### Configure the OPT2 (vtnet3)

As we have done before, enter `2` to select **Set interface(s) IP address**. And now enter `4` to select the remaining interface, **OPT2**. Answer the three next questions following these:

```
Configure IPv4 address OPT2 interface via DHCP?: n
Enter the new OPT2 IPv4 address: 10.80.80.1
Enter the new OPT2 IPv4 subnet bit count: 24
```

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

For the next question press **Enter**, again we are not going to configure the upstream gateway.

Answer the last four questions like this:

```
Configure IPv6 address OPT2 interface via DHCP6: n
For the new OPT2 IPv6 address question press Enter
Do you want to enable the DHCP server on OPT2?: n
Do you want to revert to HTTP as the webConfigurator protocol?: n
```

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
OPT2 will be used to set up the Active Directory (AD) Lab, with the Domain Controller (DC) serving as the DHCP server. As the DC will handle DHCP, DHCP-based IP address assignment has been disabled for this interface in pfSense.
{% endhint %}

Press **Enter** to save the changes, it will take you to the main menu. Compare your IPs with mine, they should be the same:

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

All the interfeces are now successfully onboarded in pfSense. For future settings changes we will use the pfSense Web Interface, that will be accessible for all the **LAN** interfaces in our LAN.

### Shutdown pfSense <a href="#shutdown-pfsense" id="shutdown-pfsense"></a>

For shutting down pfSense we will choose the `6` option Halt system, type `y` when it asks for your confirmation and wait until it shuts down.

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
When we start the lab pfSense is the first VM that has to be booted. When we shut down the lab pfSense will be the last VM that is stopped.
{% endhint %}

### Post-Installation Cleanup

To be continued...
