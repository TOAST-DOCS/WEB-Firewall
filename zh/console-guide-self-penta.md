## Security > WEB Firewall > Console Usage Guide > Self > Penta Security (WAPPLES SA)

Web Firewall Self service provides guides to create and operate web firewall instances to help protect web servers. 
This document introduces how to use the Web Firewall Self service.

To use the Web Firewall service, log in to **NHN Cloud Console**, and activate the service by clicking **Security > Web Firewall** in the service list.

![webfirewall_public_en_console-guide-self-penta_01_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_01_241115.png)
<br><br>

## Use and Cancel a Service
### Create Web Firewall

![webfirewall_public_en_console-guide-self-penta_02_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_02_241115.png)
![webfirewall_public_en_console-guide-self-penta_03_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_03_241115.png)

1. Click the **Go button** in the Apply to **Self section** of the **Web Firewall** to navigate to the Compute > Instance page.
2. Click **+ Create Instance**, select PENTA WAF from the image list, and enter the instance information. For detailed instructions, **please refer to the Detailed Procedure for Creating a Web Firewall Instance below.**

> [note]
> * Service fee will be charged as soon as the instance is created.
> * The minimum recommended instance specifications for WAPPLE SA (PENTA WAF) are 2 vCores / 4GB of memory. Using an instance with lower specifications than recommended may cause malfunctions. Therefore, **you must use an instance type that meets or exceeds these specifications.**

### Cancel a Service

![webfirewall_public_en_console-guide-self-penta_04_241115.png](https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_04_241115.png)

1. Select the Web Firewall instance from the instance list.
2. Delete the instance by clicking the '...' button and selecting **'Delete Instance'**.

> [Caution]
> * When configuring a web firewall, traffic goes through the web firewall, and service failure may occur if the instance is deleted while in use.
> * Ensure associated services are carefully reviewed before deleting a Web Firewall instance.

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
> * The minimum recommended specification is 2vCore/4GB, but make sure to use an instance type with a specification above the minimum specfication. **Otherwise, Web Firewall may not function properly.**

| Throughput (Mbps) | Instance type | vCPU | Memory(GB) |
| :-------: | :-----: | :---: | :---: |
| 100 | m2.c2m4 | 2 | 4 | 
| 300 | m2.c4m8 | 4 | 8 | 
| 700 | m2.c8m16 | 8 | 16 |
| 1,500 | m2.c16m32 | 16 | 32 |

<p align="center">[Talbe 1. Web Firewall(WAPPLES SA) Recommended Instance Type]</p>


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
| In | TCP | 5000 | IP of the LB located at the top of the WAF | Health Check Port of the LB located at the top of the WAF |
| In | TCP | 5984 | Security group of the WAF or WAF IP range | WAF policy synchronization<br><span style="color:#e11d21;">*Required for HA configuration</span> | 
| *Out | ALL | - | 0.0.0.0/0 | Communication with external servers for purposes such as external licenses, signature updates, etc. of the WAF<br>(When individual configuration is required, refer to [Table 3. WAF Outbound List]) |

<p align="center"> [Table 2. Security Group Configuration Example] </p>

> [note]
> * When configuring HA and using the configuration synchronization feature, allowing port 5984 between WAFs is additionally required.

<br>

It is recommended to allow all outbound communication for the WAF *outbound rules as shown in [Table 2. Security Group Configuration Example]. If specific outbound rules need to be allowed, refer to [Table 3. WAF Outbound List] below.

<br>

| Direction | IP Protocol | Port | Remote(CIDR) | Description |
| :-------: | :-----: | :---: | :---: | :--- |
| Out | TCP | 443 (HTTPS) | 218.145.29.166/32 | WAF License Update Server |
| Out | TCP | 443 (HTTPS) | 218.145.29.101/32 | WAF License Update Server |
| Out | TCP | 5001 | 218.145.29.168/32 | WAF Security Rule(Custom Rule) Update Server |
| Out | UDP | 123 | 218.145.29.166/32 | Penta Security Time Server (Changeable) |
| Out | UDP | 123 | 218.145.29.163/32 | Penta Security Time Server (changeable) |
| Out | UDP,TCP | 53 | 164.124.101.2/32 | DNS Server - LG U+ (changeable) |
| Out | UDP,TCP | 53 | 8.8.8.8/32 | DNS Server - Google (changeable) |
| *Out | TCP | 5984 | Security group of the WAF or WAF IP range | WAF policy synchronization<br><span style="color:#e11d21;">*Required for HA configuration</span> |

