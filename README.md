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
Setup Domain Controller in Azure
Create a Resource Group:
Navigate to the Azure Portal and create a new Resource Group for the lab environment.

<p>
<img src="https://i.imgur.com/viEFhpV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setting up my resources in Azure. 
</p>
<br />

<p>
<img src="https://i.imgur.com/uzo98kd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ensuring Connetivity.
</p>
<br />

<p>
<img src="https://i.imgur.com/EB3oyzW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Selecting Server Roles for Active Directory.
</p>
<br />
<img src="https://i.imgur.com/wFUbjNx.png"height="80%" width="80%" alt="Disk Sanitization Steps"/>
Installing Active Directory

<img src="https://i.imgur.com/TecqRZg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Created a Administrator

<img src="https://i.imgur.com/bgyYtXP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Setup User Account in Active Directory
