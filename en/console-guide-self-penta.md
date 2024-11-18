## Security > WEB Firewall > Console Usage Guide > Self > Penta Security (WAPPLES SA)

WEB Firewall Self service provides guides to create and operate web firewall instances to help protect web servers. 
This document introduces how to use the WEB Firewall Self service.

To use the WEB Firewall service, log in to **NHN Cloud Console**, and activate the service by clicking **Security > WEB Firewall** in the service list.

![webfirewall_public_en_console-guide-self-penta_01_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_01_241115.png)
<br><br>

## Use and Cancel a Service
### Create WEB Firewall

![webfirewall_public_en_console-guide-self-penta_02_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_02_241115.png)
![webfirewall_public_en_console-guide-self-penta_03_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_03_241115.png)

1. Click the **Go button** in the Apply to **Self section** of the **WEB Firewall** to navigate to the Compute > Instance page.
2. Click **+ Create Instance**, select PENTA WAF from the image list, and enter the instance information. For detailed instructions, **please refer to the Detailed Procedure for Creating a Web Firewall Instance below.**

> [note]
> * Service fee will be charged as soon as the instance is created.
> * The minimum recommended instance specifications for WAPPLE SA (PENTA WAF) are 2 vCores / 4GB of memory. Using an instance with lower specifications than recommended may cause malfunctions. Therefore, **you must use an instance type that meets or exceeds these specifications.**

### Cancel a Service

![webfirewall_public_en_console-guide-self-penta_04_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_04_241115.png)

1. Select the WEB Firewall instance from the instance list.
2. Delete the instance by clicking the '...' button and selecting **'Delete Instance'**.

> [Caution]
> * When configuring a web firewall, traffic goes through the web firewall, and service failure may occur if the instance is deleted while in use.
> * Ensure associated services are carefully reviewed before deleting a WEB Firewall instance.

## Detailed Procedure for Creating a Web Firewall Instance
This guide provides detailed procedures to reference when creating a web firewall instance.
<br>

### 1. Image
![webfirewall_public_en_console-guide-self-penta_05_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_05_241115.png)
1. Select the **'PETNA WAF'** image from the public image list.

<br>

### 2. Instance Information
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_06_241115.png" width="1200" />

