<p align="center">
<img alt="1" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/9ea02092-b450-472d-bceb-ae612bcb07e4"/>

</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure) (Part 2) </h1>


<p>Starting from where the first part of this tutorial ended, that produced our simulated Active Directory environment, in this second part we will explore the details of deploying and refining an Active Directory system. This part is designed to give a basic understanding of Active Directory services, emphasizing essential aspects such as installation, forest creation, user account administration, domain integration, and customized Remote Desktop Connection access.

</p>

<h2>Prerequisites</h2>

- <a href="https://github.com/giovannibriones/ad-and-azuresetup"> On-premises Active Directory Deployed in the Cloud (Azure) (Part 1) </a>

<h2>Key Objectives</h2>
<h3>Active Directory Installation</h3>

-  Set up and install Active Directory services on the chosen Domain Controller virtual machine.

<h3>Forest Creation</h3>

- Create a new Active Directory forest.

<h3>Administrator Account Creation</h3>

- Produce and administer user accounts with administrative privileges to deal efectively with the Active Directory environment.

<h3>Domain Joining</h3>

- Introduce the Client-01 virtual machine into the established domain, ensuring uninterrupted communication with the Active Directory infrastructure.

<h3>Remote Desktop Setup</h3>

- Configure Remote Desktop Connection access specifically designed for non-administrative users, improving user accessibility while keeping security protocols.




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)


<h2>Configuration Steps</h2>

<h3>&#9312; Install Active Directory in DC-01</h3>

- In the Server Manager dashboard, click Add roles and features and continue the setup <img width="736" alt="2" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/e6004d64-09cf-4472-b00a-08f2689b489b">


<p>

</p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Select Active Directory Domain Services and finish the installation </strong> </p>
<p>
</p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9313; Promote DC-01 to Domain Controller </h3>

- Once the installation is done, notice the flag on the top left of the Server Manager
- Click on the flag and promote DC-01 to Domain Controller.

<img width="242" alt="3" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/6020727b-0778-475a-8181-2ad597fe8137">




<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

- Now add a new Forest and set the Root domain name to “mydomain.com”
<p>
<img width="565" alt="4" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/c4ce5731-0b82-4a8a-bf41-1e2c75beeafa">
 </p>
  
- Finish setup and restart DC-01
- Log back in with “your username"@mydomain.com



<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9314; Creating an Admin in Active Directory </h3>

- Once DC-01 has rebooted, click on tools and select Active Directory Users and Computers
- Right-click on mydomain.com and select new and click on Organizational Unit
<img width="438" alt="5" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/bef564b6-0393-488a-8094-e907f092a3a1">



<br>
<br>
<br>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Create an OU named _EMPLOYEES and _ADMINS </strong></p>

<img width="450" alt="6" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/bf4d2c90-6753-4179-8304-93831f29f81e">



<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Right-click on Users and produce a new user named Jane Doe with the username jane_admin</strong></p>

<img width="323" alt="7" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/d1fe5899-daad-4589-9d03-6367f5fbc145">


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>Turn Jane Doe into an admin by right-clicking her name and adding her to the “Domain Admins” Security Group</strong></p>

<img width="412" alt="8" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/bc7ac07c-1ae5-45d7-9f60-3188ad683769">



<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>Logout of DC-01 and log back in with Jane Doe’s credentials</strong></p>

<img width="337" alt="9" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/b71e7b29-550c-4e61-a8d1-359f14235f85">


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>


<h3>&#9315; Integrate Client-01 to domain </h3>

<p><strong> For Client-01 to integrate into the domain, first set its DNS server as DC-01’s private address.</strong></p>

- In the Azure Portal, select Client-01 -> Networking -> Network interface and click on DNS servers

<img width="735" alt="10" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/b47c3880-1e1c-4c95-8613-912b2374cd25">




<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong>Choose a custom DNS server and type in the private ip address of DC-01 and restart Client-01</strong></p>

<img width="356" alt="11" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/ee5fde66-59c9-4644-ad7a-931520473158">


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now log back in to Client-01 using your original admin credentials. Click start and go to Settings > Rename this PC (advanced) > Change and add “mydomain.com” and log in with the admin credentials previously created (jane_admin) </strong></p>

<img width="297" alt="12" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/442138e1-caad-4d55-86e7-8d5ab0b38557">

<br>

<p> <strong>Once Client-01 has been added, the VM will restart.</strong></p>


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9316; Setup the Remote Desktop Connection for non-administrative users </h3>

- Log back into Client-01 using jane_admin, open Settings > Remote Desktop> User Accounts and click “Select users that can remotely access this PC”
- Add Domain Users

<br>

<img width="343" alt="13" src="https://github.com/giovannibriones/ad-deployment-configuration/assets/163789590/31475ba9-6628-41c1-8aef-a11f896cb0e6">

<p><strong>This will allow normal users to login to Client-01</strong></p>

<br>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>



<h2> In Conclusion </h2>

<p>
We've successfully completed the second part of this tutorial. Through configuring Active Directory on the Domain Controller, we grounded our infrastructure by creating a forest, administrator account, and at the very end of it all, integrating Client-01 into the domain. In the third and final part of this tutorial, users will be generated and various Active Directory situations will be simulated. </p>

