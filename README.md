<h1>Active Directory | System Administration Lab</h1>



<h2>Description</h2>
In this lab, I used Oracle VM Virtual Box to create two virtual machines. One running Windows Server as a domain controller that houses Active Directory. The other VM is created as a client that connects to a private network that is managed by the domain controller. Next, I utilize an outsourced PowerShell script on the DC that creates 1,000 users in Active Directory. I assign IP addressing to each machine and implement Remote Access Server features to support NAT/PAT and configure DNS and DHCP services to allow internet access to the client network though the domain controller acting as a default gateway.
<br />


<h2>Languages and Utilities Used</h2>


- <b>Active Directory</b>
- <b>PowerShell</b> 
- <b>Windows Command Prompt</b> 

<h2>Environments Used </h2>

- <b>Oracle VM Virtual Box</b>
- <b>Windows 10 Enterprise</b> 
- <b>Windows Server</b>

<h2>Project walk-through:</h2>

<p align="center">




Created the first virtual machine to use as a domain controller (DC) which will run Active Directory: <br/>
<img src="https://imgur.com/COTVJiF.png" height="80%" width="80%" />
<br />
<br />
Configured the DC VM to have two NICs (Network Interface Cards/Network Adaptors), one will be used to connect to the outside internet. For this NIC, DHCP will get IP addresses from the home router. The other NIC will be used to connect to the private network that the clients will connect to, this will simulate a corporate/workplace environment:  <br/>
<img src="https://imgur.com/3jm8zWl.png" height="80%" width="80%" />
<br />
<br />
Launched the first VM and installed Windows Server 2019 using the respective ISO file and assigned IP addressing for the internal network:  <br/>
<img src="https://imgur.com/a4m23JV.png" height="80%" width="80%" />
<br />
<br />
Installed Active Directory and created a domain:  <br/>
<img src="https://imgur.com/ivtUOa2.png" height="80%" width="80%" />
<br />
<br />
Created Administrator account inside a new Organizational Unit within Active Directory:  <br/>
<img src="https://imgur.com/CnUebZ8.png" height="80%" width="80%" />
</p>

Configured RAS/NAT (Remote Access Server / Network Address Translation) so the clients on the private network can connect to the internet through the domain controller:  <br/>
<img src="https://imgur.com/6PSC6hV.png" height="80%" width="80%" />
</p>

Set up DHCP on the domain controller so when the second VM is created as a Windows 10 client, it can automatically get an IP address assigned to be able to access the internet from within the private network:  <br/>
<img src="https://imgur.com/NVFCNjA.png" height="80%" width="80%" />
<img src="https://imgur.com/s4PmVQU.png" height="80%" width="80%" />
</p>

Set up DHCP Scope:  <br/>
<img src="https://imgur.com/cNnajqw.png" height="80%" width="80%" />
</p>

Ran a PowerShell script on the domain controller VM to create 1,000 users in Active Directory (I did not create this script):
PowerShell script explanation:

Why:
This script creates 1,000 users in Active Directory automatically. This prevents me from having to manually create each user.

How:
Gets a list of 1,000 names from a text file and stores them in a variable.
Runs a For loop that will iterate through the list and create a user for each name.
<br/>
<img src="https://imgur.com/ITwESQO.png" height="80%" width="80%" />
</p>

The users created:  <br/>
<img src="https://imgur.com/EKOVysp.png" height="80%" width="80%" />
</p>

Next, I created the second VM for the client machine (CLIENT1):  <br/>
<img src="https://imgur.com/gVhp7jb.png" height="80%" width="80%" />
</p>

Configured client to connect to the private network:  <br/>
<img src="https://imgur.com/5bDfXww.png" height="80%" width="80%" />
</p>

Installed Windows 10 Enterprise on the client VM and joined the domain. 
Logged into CLIENT1 from one of the domain accounts and pinged google.com from the client VM to test internet connection and it resolved. 
(Domain controller server on the left - Client user on the right)
:  <br/>
<img src="https://imgur.com/9su0TbB.png" height="80%" width="80%" />
</p>

Since google.com resolved, I know the DNS server is working correctly. The ping to the internet shows there is connectivity from the client to the domain controller running on the other VM (which acts as the default gateway for the client), which then uses NAT properly to forward the connection to the internet and back into the private network. I can then log in to any of the users created.  <br/>





<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
