<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- <h4>Provision Azure Virtual Machines and Network Resources: </h4>
Set up two or more virtual machines (VMs) in Azure, along with the necessary virtual networks and subnets to enable communication between them.
- <h4>Configure Network Security Groups (NSGs): </h4>
Create and apply NSGs to control inbound and outbound traffic rules between the VMs, defining which types of traffic are allowed or denied.
- <h4>Capture Network Traffic with Wireshark: </h4>
Install and use Wireshark on one or more VMs to monitor and analyze network packets, observing the impact of NSG rules on different traffic flows.
- <h4>Test and Modify NSG Rules: </h4>
Conduct experiments by modifying NSG rules and observing how changes affect traffic visibility and accessibility between the VMs, reinforcing network security concepts.
<h2>Actions and Observations</h2>

<p>
<img src="https://github.com/user-attachments/assets/bd60f0f5-e414-484a-9769-9f5f035ae9df"/>
</p>
<p>
This screenshot shows the Azure Portal with two virtual machines deployed: `linux-vm` (Ubuntu Server 20.04) and `windows-vm` (Windows 10).  
Both VMs are part of the same resource group (`RG-Network-Activities`) and are running in the `East US 2` region, ensuring they can communicate efficiently within the same virtual network.  
Public IP addresses are assigned to each VM to allow remote access using SSH (Linux) and RDP (Windows).  
This setup serves as the foundation for experimenting with network traffic and applying Network Security Groups (NSGs).
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/69cdd02e-f41b-4ceb-8907-a2f836aed7fb"/>
</p>
<p>
In this step, a custom inbound security rule was added to the Network Security Group (NSG) associated with the `linux-vm`.  
The rule specifically denies ICMPv4 traffic from any source to any destination, effectively blocking ping requests to the VM.  
A priority value of 290 was set to ensure this rule takes precedence over the existing SSH rule (priority 300).  
This configuration allows us to observe how NSG rules affect network communication, which will later be verified using traffic analysis tools like Wireshark.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/98e259fd-84c6-4a00-9335-22ac3758f65b"/>
</p>
<p>
During this step, Wireshark was used to monitor ICMP traffic between virtual machines. A continuous ping test was initiated, and the packet capture showed ICMP Echo Requests being sent but not receiving any Echo Replies. This behavior, along with "Request timed out" messages in PowerShell, indicates that the traffic was successfully blocked. The result demonstrates how Network Security Group (NSG) rules can control and restrict specific types of traffic, such as ICMP.
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/d92b1153-e95c-4776-9a39-34f7420975ff" width="30%"><br><sub>SSH Traffic</sub>
  
  <img src="https://github.com/user-attachments/assets/d8c9052b-02e9-4fba-b83a-abd8b2efefa6" width="30%"><br><sub>DNS Traffic</sub>
  
  <img src="https://github.com/user-attachments/assets/f30b7910-5265-4949-a79f-27632155f4a7" width="30%"><br><sub>RDP (Port 3389)</sub>
</p>
<p>
These images collectively demonstrate the impact of modifying Network Security Group (NSG) rules on traffic visibility and communication between virtual machines. The first screenshot shows successful SSH access to a VM, confirming that the relevant port is open. The second image captures DNS resolution activity, verifying name resolution functionality across the network. The third screenshot highlights RDP traffic on port 3389, showing secure remote desktop connections. Together, these tests illustrate how enabling or restricting specific ports in NSG rules directly influences network accessibility and security. Monitoring these interactions with tools like Wireshark reinforces key network security concepts in a practical context.

</p>
<br />