1. Availability Zone: Configure the availability zone where the web firewall instance will be located. For more details on availability zones, refer to [the availability zone section in the instance overview.](https://docs.nhncloud.com/en/Compute/Instance/en/overview/#availability-zone)<br>
2. Instance Name: Configure the instance Name.<br>
3. Flavor: Configure the virtual hardware performance. Set the instance type by referring to the recommended specifications table for the web firewall below.<br>
4. Number of Instances: Set the number of instances to be created.<br>
5. Key Pair: Configure the key pair used for SSH access to the instance. You can either use an existing key pair or create a new one.<br>

> [note]
> * The minimum recommended specification is 2vCore/4GB, but make sure to use an instance type with a specification above the minimum specfication. **Otherwise, WEB Firewall may not function properly.**

| Throughput (Mbps) | Instance type | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | m2.c4m8 | 4 | 8 | 
| 700 | m2.c8m16 | 8 | 16 |
| 1,500 | m2.c16m32 | 16 | 32 |

<p align="center">[Talbe 1. WEB Firewall(WAPPLES SA) Recommended Instance Type]</p>


### 3. Root Block Storage
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_07_241115.png" width="1200" />

1. Block Storage Type: You can select HDD, SSD, Encrypted HDD, and Encrypted SSD. For information on Encrypted HDD/SSD, refer to [the encrypted block storage section.](https://docs.nhncloud.com/en/Storage/Block%20Storage/en/console-guide/#_2)<br>
2. Block Storage Size(GB): Configure the capacity of the root block storage. the minimum capacity for PENTA WAF is 200GB.

### 4. Network Settings
<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_08_241115.png" width="1200" />

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
| In | TCP | 443 (HTTPS) | 0.0.0.0/0 | WAF Web Service Port<br><span style="color:#e11d21;">*Refer to the note below</span> |
| In | TCP | 5001 | Admin IP | WAF Management Console(UI) Port(Allow Only Admin IP) |
| In | TCP | 22 (SSH) | Admin IP | WAF SSH Terminal Port(Allow Only Admin IP) |
| In | TCP | 5000 | IP of the LB located at the top of the WAF | 상단 LB의 헬스체크(health check) 포트 |
| In | TCP | 5984 | Security group of the WAF or WAF IP range | WAF policy synchronization<br><span style="color:#e11d21;">*Required for HA configuration</span> | 
| *Out | ALL | - | 0.0.0.0/0 | Communication with external servers for purposes such as external licenses, signature updates, etc. of the WAF<br>(When individual configuration is required, refer to [Table 3. WAF Outbound List]) |

<p align="center"> [Table 2. Security Group Configuration Example] </p>



※ Set up a security group for trusted IPs and ports to use, as shown in the example below.

| Direction | IP Protocol | Port range | Remote | Description | 
| :-------: | :-----: | :---: | :---: | :--- | 
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | WAF web service port | 
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | WAF web service port | 
| Ingress | TCP | 5001 | x.x.x.x/32 (CIDR) | WAF management tool(UI) pot (Only allow administrator IP) | 
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | WAF SSH Terminal port (Only allow administrator IP) | 
| Ingress | TCP/HTTP | 5000 | IP of top LB of WAF<BR>x.x.x.x/32 (CIDR) | health check port between WAF(redundancy) and Top LB | 
| Egress | TCP | 443 (HTTPS) | 218.145.29.166/32 (CIDR) | WAF License Update server 
| Egress | TCP | 443 (HTTPS) | 218.145.29.101/32 (CIDR) | WAF License Update server | 
| Egress | TCP | 5001 | 218.145.29.168/32 (CIDR) | WAF Security rule(custom rule) Update server |

※ Note : When using WAF redundancy (when using the settings synchronization function) or Auto Scaling, ports 5984 and 6984 must be allowed between WAFs.

## Initial Settings for Web Firewall

* Initial setup after WAF initial run

1. Access Web Firewall Web Management Tool (UI) from a browser (chrome recommended)
    * https://WAF IP:5001
    * Login Access information : Contact ct@pentasecurity.com

2. Settings > System > Set time synchronization
    * Set up time servers Penta Server 1 & Penta Server 2 respectively

3. Network Settings > Proxy IP Settings
    * Enter network information checked in NHN console (WAF IP, gateway, netmask)

4. Set WAF Protection Targets
    * Network Settings > Setting up a protected server
    * Server mode: Select proxy and enter port
    * Enter web server IP (domain) and port (‘single’ or ‘multiple’ can be selected depending on infrastructure configuration)
    * Disable health check (only when entering web server domain)
    * Specify an SSL certificate if your WAF provides HTTPS services (requires pre-setup in the SSL Profile menu)

5. Set Protection Policy
    * Security Settings > Policy Settings > Add a new policy (default policy: Select 'Detect only and do not block')
    * Security Settings > Policy Settings > Add new website (apply to new policy)

7. Set X-Forwarded-For IP
    * Security Settings > Policy Additional Settings > X-Forwarded-For Settings (Both Block & Detect Settings)

* Notes when applying WAF
    * Change and configure network routing to apply WAF services to customer infrastructure environments through NHN Cloud Managed Service Provider (MSP).
    * Depending on the customer infrastructure configuration, DNS changes to WAF floating IP may be required or DNS changes to top load balancer IP may be required when configuring WAF redundancy.

## Operate Web Firewall

* Provide web firewall's overall user manual and how to use it in Web Firewall's Management Tools (UI).
* Refer to the location of user manual on the screen below for instructions on how to use web firewall in general. 
![wapples_manual.png](https://static.toastoven.net/prod_web_firewall/wapples_manual.png)

※ Self-service only provides the user guide and Managed Service provides operating agency service and 24-hour security control services.
