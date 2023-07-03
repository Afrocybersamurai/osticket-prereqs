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

- Enable (Internet Information services) IIS
- Install webplatform instraller
- Install MySQL
- Install C++ redistributable
- Configure permissions

<h2>Installation Steps</h2>


Open this: [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

We will use these files to install osTicket and some of the dependencies. I’m using this offline version to make sure everyone is using the same version of all the files :)

### Install / Enable IIS in Windows WITH CGI and Common HTTP Features
Navigate to Control Panel -> Programs -> Turn Windows features on or off


- Internet Information Services -> World Wide Web Services -> Application Development Features -> 
[X] CGI
- Internet Information Services -> World Wide Web Services -> 
[X] Common HTTP Features

AND IIS Management Console
- Internet Information Services -> Web Management Tools -> IIS Management Console
	[X] IIS Management Console
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/56b06680-a2ce-4d4f-8379-4b7e7876a5d9)


- Test web server is up and running by inputting
127.0.0.1
Into the web browser

### Install PHP Manager for IIS
- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

### Install Rewrite Module
- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download and install the Rewrite Module (rewrite_amd64_en-US.msi)

### Install PHP
- Create the directory C:\PHP in Windows explorer

- From the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6), download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the contents into C:\PHP
- !! ATTENTION !!
If this appears, choose to “Keep” the file:

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/709050b9-1cad-411e-8dd1-7c659b5bc111)

![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/5c3b1981-1ed1-478c-b77d-6846e97c0ea7)

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
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/77002e29-b16b-47d2-a591-a2caf2c17019)

 ### Register PHP on IIS
- Open IIS as an Admin
Click on windows start button
Type IIS in search box
Right click and ‘run as administrator’
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/2a6d065a-2c81-4a08-9586-9f482aee28f0)

- Register PHP from within IIS
Click on PHP Manager
Register new PHP version
Browse to C:\PHP
Click php-cgi

- Reload IIS (Open IIS, Stop and Start the server)
![image](https://github.com/Afrocybersamurai/osticket-prereqs/assets/136266716/e9ca4e4c-172b-4727-ac6f-261f12ba08aa)


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

