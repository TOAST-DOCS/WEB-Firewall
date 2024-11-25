## Security > WEB Firewall > Console Usage Guide > Self > PIOLINK (WEBFRONT-KS)

Web Firewall Self service provides guides to create and operate web firewall instances to help protect web servers. 
This document introduces how to use the Web Firewall Self service.

To use the Web Firewall service, log in to **NHN Cloud Console**, and activate the service by clicking **Security > Web Firewall** in the service list.

![webfirewall_public_en_console-guide-self-piolink_01_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_01_241122.png)
<br><br>

## Use and Cancel a Service
### Create Web Firewall

![webfirewall_public_en_console-guide-self-piolink_02_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_02_241122.png)
![webfirewall_public_en_console-guide-self-piolink_03_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_03_241122.png)

1. Click the **Go button** in the Apply to **Self section** of the **Web Firewall** to navigate to the Compute > Instance page.
2. Click **+ Create Instance**, select PENTA WAF from the image list, and enter the instance information. For detailed instructions, **please refer to the Detailed Procedure for Creating a Web Firewall Instance below.**

> [note]
> * Service fee will be charged as soon as the instance is created.

### Cancel a Service

![webfirewall_public_en_console-guide-self-piolink_04_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_04_241122.png)

1. Select the Web Firewall instance from the instance list.
2. Delete the instance by clicking the '...' button and selecting **'Delete Instance'**.

> [Caution]
> * When configuring a web firewall, traffic goes through the web firewall, and service failure may occur if the instance is deleted while in use.
> * Ensure associated services are carefully reviewed before deleting a Web Firewall instance.

## Detailed Procedure for Creating a Web Firewall Instance
This guide provides detailed procedures to reference when creating a web firewall instance.
<br>

### 1. Image
![webfirewall_public_en_console-guide-self-piolink_05_241122.png](https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_05_241122.png)
1. Select the **'PLOS WAF'** image from the public image list.

<br>

### 2. Instance Information
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_06_241122.png" width="1200" />

1. Availability Zone: Configure the availability zone where the web firewall instance will be located. For more details on availability zones, refer to [the availability zone section in the instance overview.](https://docs.nhncloud.com/en/Compute/Instance/en/overview/#availability-zone)<br>
2. Instance Name: Configure the instance Name.<br>
3. Flavor: Configure the virtual hardware performance. Set the instance type by referring to the recommended specifications table for the web firewall below.<br>
4. Number of Instances: Set the number of instances to be created.<br>
5. Key Pair: Configure the key pair used for SSH access to the instance. You can either use an existing key pair or create a new one.<br>

| Throughput (Mbps) | Instance type | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | r2.c2m8 | 2 | 8 | 
| 500 | m2.c4m8 | 4 | 8 |
| 1,000 | m2.c8m16 | 8 | 16 |

<p align="center">[Talbe 1. Web Firewall(WEBFRONT-KS) Recommended Instance Type]</p>

### 3. Root Block Storage
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_07_241122.png" width="1200" />

1. Block Storage Type: You can select HDD, SSD, Encrypted HDD, and Encrypted SSD. For information on Encrypted HDD/SSD, refer to [the encrypted block storage section.](https://docs.nhncloud.com/en/Storage/Block%20Storage/en/console-guide/#_2)<br>
2. Block Storage Size(GB): Configure the capacity of the root block storage.

### 4. Network Settings
<img src="https://static.toastoven.net/prod_web_firewall/Piolink/public/en/webfirewall_public_en_console-guide-self-piolink_08_241122.png" width="1200" />

1. Network Interface Settings
   * Create network interface: It is a method where the interface is automatically created in the selected subnet.
   * Specify existing network interface: This method involves selecting an already created interface. The settings for '2. Network' and '3. Floating IP' are omitted, as they follow the configuration of the existing interface.
2. Network: Select the subnet from the ones defined in the VPC to connect to the instance. PENTA WAF does not support additional interface configurations.
3. Floating IP: Specify whether to use a floating IP after the instance is created. At this time, the VPC to which the web firewall instance belongs must be connected to an internet gateway. Even if not configured now, it can be set later in 'Instance > Floating IP Management' or 'Network Interface > Floating IP Management', Etc.
4. Security Group: Select the security group to apply to the web firewall instance. Refer to the example settings below for guidance on configuring the security group.

<br>

| Direction | IP Protocol | Port | Remote(CIDR) | Description |
| :-------: | :-----: | :---: | :---: | :--- |
| In | TCP | 80 (HTTP) | 0.0.0.0/0 | WAF Web Service Port |
| In | TCP | 443 (HTTPS) | 0.0.0.0/0 | WAF Web Service Port |
| In | TCP | 8443 | Admin IP | WAF Management Console(UI) Port(Allow Only Admin IP) |
| In | TCP | 22 (SSH) | Admin IP | WAF SSH Terminal Port(Allow Only Admin IP) |
| Out | ICMP | - | 0.0.0.0/0 | Communication for health check between the web firewall and web server |
| *Out | ALL | - | 0.0.0.0/0 | Communication with external servers for purposes such as external licenses, signature updates, etc. of the WAF |

<p align="center">[Table 2. Security Group Configuration Example]</p>

> [note]
> * Web firewall's default health check method is set to ICMP, and web service does not work when the web server and health check fail.
> * It is recommended to allow all outbound communication for the WAF *outbound rules as shown in [Table 2. Security Group Configuration Example].

## Initial Setup for Web Firewall

* Refer to Web Firewall Initial Setup Guide to proceed with initial setup, which includes the following information.
 * Set up application.
 * From Load Balancing menu, set up the actual server to be protected.
 * Enable Source NAT feature to make it work as proxy.
 * Do test access to Web Firewall IP to verify whether or not the Web service is normal.
 * Save and back up settings.

[WEBFRONT-KS_KR_Initial-Setup-Guide.pdf](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_KR_Initial-Setup-Guide.pdf)
* After initial setup is complete, DNS needs to be changed to Web Firewall Floating IP so that protected domain traffic passes through the Web Firewall. 
* You should update Web Firewall PLOS version to the latest, referring to the release notes provided by the manufacturer. 
 * How to download release notes: Web Firewall Access > SYSTEM > General Settings > PLOS Management > Download PLOS > Download

## Operate Web Firewall

* Operate the equipment by referring to web firewall configuration manual, which includes the following information.
 * Enable security policy you want to use.
 * Use learning feature to optimize policy such as handling exclusions.
 * Monitor security logs.

[WEBFRONT-KS_KR_Application-Configuration-Guide.pdf](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_KR_Application-Configuration-Guide.pdf) <br>
[WEBFRONT-KS_KR_System-Configuration-Guide.pdf](https://static.toastoven.net/prod_web_firewall/Piolink/Manual/WEBFRONT-KS_KR_System-Configuration-Guide.pdf) <br>

> [note]
> * Self-service only provides user guide and Managed Services provides operating agency service and 24-hour security control services. 
