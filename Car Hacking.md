
## Sumary
Car Hacking

Use virtual and real tools to attack a car.

## Descritpion

[Car Hacking](https://en.wikipedia.org/wiki/Automotive_hacking) is the exploitation of vulnerabilities within the software, hardware, and communication systems of automobiles. In this practice the target is attack the virtual can network and a can network of a vehicle, and carry out an attack with radio signals.

## Steps to reproduce:


1. **Install Vm's**
- Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  6.1.14
- Download the [Kali Linux ova](https://images.kali.org/virtual-images/kali-linux-2020.3-vbox-amd64.ova) version 2020.3 for VirtualBox
	- Kali
			- Open VirtualBox and select the option "import virtualized service" and select the file "kali-linux-2020.3-vbox-amd64.ova".
			- Import the VM.
			- Go to settings of this VM and select network. Enable two adapters; a NAT adapter, and a Bridged adapter, allowing promiscuous mode.
			- Start the virtual machine. User `kali` password `kali`
			- Use the command `sudo su` in a terminal to login into the root account. Password `kali`.

2. **Analyze and replicate the traffic on the CAN network of a simulated device.**

- In the terminal where you used the command "sudo su" use the command `apt-get install can-utils` to install can-utils.
- Setup Virtual CAN
  - `modprobe vcan`
- Verify Virtual CAN module is installed
  - `modprobe vcanmodprobe -c | grep vcan`
- Create a new network vcan interface using "ip" command
  - `ip link add dev vcan0 type vcan`
 - List the new interface
   - `ip -h link show`
 - Turn on the newly created network interface
   - `ip link set up vcan0`
 - List the differences after setting it up
   - `ip -h link show`
  - Test Virtual CAN communication using can-utils
  - On one linux terminal run the candump can on vcan0
    - `candump vcan0` 
  - From another linux terminal window, send a CAN frame with identifier 0x1A
    - `cansend vcan0 01a#11223344AABBCCDD` 
  - Verify this data appears on the former terminal window "vcan0 01A [8] 11 22 33 44 AA BB CC DD"
  - Stop candump on the first terminal typing Ctrl + C
  - Restart the candump util again
    - `candump vcan0` 
  - From another linux terminal window, send random CAN frames
    - `cangen vcan0` 
 - Stop both terminals typing Ctrl + C
 - Install Instrument Cluster Simulator
    - `sudo apt-get install libsdl2-dev libsdl2-image-dev` 
  - Clone ICSim repository
    - `git clone https://github.com/zombieCraig/ICSim.git` 
    - `cd ICSim` 
    - `make`
  - Start the simulator
    - `./icsim vcan0` 
  - Start the controls on a different Linux terminal window
    - `./controls vcan0` 

 - Install Docker using this [tutorial](https://medium.com/@calypso_bronte/installing-docker-in-kali-linux-2018-1-ef3a8ce3648).
 - Install the Docker version of CANalyzat0r using this [tutorial](https://github.com/schutzwerk/CANalyzat0r/tree/master/docker).

  - Clone CANalyzat0r from https://github.com/schutzwerk/CANalyzat0r on a different Linux terminal window
    - `git clone https://github.com/schutzwerk/CANalyzat0r` 
    - `cd CANalyzat0r/docker`
    - `make build & make run`

- See packet traffic in "Sniffer"
- Go to "Filter" and change the capture time to 10 seconds.
- To identify the packages we need, look for the most repeated id
- Copy the chosen package and paste it in "Sender" and click on "send all"


3. **Analyze and replicate the traffic of a CAN network in a real car.**
-   Set up the CAN interface with
    - `sudo ip link set can0 type can bitrate 125000`
-   Turn the interface up with
    - `sudo ip link set up can0`
- Repeat the previous exercise, but now connected to a real car via OBD2 connector.
  - Use Turn lights as an example package.
  - Repeat the process of choosing the package and send it.

4. **Analyze and replicate the radio signal and access code from a keyfob to a real car.**
- Connect HackRF One A Laptop Computer. It is recommended to use a computer with partition on Kali linux or booted from a bootable usb memory with Kali.
- Install Universal Radio Hacker
- Clone from github
  - `git clone https://github.com/jopohl/urh.git`
- Install urf following the [github](https://github.com/jopohl/urh.git) instructions
  - `cd urh`
  - `urh`
 - Research on the internet the frequency at which the control of your car works
 - For example my key works in 315 MHz
 - Watch this [video](https://www.youtube.com/watch?v=YmOQstLRVWM) to understand how urh works
 - Record your key fob signal
 - Reproduce this signal like in the video


## References

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  6.1.14
- [Kali Linux ova](https://images.kali.org/virtual-images/kali-linux-2020.3-vbox-amd64.ova) 
- [Car Hacking](https://en.wikipedia.org/wiki/Automotive_hacking)
- [video 1](https://www.youtube.com/watch?v=YmOQstLRVWM)
- [video 2](https://www.youtube.com/watch?v=uIVBVd6yi_A)
- [Evidence from practices](https://1drv.ms/u/s!AsNCtcAQYCEBjDAhbR_X-RRr74e7?e=c8f7Xv)
