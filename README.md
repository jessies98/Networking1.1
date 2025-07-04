<h1>Static Routing-Based Enterprise Branch Network with Segmented Department Access</h1>


<h2>Description</h2>
This project was completed as part of my college networking course. It is designed to simulate a branch office setup within a larger corporate infrastructure. The network aims to provide segmented, secure, and scalable connectivity for multiple departments or workgroups.
The implementation of VLANs separates different types of users—such as HR, IT, and Administration—ensuring both optimal performance and enhanced security. The branch office connects to a main headquarters or cloud services through a simulated WAN connection (via ISP Router), enabling access to remote resources and internet-based applications. Additionally, internal servers are hosted locally to provide essential services such as file sharing, internal web applications, and authentication.

Routers and switches are configured to support the following:
- Inter-VLAN routing
- Local LAN segmentation
- Connectivity to the upstream internet or corporate backbone

<img src="https://github.com/jessies98/Networking/blob/main/Picture1.png?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h2>Project walk-through:</h2>


Starting off the project, we are provided an internet connection that simulates an ISP.  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, we will set up the physical layout of the network equipment. A network rack will hold three routers, three switches, and one server, while a nearby workstation table will include four computers for end-user access and testing.  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture3.png " height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next we will add serial ports to all router before wiring the network <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, we will begin wiring the network. Starting with the routers, we will use serial cables to connect them, designating the S1/0/1 port as the clock rate interface.
-	Router 1 will be connected to Router 2 and Router 3 via serial ports. It will also connect to the ISP through its Gigabit Ethernet port.
- Router 2 will connect to Router 1 and Router 3 using serial ports. Additionally, it will be connected to Switch 1 through its Gigabit port.
- Router 3 will connect to Router 1 and Router 2 via serial ports and will also be connected to Switch 3, which has a server connected to it.
  
Switch Connections:
- Switch 1 and Switch 2 will be connected and configured with a trunk link.
- Switch 1 will be configured with VLANs 10 and 20, while Switch 2 will be configured with VLANs 30 and 40.
-	Each computer will be assigned to its respective VLAN.
-	On Switches 1 and 2, one computer will be connected to port F0/1 and another to port F0/12.
-	VLANs will be separated by port ranges: F0/1–F0/11 for one VLAN, and F0/12–F0/24 for the other.
  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now it's time to configure the routers and bring all interfaces online. Each router's serial interface S1/0/1 will be configured with a clock rate of 500,000.
To allocate IP addresses efficiently across VLANs, we are implementing Variable Length Subnet Masking (VLSM). Specifically, we will use a /27 subnet mask for each VLAN, which provides up to 30 usable host addresses per subnet—ideal for the number of users in each department.
  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Here is the configuration for Router 2. The G0/0/0 interface is divided into sub-interfaces G0/0/0.10 through G0/0/0.40, with each sub-interface serving as the default gateway for VLANs 10 through 40, respectively. This is followed by the IP interface brief output for Routers 1 through 3.
 <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture10.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now it's time to configure the switches. Switch 1 will host VLAN 10 on ports F0/1–F0/11 and VLAN 20 on ports F0/12–F0/24. The Gigabit ports will be configured as trunk ports to allow VLAN traffic to pass between switches and routers.
Switch 2 will be configured similarly, but it will host VLAN 30 on ports F0/1–F0/11 and VLAN 40 on ports F0/12–F0/24.
  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture11.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture12.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <br />
<br />
Router 2 will be configured to provide DHCP services, allowing each connected computer to automatically receive an IP address based on its assigned VLAN. <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture13.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture14.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
A static IP address of 192.168.32.130 is assigned to the server. Below is a ping test to the default gateway to verify network connectivity  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture16.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Static routing is implemented on Routers 1 through 3 to enable communication between all internal networks and ensure proper routing toward the ISP.   <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture17.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
RIPv2 is configured on Router 1 to enable dynamic routing and establish communication with the ISP router.  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture18.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
A ping test was performed from both the PC and the server to verify network connectivity to the ISP router. Successful responses confirm that the internal devices can reach external networks through the configured routing setup.  <br/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture19.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking/blob/main/Picture20.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <br />
<br />
