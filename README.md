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
<img src="https://i.imgur.com/xun83MA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Add the features from the Active Directory Domain Services 
<img src="https://i.imgur.com/Jh1ZOPu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Open the noticiation window and select "promote this server to a domain controller"
<img src="https://i.imgur.com/liXLchA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Add mydomain.com as a new forest image
<img src="https://i.imgur.com/pVxzKOv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Deselect "Create DNS delegation image
<img src="https://i.imgur.com/1P69f3o.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Finish the setup wizard and install image
<img src="https://i.imgur.com/tpldaxh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The DC-1 will automatically restart

DC-1 is a domain now, in order to complete the next steps, we will have to login using the proper domain 
context (mydomain.com\labuser will be our username - same passwoord) 
<img src="https://i.imgur.com/iTc0ZRq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Create a Domain Admin User
1. Open Active Directory Users and Computers (ADUC).
2. Create an Organizational Unit (OU) named _EMPLOYEES.
3. Create another OU named _ADMINS.
4. Add a new user:
  - Name: Jane Doe
  - Username: jane_admin
  - Password: Cyberlab123!
5. Add jane_admin to the Domain Admins security group.

6. Log out and log back in as mydomain.com\jane_admin.
<img src="https://i.imgur.com/Ufl6m7K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/dxTLbuN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/ObxaJfR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/9vWe4JS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/jRfsfUq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/UkDRDBF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/cvjxZdm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Join Client-1 to the Domain
1. Log in as the local admin and join Client-1 to the domain.
2. Create a new OU titled '_CLIENTS' & add Client-1 in ADUC to _CLIENTS.
Log into DC-1 as Jane the Admin

- We will use DC-1 in a bit image
<img src="https://i.imgur.com/cvjxZdm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Log into client-1 as labuser
<img src="https://i.imgur.com/45A9iS4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Navigate to the system window by right clicking the windows button image
<img src="https://i.imgur.com/wUBpa2s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Join Client-1 to the domain by using the 'rename this pc' tool image
<img src="https://i.imgur.com/MFWS2PF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Verify that Client-1 has joined the domain image
<img src="https://i.imgur.com/1rh5a9H.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Create a new folder named '_CLIENTS' and drag/drop the Client-1 computer into it image
<img src="https://i.imgur.com/Ee58OQ8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Part 3: Creating Users with PowerShell

Setup Remote Desktop for Domain Users
1. Log into Client-1 as mydomain\jane_admin.
2. Open System Properties and enable Remote Desktop.
3. Allow "domain users" access to Remote Desktop.
<img src="https://i.imgur.com/YD5Ht4H.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>image

<img src="https://i.imgur.com/rQcg5Du.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>image

Create Users with PowerShell
1. Log in to DC-1 as jane_admin.
2. Open PowerShell ISE as an administrator.
3.Create multiple new users using a script (script link:
</p>
https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1).
4. Verify users appear in the _EMPLOYEES OU in ADUC.
5. Attempt to log into Client-1 with one of the created accounts.
<img src="https://i.imgur.com/F1O9ugb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>image

- Create a new file image
<img src="https://i.imgur.com/e3azm8k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Copy/Paste scripts & run it image
<img src="https://i.imgur.com/YkjIK8f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Verify users image
<img src="https://i.imgur.com/WwX4hkJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/V1Wqiju.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Log into Client 1 using one of the created accounts image
<img src="https://i.imgur.com/P8PhZNY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Part 4: Group Policy and Managing Accounts

Account Lockout Configuration

1. Log in to DC-1.
2. Open Group Policy Management.
3. Edit the Default Domain Policy:
  - Set account lockout threshold to 5 invalid attempts.
4. Attempt to log in with a user account using incorrect passwords. Observe the account lockout behavior.
5. Unlock the account in ADUC and reset the password.

- Type gpmc.msc into the start window image
<img src="https://i.imgur.com/Kd7xFlk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Right click and edit the default domain policy image
<img src="https://i.imgur.com/n2YsdBO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Navigate to the account lockout policy image
<img src="https://i.imgur.com/reGEizs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Adjust the lockout policy image
<img src="https://i.imgur.com/FLZQp4M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- You can either wait for the policy to auto update (~90 minutes) or log into Client 1 as Jane and force the policy update image
<img src="https://i.imgur.com/Sy1TJXm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Attempt to login with the incorrect password image
<img src="https://i.imgur.com/fWfe6vB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Back on DC-1 Open 'Active Directory Users and Computers' and search for the locked out user image
<img src="https://i.imgur.com/Js4wJ5y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Find the user account and unlock it image
<img src="https://i.imgur.com/xZRdJwf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- You can also reset the password + unlock the account by right clicking on the user name image
<img src="https://i.imgur.com/KgZNdzR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Verify that the account has been unlocked by logging into Client-1 using the correct password image
<img src="https://i.imgur.com/ZVBbaL0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Enable and Disable Accounts

1. Disable a user account in ADUC.
2. Attempt to log in with the disabled account and observe the error message.
3. Re-enable the account and log in successfully.

Right click and disable the account image
<img src="https://i.imgur.com/XRQcWPJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>image
<img src="https://i.imgur.com/BuNCDuQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Attempt to login image
<img src="https://i.imgur.com/HwY8ncw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Re-enable the account from DC-1 image
<img src="https://i.imgur.com/88U4aDm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You should be able to log into Client-1 using the re-enabled account image
<img src="https://i.imgur.com/VRoM7Fl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Observing Logs

Review authentication and account-related logs in Event Viewer:
  - Log on DC-1 for domain-level events (shown below).
  - Log on Client-1 for local events.

- Open eventvwr.msc using the start menu in DC-1 image
<img src="https://i.imgur.com/Uxdr6fg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Navigate to the Security window and find the activity for the test account image
<img src="https://i.imgur.com/t5fT78J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/32pPnHW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>image


- Open Event Viewer using Client-1 and view the audit failures image
<img src="https://i.imgur.com/79klbfr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- If you are using a non-admin account, you won't be able to see the security events image
<img src="https://i.imgur.com/ZzpFkRR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- You can either log off Client 1 and login using an admin account or run the Event Viewer as an admin and enter admin credentials 
<img src="https://i.imgur.com/MfaHMWI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/OAIi8lu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>image

Completion
Congratulations! You have successfully deployed and configured an on-premises Active Directory environment in Azure.


</p>



























