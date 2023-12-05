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

<h2>Steps</h2>

- Create a resource group in Azure, then create both a Windows 10 and Ubuntu Virtual Machine.  While creating the Windows VM, allow it to create a new Virtual Network (Vnet) and Subnet.  Use Network Watcher to observe your Virtual Network.
- Use Remote Desktop to connect to your Windows 10 Virtual Machine.  Within your Windows 10 Virtual Machine install Wireshark.  Open Wireshark and filter for ICMP traffic only.  Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM.  From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark.  Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.  Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic.  Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity.  Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using.  Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working).  Stop the ping activity.
- Back in Wireshark, filter for SSH traffic only.  From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address).  Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.  Exit the SSH connection by typing ‘exit’ and pressing [Enter].  Back in Wireshark, filter for DNS traffic only.  From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are.  Observe the DNS traffic being show in WireShark.  Back in Wireshark, filter for RDP traffic only (tcp.port == 3389).  Observe the immediate non-stop spam of traffic.
- Close your Remote Desktop connection.  Delete the Resource Group(s) created at the beginning of this tutorial.  Verify Resource Group Deletion.


<h2>Actions and Observations</h2>

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/eb6ac9e9-1214-4f3d-a90b-76322bd0b292"/>
</p>
<p>
Firstly, we create our two Virtual Machines in Microsoft Azure.  
</p>
<br />

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/958e0ef5-e37c-45e5-af12-0d4d1396bfb4"/>
</p>
<p>
After creating our Windows and Ubuntu Virtual Machines in Microsoft Azure, we use Remote Desktop to connect to the Windows VM using its public IP address.
</p>
<br />

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/a78fcb02-7909-4116-8d90-794cfe89d765"/>
</p>
<p>
Once we access our Windows Virtual Machine we go to Wireshark's website to download and install the program.
</p>
<br />

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/8743ab43-069a-4b63-b743-04d2db249cc6"/>
</p>
<p>
When Wireshark has finished installing open the program and select the ethernet adapter, then press "Start Capturing Packets" in the top left.  This will show you all the live traffic happening on the VM.  
</p>
<br />

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/a792efe6-ddcf-4c6d-b337-a75bf697a2ea"/>
</p>
<p>
We want to filter by ICMP, so type ICMP into the open bar and press enter.  This will be used to allow us to watch traffic between our two VMs.  We will need to get our second VM's private IP address to do this, which is found in Azure.
</p>
<br />

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/26cba95d-e911-42a5-ba43-562d4c8ecb19"/>
</p>
<p>
With our VM2 private IP address, go back to our RDP connection with VM1 and open up PowerShell.  Use the ping command followed by the VM2 private IP.  The ping traffic will be visible in both PowerShell and Wireshark.
</p>
<br />

<p>
<img src="https://github.com/yUSaul/azure-network-protocols/assets/140694677/fa4a8600-1ba9-41cc-8f45-588faa46ad29"/>
</p>
<p>
We can also try out a website such as google.com.  Using the ping command again followed by www.google.com, we can then analyze traffic in Wireshark.  There is much more that can be done with Wireshark, such as monitoring other types of traffic.  SSH, DNS, and RDP are a few examples.
</p>
<br />