<p align="center">[Table 3. WAF Outbound List]</p>

> [Caution]
> * If the TCP 443 (HTTPS) policy for the protected server is not configured on the web firewall, access to the web firewall's management console (UI) is possible via TCP 443 (HTTPS). Therefore, the 'Inbound TCP 443' rule in the security group ACL should be allowed in the security group after configuring the TCP 443 setting for the protected server on the web firewall.

## Initial Setup for Web Firewall
### Initial Setup after WAF Initial Run
1. Access the Web Firewall's Management Console(UI) in a Browser (Chrome Recommended)
	* https://WAF IP:5001
	* Login Access information: Contact ct@pentasecurity.com
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_01_241115.png" width="1000" />
<br>

2. Configuration > System > Time Sync
	* Configure each time server
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_02_241115.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_03_241115.png" width="1000" />
<br>

3. Security Settings > Network Settings > Proxy IP
	* Enter network information from NHN Cloud Console (WAF IP, gateway, netmask)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_04_241115.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_05_241115.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_06_241115.png" width="1000" />
<br>

4. Configure WAF Protection Target Servers
	* Security Settings > Network Settings > Destination Server > Add Servers
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_07_241115.png" width="1000" /><br><br>

	* Register Destination Server
		* Single: It is used when connecting to the IP or port of the destination web server (or LB located at the bottom of the WAF, etc.) without the need to branch based on the web host name. (1:1 Matching)
		* Multiple: It is used when connecting to the IP or port of the destnation web server (or LB located at the bottom of the WAF, etc.) based on the configured web host name. (1:N Matching) <br><br>

		* Configure Single
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_08_241115.png" width="1000" /><br><br>
		* Configure Multiple
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_09_241115.png" width="1000" />
			<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_10_241115.png" width="1000" /><br><br>
	* Save and apply
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_11_241115.png" width="1000" /><br><br>

> [note]
> * If the WAF needs to provide HTTPS, you can proceed by adding a certificate under [Network Settings > SSL Profile > SSL Profile Settings], and then configure SSL settings when adding each destination web server.
> * For more details, please refer to the user manual located under the 'WEB Firewall Operation' section below.

5. Configure the Security Policy
	* Security Settings > Policy Settings > Add Policy (the Base Policy: Select '1. Detect Without Blocking')
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_12_241115.png" width="1000" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_13_241115.png" width="800" /><br><br>
	* Security Settings > Policy Settings > Add Website (Apply to New Policy)
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_14_241115.png" width="800" />
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_15_241115.png" width="1000" />
<br>

6. Configure X-Forwarded-For IP
	* Security Settings > Additional Policy Settings > X-Forwarded-For (Configure both 'Block & Detect')
		<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_16_241115.png" width="1000" /><br><br>

> [notes when applying WAF]
> * Network routing needs to be modified to apply the WAF service to the customer's infrastructure environment.
> * Depending on the customer's infrastructure configuration, updating the DNS to the WAF floating IP or the load balancer floating IP above the WAF may be necessary.

<br>

## Web Firewall Operation

* The comprehensive user manual and instructions for the web firewall are available in its Management Console (UI).
* Refer to the location of the user manual in the screen below for detailed instructions on operating the web firewall.
	<img src="https://static.toastoven.net/prod_web_firewall/Penta/public/en/webfirewall_public_en_console-guide-self-penta_WAF_17_241115.png" width="1000" /><br><br>

> [note]
> * In the 'Self' service, only the user guide is provided, while the 'Managed' service offers operation management and 24/7 security monitoring.
