<p align="center">
<img src="https://imgur.com/qeQ17Bg.png" height="60%" width="60%" alt="Windows Troubleshooting"/>
</p>

<h1>Basic Tools for Troubleshooting Windows</h1>
Across the globe businesses, institutions, and personal use computers are predominantly using the Windows Operating System. It is by far the most widely used computer operating system. IT workers must have a solid understanding of how to troubleshoot, and how to use the tools provided from Windows to troubleshoot this operating system. In this tutorial we are going to cover the basics of what these tools do and how to use them effectively.  <br />

<h2>Technologies We'll Be Covering</h2>

- Preinstallation Environment
- Windows System Restore
- System File Check
- Startup Repair

<h2>Operating Systems Used</h2>

- Windows 10 
- Windows 11

<h2>High-Level Steps</h2>

- Creating the VM's
- Installing Wireshark
- Observing network traffic with Wireshark

<h2>Actions and Observations</h2>

<p>
<img src="https://imgur.com/tYRYkNT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>1. Creating the VM's in Azure</h2>

First we must create 2 VM's to send network traffic between. For the main VM we will be using I am running Windows 10, and for the other VM I used Ubuntu server. 

I created both of these in Azure, but this can be done with any VM application.
</p>
<br />

<p>
<img src="https://imgur.com/wupbYrd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>2. Installing Wireshark</h2>
Once completed, boot up the main VM and search download wireshark in google. The installation is pretty straightforward, and once completed wireshark should automatically open. We can now begin sending / receiving data and analyze how protocols work in more detail. 

Since my VM is in Azure, wireshark is automatically running tons of traffic.
</p>
<br />

<p>
<img src="https://imgur.com/KHXBCsY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>3. Observing ICMP Traffic</h2>

Now that we have wireshark, let's observe some protocols in action. In windows powershell I ping the IP address of our Ubuntu server and observe what wireshark captures. In the filters bar on the top left in wireshark enter icmp. We do this so wireshark only shows us traffic from our pings. Now we can see in wireshark echo requests are being sent from our IP address (Source IP), and being received by the Ubuntu server (Destination IP). If the Ubuntu server had a firewall that was blocking ICMP packets, we would not be receiving replies back. 
</p>
<br />

<p>
<img src="https://imgur.com/NzCt6j8.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/90QcF9e.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>4. Observing SSH Traffic</h2>

Next, we will SSH login to the Ubuntu server and observe the traffic wireshark shows us. We do this in Powershell by typing "ssh (username)@(VM's IP)". Immediately after we type this we see Elliptic Curve Deffie-Hellman Key traffic. This is a protocol that establishes a shared secret connection channel between two devices. Next we input the password for the Ubuntu VM, and we are fully logged in. You will now see that the command line changes color and is using bash (linux commands). Anything we type in the terminal will be shown on wireshark. 
</p>
<br />

<p>
<img src="https://imgur.com/XiQVYD5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>5. Observing DHCP Traffic</h2>

Next we will look at DHCP traffic. This is the protocol that automatically assigns device's an IP address so they don't have to be manually configured. We can force some of this traffic by forcing a DHCP renewal of our IP address. We type ipconfig /renew in powershell to perform this action. Once entered we see a DHCPREQUEST and DHCPACK packets. 
</p>
<br />

<p>
<img src="https://imgur.com/sF43sQ0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>6. Observing DNS Traffic</h2>

Finally, we will observe DNS traffic. DNS is the protocol that takes human readable names like "google.com" and converts them into IP addresses so your computer knows where to route. We can generate some traffic in Powershell again using "nslookup google.com" command. Once entered we can see all the information our computer received about the domain google.com, as well as some IP addresses of google servers. 
</p>
<br />
