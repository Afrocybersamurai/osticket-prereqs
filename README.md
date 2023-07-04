<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>


<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com/watch?v=K7T_JjvEamg&pp=ygUIb3N0aWNrZXQ%3D)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- Internet Information Services (IIS)
- PHP Manager
- Rewrite Module
- VC Redist
- MySQL
- Heidi SQL
- osTicket v1.15.8

<h2>Create Azure virtual machine (recommended)</h2>

1.) Create a virtual machine by going to https://portal.azure.com/. 
- Setup your virtual machine with Windows 10 Pro, version 22H2.
- Note, you will want to create a virtual machine with atleast 2 vcpus and 16 gbs of memory.
- - Ensure Adminstrator account -> Authentication type [x] Password 
- Enter your desired username and password (ensure these details are kept safe somewhere, I recommend in notepad on the desktop since we'll only use for this lab)
- Review and create VM
  
2.) Once you have created your virtual machine you will connect to it by copying the public ip address provided in the azure portal details. 

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/70a83f19-e7f8-47f3-a5e9-455672849904)


3.) You will connect using the remote desktop connection app. Search remote desktop in your start menu search bar.
- Enter the public ip address

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/c0e8620b-20bf-479c-8192-4b091e992c6d)

- Once connected use previous username and password you save to notepad

<h2>Installation Steps</h2>

Open this: [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

We will use these files to install osTicket and some of the dependencies. I’m using this offline version to make sure everyone is using the same version of all the files :)

### Install / Enable IIS in Windows WITH CGI and Common HTTP Features
Navigate to Control Panel -> Programs -> Turn Windows features on or off
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/a4025bf4-a9ea-4c27-9d0e-b8fdb4d283ea)
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/d4040c48-2066-4cfc-8def-e0cd5fed67db)




- Internet Information Services -> World Wide Web Services -> Application Development Features -> 
[X] CGI


![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/a126ed25-906c-4ae8-84a4-cca4c5b74b8a)
- Internet Information Services -> World Wide Web Services -> 
[X] Common HTTP Features
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/e5a81c8f-175f-43cf-95d2-1a8fafe13647)

AND IIS Management Console
- Internet Information Services -> Web Management Tools -> IIS Management Console
	[X] IIS Management Console



- Test web server is up and running by inputting
127.0.0.1
Into the web browser
It should look something like this.
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/401fdf89-8575-4bf1-a669-a89bc0499ea7)


### Install PHP Manager for IIS
- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

### Install Rewrite Module
- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download and install the Rewrite Module (rewrite_amd64_en-US.msi)

### Install PHP
- Create the directory C:\PHP in Windows explorer

- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the contents into C:\PHP
- !! ATTENTION !!
If this appears, choose to “Keep” the file:


![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/bd903646-790f-4d85-90ab-0862dc0e4b26)
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/08fb175d-2e00-4d20-aaa5-7e3beb62cafc)


If you are still having trouble downloading PHP 7.3.8, please try downloading and installing Google Chrome and doing it from within there. 

- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download and install VC_redist.x86.exe.

### Install MySQL
- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
- Typical Setup ->
- Launch Configuration Wizard (after install) ->
- Standard Configuration ->
[X] Install as Windows Service
- Next
- Enter desired your password x2
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/c3ae8872-8c40-4f90-9ecd-224393860603)

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/292febfc-0e0a-4257-a6f2-d91cca00736b)

 ### Register PHP on IIS
- Open IIS as an Admin
Click on windows start button
Type IIS in search box
Right click and ‘run as administrator’


- Register PHP from within IIS
Click on PHP Manager

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/5fc71b94-83b1-4b5f-b480-86d68c787aa1)

- Register new PHP version

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/e43f6805-740d-462a-986e-f0db11e517b4)

Browse to C:\PHP
Click php-cgi
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/d1a7d5f1-0fef-4865-93ba-b4f18a435f23)

- Reload IIS (Open IIS, Stop and Start the server)
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/b060e462-302d-407a-a8fd-d4759094474b)


### Install osTicket
- Install osTicket v1.15.8
Download osTicket from the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6) Folder
Extract and copy “upload” folder to c:\inetpub\wwwroot
Within c:\inetpub\wwwroot, Rename “upload” to “osTicket”

Reload IIS (Open IIS, Stop and Start the server)

- Go to sites -> Default -> osTicket
On the right, click “Browse *:80”

Note that some extensions are not enabled
Go back to IIS, sites -> Default -> osTicket
Double-click PHP Manager
Click “Enable or disable an extension”
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opcache.dll
Refresh the osTicket site in your browse, observe the changes

- Rename: ost-config.php
From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

- Assign Permissions: ost-config.php
Disable inheritance -> Remove All
New Permissions -> Everyone -> All

Continue Setting up osTicket in the browser (click Continue)
Name Helpdesk
Default email (receives email from customers)

- From the Installation Files, download and install HeidiSQL.
Open Heidi SQL
Create a new session, root/Password1
Connect to the session
Create a database called “osTicket”

- Continue Setting up osticket in the browser
MySQL Database: osTicket
MySQL Username: root
MySQL Password: [enter password you used earlier]
Click “Install Now!”

Congratulations, hopefully it is installed with no errors!
Browse to your help desk login page: http://localhost/osTicket/scp/login.php

End Users osTicket URL:
http://localhost/osTicket/ 

- Clean up
Delete: C:\inetpub\wwwroot\osTicket\setup
Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Notes:
Browse to your help desk login page: http://localhost/osTicket/scp/login.php  
End Users osTicket URL: http://localhost/osTicket/ 

<h2>osTicket Post installation Configure Roles</h2>
Configure Roles
- Admin Panel -> Agents -> Roles
- Supreme Admin
- Configure Departments
- Admin Panel -> Agents -> Departments
- System Administrators

Configure Teams
- Admin Panel -> Agents -> Teams
- Level I Support
- Level II Support

Allow anyone to create tickets
- Admin Panel -> Settings -> User Settings
Registration Required: Require registration and login to create tickets 

Configure Agents (workers)
- Admin Panel -> Agents -> Add New
- for example =
Jane
John

Configure Users (customers)
- Agent Panel -> Users -> Add New
- for example =
Karen
Ken

Configure SLA
- Admin Panel -> Manage -> SLA
- Sev-A (1 hour, 24/7)
- Sev-B (4 hours, 24/7)
- Sev-C (8 hours, business hours)

Configure Help Topics
- Admin Panel -> Manage -> Help Topics
Business Critical Outage
Personal Computer Issues
Equipment Request
Password Reset

<h2>Practice making, assigning and completing tickets</h2>
Just practice creating, triaging, and solving tickets. I recommend watching the video to learn about triaging multiple tickets.

- Ticket examples:
- Sev-A (1 hour, 24/7) [entire mobile/online banking system is down] -> SysAdmins
- Sev-B (4 hours, 24/7) [accounting department needs adobe upgrade, broken]
- Sev-B/C (2 hours, business hours) [CFO’s laptop seems a bit slow]

