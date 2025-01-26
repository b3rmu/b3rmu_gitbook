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

# X - Uncover what’s hidden: Splunk installation and setup

I will install Splunk on an Ubuntu VM. Splunk will be our SIEM, its basic functionality is to filter and analyze the logs that it will ingest from the various sources that I will configure in the following chapters. I will be using **Splunk Enterprise 9.4.0**, whose **free trial option** gives us 60 days of free use.

### Download of Ubuntu image

Ubuntu is a powerful, free and versatile operating system, which makes it perfect for use in this project. The first thing to do is to download the image from the official site: [Ubuntu download](https://ubuntu.com/download/desktop)

{% hint style="info" %}
What do I mean with “_image_”? No, it is not a picture of your cat, a .iso OS image is a file that contains the OS, we will load it into our VM and then install Ubuntu. [Explanation](https://stackoverflow.com/questions/62282399/what-is-an-os-image-and-vm-image-in-short-i-would-need-to-understand-in-more-v)
{% endhint %}

I will choose the latest LTS version (in my case 24.04.1), as you can see the file is close to 6 GB:

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

### Create and configure the VM

Open VirtualBox and click on New.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Give our VM a name and choose where do you want to store it. Then select the ISO image we downloaded and check the **Skip Unattended Installation** box. Click Next.

<figure><img src="../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

Set the Base Memory to **4096MB**, the Processors do not need to be increased. Click Next.

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Set the Hard Disk size to **100GB** and click Next.

<figure><img src="../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

Confirm the configuration by clicking **Finish**.

<figure><img src="../../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

Optionally, we can include the VM in the previously created group.

### VM setup

Let's configure our machine. To do this we select the VM and click on Settings in the toolbar.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

Go to System and there in the **motherboard tab** we will place Hard Disk as the first option in the Boot Order, followed by Optical and uncheck the Floppy option.

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

Click OK to save changes. The configuration is done! ✅

### Ubuntu installation

Start by booting our virtual machine, select it and click Start.

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

When these three options appear on the screen, press Enter to start the installer.

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

We wait a little and select our language. Click on Next.

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>

Proceed to the next screen, where you can choose the keyboard you want to use. In my case default English (US) keyboard will work.

<figure><img src="../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

We do not modify anything in this screen. Click on Next.

<figure><img src="../../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure>

Select Install Ubuntu.

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

Click on Interactive installation. Click on Next.

<figure><img src="../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

Choose Default selection, click Next.

<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

Check “Install third-party software for graphics and Wi-Fi hardware” box. Click on Next.

<figure><img src="../../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>













