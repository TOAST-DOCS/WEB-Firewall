## Security > WEB Firewall > Console Guide > Self-Service

The WEB Firewall Self-Service provides guides to create and operate  WEB Firewall instances for the protection of web servers. 
This document shows how to use the WEB Firewall Self-Service. 

To enable WEB Firewall, login to **NHN Cloud Console** and click **Security > WEB Firewall** on the service list. 

## Service Application and Release 

![webfirewall_console_guide_self_en_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_en_210625.png)

### Create WEB Firewall 

1. Go to **WEB Firewall** and **Pricing**, and click **Direct Link** for **Self-Service** to create instances. 
2. Click **+Create Instances** and select PLOS WAF on the list and enter instance information. For more details, see **Details for Creating WEB Firewall Instances** as below. 

※ Prices are charged immediately after an instance is created. 

### Release 

Select and delete WEB Firewall instances. 

※ Since traffic goes through WEB Firewall , while it is configured, deleting an instance during service may cause service failure. 
※ Check if your web service is in service before deleting an instance. 

## Creating WEB Firewall Instances 

![webfirewall_console_guide_self_1_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_1_210625.png)

※ Security groups are set as below for reliable IPs and ports, like below.  

| Direction | IP Protocol | Port Range | Remote | Description |
| :-------: | :-----: | :---: | :---: | :--- |
| Ingress | TCP | 80 (HTTP) | 0.0.0.0/0 (CIDR) | Web service port |
| Ingress | TCP | 443 (HTTPS) | 0.0.0.0/0 (CIDR) | Web service port |
| Ingress | TCP | 8443 | x.x.x.x/32 (CIDR) | WEB Firewall management port <br />(allows manager IP only) |
| Ingress | TCP | 22 (SSH) | x.x.x.x/32 (CIDR) | WEB Firewall terminal port<br />(allows manger IP only) |
| Ingress | ICMP | - | 192.168.0.0/24 (CIDR) | Health check communication between WEB Firewall and web servers |

※ Health checks for WEB Firewall are based on ICMP, and if health check fails for web servers, the web service does not operate.    

## Initial Setting 

Follow the guide for WEB Firewall initial setting, including the following: 

* Set the application; 
* Set the server to be protected, from load balancing menu; 
* Enable Source NAT to run in the proxy mode;
* Test the access to WEB Firewall IP to see if the web service works properly. 
* Save and back up the setting. 

[Guide for WEBFRONT-KS Initial Settings](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_초기%20설정%20가이드.pptx)
* After initial setting is completed, change your DNS setting to WEB Firewall floating IP, to lead the domain traffic you need to protect to go through WEB Traffic. 
* The PLOS of the web firewall must be updated to the latest version as specified in the release note provided by the manufacturer.
  * To download release note: Access firewall > SYSTEM > General Settings > Manage PLOS > Download PLOS > Download.

## Operations 

Read through the WEB Firewall configuration description to run equipment, including the following: 

* Enable the security policy to apply. 
* Make use of the learning technique to optimize policy, including exception handling.  
* Monitor security logs. 

[Description of WEBFRONT-KS Application Configuration](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_애플리케이션%20구성%20설명서.pdf)
[Description of WEBFRONT-KS System Configuration](http://static.toastoven.net/prod_web_firewall/WEBFRONT-KS_시스템%20구성%20설명서.pdf)

※ Self-Service provides User Guides only, while Managed Service supports with operations and around-the-clock security surveillance service.    
