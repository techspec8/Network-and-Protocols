<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic protocols and command prompts in an Azure Windows 10 Virtual Machine, and a Linux (Ubuntu) Virtual Machine using Wireshark and PowerShell. We also experiment with creating a firewall in Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools in PowerShell
- Various Network Protocols (SSH, RDP, DNS, DHCP, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04 (Linux)

<h2>High-Level Steps</h2>

- Use VM1 and VM2 Created From Azu
- Copy Windows IP Address from VM1
- Open Remote Desktop 
- Download and Install Wireshark
- Observe ICMP Traffic
- Create a Firewall
- Observe SSH Traffic fron Linux

<h2>Actions and Observations</h2>

<p> In Azure create a Resource Group with a Windows 10 Virtual Machine (e.g. VM1), and another Linux Ubuntu Virtual Machine (e.g. VM2). Refer to repository 'Compute in Azure' for instructions.</p>
<p>
<img src= https://i.imgur.com/biV3tEk.png
</p>
<br/>
<p>Copy the 'Public IP address' from Windows VM1.</p>
<p>
<img src= https://i.imgur.com/mknn4hA.png
</p>
<br/>
<p>Open 'Remote Desktop' from your search bar. Then, paste your Windows 10 IP address in 'Computer', enter the 'User name', click 'Connect'. You'll then be prompted to enter your password. A security screen will open, click 'Yes" and you're connected.</p>
<p>
<img src= https://i.imgur.com/tMBSPA4.png
</p>
<p>
<img src= https://i.imgur.com/xPmu7mk.png
</p>
<br/>
<p>Using the internet on your Remote Desktop, search Wireshark, download Windows x64 Installer, then 'open file' to install. Click 'Next' throughout each prompt for a standard installation, add a desktop icon if you prefer, click Finish to complete the installation.</p>
<p>
<img src= https://i.imgur.com/y5LGMeO.png
</p>
<p>
<img src= https://i.imgur.com/wGbavZ9.png
</p>
<br/>
<p>Open Wireshark and click the blue shark fin in the upper left corner. Observe the live traffic that runs in the background.</p>
<p>
<img src= https://i.imgur.com/RY6xfOG.png
</p>
<p>Type ICMP in the search bar to filter by ICMP traffic, and notice that there is no ICMP traffic.</p>
<p>
<img src= https://i.imgur.com/t4VZHbp.png
</p>
<p>Retrieve the private IP address of the Ubuntu VM. In PowerShell enter ping 10.0.0.6. and observe ping requests and replies within WireShark and PowerShell.</p>
<p>
<img src= https://i.imgur.com/ZxQL2St.png
</p>
<p>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM by entering ping 10.0.0.6 -t in a PowerShell command line.</p>
<p>
<img src= https://i.imgur.com/RD2sm0W.png
</p>
<p>Open the Network Security Group your Ubuntu VM in Azure and disable incoming (inbound) ICMP traffic by creating a new firewall rule.
</p>
<p>
<img src= https://i.imgur.com/toVSvRM.png
</p>
<p>Back in the Windows 10 VM, observe that ICMP traffic in WireShark and the command line Ping activity has timed out.</p>
<p>
<img src= https://i.imgur.com/kFw5Hci.png
</p>
<p>Re-enable ICMP traffic for the Network Security Group on your Ubuntu VM by changing your rule to allow traffic again. Back in the Windows 10 VM, observe that the ICMP traffic Ping activity has start working again.</p>
<p>
<img src= https://i.imgur.com/DFX1fhs.png
</p>
<p>To observe SSH traffic, back in Wireshark, filter for SSH traffic only. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine by typing the commands 'ssh labuser@10.0.0.6' and then 'Password' and observe the SSH traffic spam in WireShark. You now have a Linux command line shown as labuser@VM2. You can also observe Linux commands and traffic, ($ id, $ uname -a, $ pwd, etc.).Type exit into the command to log out of SSH and go back into your VM1 Windows 10 machine.</p>
<p>
<img src= https://i.imgur.com/drxHim2.png
</p>
<p>Back in Wireshark, filter for DHCP traffic. From Windows 10 VM, issue your VM a new IP address from the command line (ipconfig /renew).</p>
<p>
<img src= https://i.imgur.com/83X73Os.png
</p>
<p>In Wireshark, filter for DNS traffic only. From Windows 10 VM, within a command line, use nslookup to see what google.com's IP address is.</p>
<p>
<img src= https://i.imgur.com/VQa1aQH.png
<p/>
<p>Filter for RDP Traffic only using tcp.port == 3389 in Wireshark. Observe the immediate non-stop spam of traffic because the RDP (protocol) is showing a constant live stream from one computer to another becuase we have an active RDP Port 3389 session from our host, Windows VM1.<p/>
<p>
<img src= https://i.imgur.com/b7zqS5q.png
</p>
