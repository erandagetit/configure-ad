# configure-ad<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Dicrectory
- Create an Admin and Normal User Account in AD

<h2>Deployment and Configuration Steps</h2>

Part 1: Preparing the AD Infrastructure in Azure
  - Setup Domain Controller in Azure
  - Create a Resource Group:
- Navigate to the Azure Portal and create a new Resource Group for the lab environment.

<p>
<img src="https://i.imgur.com/nYzhLx4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/riZJluD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
- Create a Virtual Network and Subnet:
Set up a Virtual Network with a subnet to host your VMs.
</p>
<img src="https://i.imgur.com/zcgmgc4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/RQGpXUB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
- Create the Domain Controller VM (Windows Server 2022):
Name the VM: DC-1.
Ensure that the VM is on the Virtual Network created previously.
</p>
</p>
<img src="https://i.imgur.com/USDmxyz.png"height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/RdNgxHC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/MMJKIiS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
- Set Static Private IP for DC-1: - After the VM is created, navigate to its Network Interface Card (NIC) settings and set the private IP to static.

  - Navigate to the Virtual Machines window and select the DC-1 VM
<p>
<img src="https://i.imgur.com/1hAHvkk.png " height="80%" width="80%" alt="Disk Sanitization Steps"/> 
</p>
<br />
- Set the Allocation to Static underneath the Private IP Address Settings
<p>
<img src="https://i.imgur.com/tzfsVaw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Disable Windows Firewall:

  - Log in to DC-1 and disable the Windows Firewall for testing connectivity

<img src="https://i.imgur.com/duWiJLi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/Au2EVST.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
- Setup Client-1 in Azure
  - Create the Client VM (Windows 10 22H2):
  - Name the VM: Client-1.
</p>
<br />
<img src="https://i.imgur.com/mCc5GLm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/XMOtCSy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Attach Client-1 to the Same Region and Virtual Network:
  - Ensure it is in the same Virtual Network and subnet as DC-1.
</p>
<br />
<img src="https://i.imgur.com/EAmWGLP.png"height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
- Set DNS Settings:
  - Update Client-1's DNS settings to point to DC-1's private IP address. (navigate to the vm's network interface card)
</p>
- You can also change the DNS settings from within the client- computer
</p>
</p>
<img src="https://i.imgur.com/ZuUAskV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/VEwjXCu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/7JH5gyD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Test Connectivity:

  - Restart Client-1 from the Azure Portal.
  - Log into Client-1 and use the ping command to test connectivity with DC-1.
  - Verify DNS Settings:

- Run ipconfig /all in PowerShell on Client-1 to ensure the DNS points to DC-1.
</p>
</p>
<img src="https://i.imgur.com/ST5jGPJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Part 2: Deploying Active Directory
Install Active Directory
Log in to DC-1.
Install Active Directory Domain Services (AD DS).
Promote DC-1 as a Domain Controller and set up a new forest (e.g., mydomain.com).
Restart DC-1 and log in as mydomain.com\labuser.
</p>
Open Server Manager then add roles and features

<img src="<img src="https://i.imgur.com/ST5jGPJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


https://i.imgur.com/kiaiVcB.png


</p>



























