<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Traffic Examination"/>
</p>

<h1>Configuring GPO and Unlocking Users Accounts & Resetting Password in Azure Virtual Miachine</h1>
This tutorial outlines the implementation of on-premise Active Directory within Azure Virtual Machines.<br />
 

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Powershell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Step 1: Log into our DC-1 (Domain Controller) Virtual Machine</h2>
<b>Log into your domain controller as Jane Admin</b>
<img src="https://imgur.com/a/90l9jg1" width="600" alt="AD"/>
<br />


<h2>AStep 2: Access run in search menu</h2>
<b>We are going to configure the Group Policy Object(GPO) by accessing Group Policy Management through run</b>
<p>
  <ul>
    <li>Go to the search bar menu at the bottom left of the screen</li>
    <li>Type in run</li>
    <li>Next type gpmc.msc</li>
    <li>Open up Group Policy Management</li>
    <img src="https://i.imgur.com/ORmudXb.png" width="600" alt="AD"/>
    <img src="https://i.imgur.com/1bSFgUE.png" width="600" alt="AD"/>
  </ul>
</p>
<br />


<h2>Step 3: Configuring the Account Lockout Policy</h2>
<b>Inside Group Policy Management, we are going to edit our domain (mydomain.com)</b>
<p>
  <ul>
    <li>Click the Domain folder dropdown</li>
    <li>Click mydomain.com dropdown</li>
    <li>Go to Default Domain Policy > right-click and go to Edit</li>
    <li>This will open Group Policy Management Editor</li>
    <img src="https://i.imgur.com/nkFWkCr.png" width="600" alt="AD"/>
    <li>Next click on Computers Configuration</li>
    <li>Click Policies folder dropdown</li>
    <li>Drop down the Windows settings folder</li>
    <li>Drop down the Security Settings</li>
    <li>Drop down the Account Policies > Left click Account Lockout Policy</li>
    <li>Configure the settings in the right pane to these settings shown in the screenshots</li>
    <img src="https://i.imgur.com/e9LtkYg.png" width="600" alt="AD"/>
    <img src="https://i.imgur.com/ne20v5U.png" width="600" alt="AD"/>
  </ul>
</p>
<br />


<h2>Step 4: Enforce the Group Policy Update</h2>
<b>We have to access our Client-1 machine to enforce the group policy update via the command line</b>
<p>- Log into your CLIENT-1 vm as Jane Admin</p>
<img src="https://i.imgur.com/u1luCtC.png" width="600" alt="AD"/>
<p>
  <ul>
    <li>In the Search bar, type Command Prompt</li>
    <li>Right click to run as administrator</li>
    <li>Type gpupdate /force</li>
    <img src="https://i.imgur.com/rXsdDx5.png" width="600" alt="AD"/>
    <li>Group Policy will be updated</li>
    <img src="https://i.imgur.com/Fs1uErZ.png" width="600" alt="AD"/>
  </ul>
</p>
<br />


<h2>Step 5: Attempt to log into CLIENT-1 as a random user to lockout the account with the wrong password</h2>
<b>We will perform a deliberate account lockout</b>
<p>
  <ul>
    <li>Choose a random user from the _EMPLOYEES in Active Directory (DC-1)</li>
    <li>Type in the password wrong several times</li>
    <li>The account should lockout</li>
    <img src="https://i.imgur.com/8BKTrJk.png" width="600" alt="AD"/>
    <li>The shown error message will appear:</li>
    <img src="https://i.imgur.com/9Z2xisz.png" width="600" alt="AD"/>
  </ul>
</p>
<br />


<h2>Step 6: Find the account in our Active Directory</h2>
<b>In our Domain Controller, we search for the end user's account(locked out account) in our Actice Directory</b>
<p>
  <ul>
    <li>Go to Active Directory Users and Computers on the Domain Controller</li>
    <li>Right click mydomain.com > find</li>
    <li>Type in the end user's name</li>
    <img src="https://i.imgur.com/1cRYExo.png" width="600" alt="AD"/>
  </ul>
</p>
<img src="https://i.imgur.com/YJHCa8o.png" width="600" alt="AD"/>
<p>
  <ul>
    <li>Double click their name that's at the bottom</li>
    <li>Go to the account tab</li>
    <li>Click the unlock account checkbox</li>
    <li>Click Apply > OK</li>
    <img src="https://i.imgur.com/sak5iNX.png" width="600" alt="AD"/>
    <li>Go back to their name and right click > reset password</li>
    <li>Type in their new temporary password</li>
    <img src="https://i.imgur.com/NBBTvQG.png" width="600" alt="AD"/>
    <img src="https://i.imgur.com/gYbDR4d.png" width="600" alt="AD"/>
  </ul>
</p>
<br />


<h2>Step 7: Attempt to log into CLIENT-1 as the end user with the right password</h2>
<b>We are going to log in CLIENT-1 as the end user with the right password this time</b>
<p>
  <ul>
    <li>Log into CLIENT-1 as the end user</li>
    <li>The end user should be able to login to their account</li>
    <img src="https://i.imgur.com/JA1L8FH.png" width="600" alt="AD"/>
    <li>If you open PowerShell, you’ll see that we’re currently logged into the Client-1 machine as the user mog.raki</li>
    <img src="https://i.imgur.com/mf71RBh.png" width="600" alt="AD"/>
  </ul>
</p>
<br />
