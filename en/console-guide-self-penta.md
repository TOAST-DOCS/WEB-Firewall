## Security > WEB Firewall > Console Usage Guide > Self > Penta Security (WAPPLES SA)

WEB Firewall Self service provides guides to create and operate web firewall instances to help protect web servers. 
This document introduces how to use the WEB Firewall Self service.

To use the WEB Firewall service, log in to **NHN Cloud Console** and click on **Security>WEB Firewall** in the service list.

## Apply for and Cancel a Service

![webfirewall\_console\_guide\_self\_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_220613.png)

### Create Web Firewall

1. On **WEB Firewall** console, click on **Shortcut** from **Apply for Self** to navigate to the Create Instance page.
2. Click on **\+ Create Instance** and select PENTA WAF from the image list and enter the instance information. Refer to ** Detailed Procedure to create Web Firewall Instance ** below for more information.

※ Service fee will be charged as soon as the instance is created.

### Disable Web Firewall

Select and delete a Web firewall instance.

※ When configuring a web firewall, traffic goes through the web firewall, and service failure may occur if the instance is deleted while in use.<BR>
※ Please delete instance after checking the web service you are using.

## Detailed Procedure to Create Web Firewall Instance

![webfirewall\_console\_guide\_self\_1\_210625.png](https://static.toastoven.net/prod_web_firewall/webfirewall_console_guide_self_penta_230904.png)

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
![wapples\_manual.png](https://static.toastoven.net/prod_web_firewall/wapples_manual.png)

※ Self-service only provides the user guide and Managed Service provides operating agency service and 24-hour security control services.
