# Vulnerability analysis with NMap
## Sumary

Search for vulnerabilities with nmap in wordpress.


## Descritpion

Using a kali linux virtual machine, the objective is analyze a server with worpress for vulnerabilities using Nmap. [Nmap](https://nmap.org/) ("Network Mapper") is a free and open source ([license](https://nmap.org/data/COPYING)) utility for network discovery and security auditing. [WordPress](https://en.wikipedia.org/wiki/WordPress) is a free and open-source content management system(CMS) written in PHP4 and paired with a [MySQL](https://en.wikipedia.org/wiki/MySQL "MySQL") or [MariaDB](https://en.wikipedia.org/wiki/MariaDB "MariaDB") database.

## Steps to reproduce:

1. **Install Vm's**
- Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  6.1.14
- Download the [Kali Linux ova](https://images.kali.org/virtual-images/kali-linux-2020.3-vbox-amd64.ova) version 2020.3 for VirtualBox
- Download file .ova with [Wordpress](https://bitnami.com/redirect/to/1135601/bitnami-wordpress-5.5.1-0-linux-debian-10-x86_64.ova)
	- Kali
			- Open VirtualBox and select the option "import virtualized service" and select the file "kali-linux-2020.3-vbox-amd64.ova".
			- Import the VM.
			- Go to settings of this VM and select network. Enable two adapters; a NAT adapter, and a Bridged adapter, allowing promiscuous mode.
			- Start the virtual machine. User `kali` password `kali`
			- Use the command `sudo su` in a terminal to login into the root account. Password `kali`.
	
	- Wordpress
			- Open VirtualBox and select the option "import virtualized service" and select the file "bitnami-wordpress-5.5.1-0-linux-debian-10-x86_64.ova".
			- Import the VM.
			- Go to settings of this VM and select network. Enable two adapters; a NAT adapter, and a Bridged adapter, allowing promiscuous mode.
			- Start the virtual machine. User `bitnami` password `bitnami`.
			- The console will show the IP address to access the page.
- Disable firewalls and antivirus.
	
2. **non intrusive scan to scanme.nmap.org**
- In the terminal where you used the command "sudo su" use the command `nmap -O scanme.nmap.org` to get open ports, OS guesses, network distance and the ip address. 
- Use the command `nmap -sn --script broadcast-ping scanme.nmap.org` to check if this brodcast ping is enable.
- Use the command `locate *.nse` to check all supported Nmap scripts.

3. **Wordpress server tests**
- Use the command `nmap -sn [network]/24` where network is the bridge adapter network. This command gives you all hosts in the network.
- Use command `nmap -A -sV [network]/24`. This command gives you open ports, the service and the version.
- Use the command `nmap -O [network]/24`. This command gives you operating systems of hosts.
- Use the command `nmap --p3306 --script mysql-brute [IP]` (where IP is the IP Address of the WordPress server). This command make a MYSQL brute force attack.
- Use the command `nmap -sV -p330 [IP]`. This command look for insecure MYSQL settings.
- Use the command `nmap -sV --script http-wordpress-enum [IP]`. This command look for plugins installed in Wordpress.
- Use the command `nmap -sV --script http-wordpress-users [IP]`. This command look for the users in Wordpress.
- Use the command `nmap -sV --script http-wordpress-brute [IP]`. This command make a brute force attack on the users in Wordpress.

|IP| OS| Port | Services | Versions|Vulnerabilities (CVE)|Vulnerabilities (PT)|
|--|--|--|--|--|--|--|
| 192.168.0.36 | Linux 2.6.32 to 3.13 (95%) | 22/tcp closed 80/tcp open 443/tcp open | ssh - http - ssl| Apache httpd (PHP 7.4.9) | [CVE-2019-16223](https://www.cvedetails.com/cve/CVE-2019-16223/ "CVE-2019-16223 security vulnerability details") | XML-RPC enabled, external WP-Cron enabled. |


## References

- [VirtualBox 6.1.14](https://www.virtualbox.org/wiki/Downloads)
- [Nmap](nmap.org)
- [NSE Database](https://nmap.org/nsedoc/scripts/)  
- [WPScan guide](https://tools.kali.org/web-applications/wpscan) 
- [Wordpress vulnerabilities](https://www.cvedetails.com/vulnerability-list/vendor_id-2337/product_id-4096/year-2019/Wordpress-Wordpress.html)
- [ova Kali](https://images.kali.org/virtual-images/kali-linux-2020.3-vbox-amd64.ova)
- [ova WordPress](https://bitnami.com/redirect/to/1135601/bitnami-wordpress-5.5.1-0-linux-debian-10-x86_64.ova)



