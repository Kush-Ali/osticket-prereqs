<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo">
</p>

<h1>osTicket - Prerequisites and Installation</h1>

<p>In this lab, I will walk through the prerequisites and installation of the open-source help desk ticketing system, osTicket, using Microsoft Azure virtual machines.</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- PHP 7.3.8
- MySQL 5.5.62
- VC_redist
- PHP Manager for IIS
- Rewrite Module for IIS

<h2>Operating Systems Used</h2>

- Windows 10 (22H2)

<h2>List of Prerequisites</h2>

<ul>
  <li><strong>Azure Virtual Machine:</strong> I set up a Windows 10 VM with 4 vCPUs using Microsoft Azure.</li>
  <li><strong>Remote Desktop Connection (RDP):</strong> I connected to the VM using Remote Desktop.</li>
  <li><strong>Internet Information Services (IIS):</strong> I installed and configured IIS on the Windows 10 VM to serve web applications.</li>
  <li><strong>PHP and PHP Manager:</strong> I installed and configured PHP with PHP Manager on IIS to support osTicket.</li>
  <li><strong>MySQL Database:</strong> I installed MySQL to store osTicket data.</li>
  <li><strong>osTicket Installation Files:</strong> I downloaded and extracted osTicket installation files.</li>
</ul>

<h2>Installation Steps</h2>

<p><strong>Create a Virtual Machine on Azure Step 1</strong>: I started by logging into the Azure Portal and clicking on "Create a Resource." From there, I selected "Virtual Machine" and named my virtual machine osTicket-Lab. I chose Windows 10 Pro, Version 22H2 for the image and selected Standard_D2s_v3 (2 vCPUs, 8 GiB memory) for the size. After creating a username and password (labuser and osTicketPassword1!), I clicked "Review + Create" and deployed the virtual machine.</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/474e6171-e698-4d18-94c5-deebdd987e5c" height="80%" width="80%" alt="Step 1 Image"/>
</p>


<p><strong>Connect to the VM Step 2</strong>: Once the VM was deployed, I went to the homepage in Azure and clicked on the VM (osTicket-Lab). This displayed its public IP address, which I used to connect to the VM via Remote Desktop. I added the IP to Remote Desktop by clicking "Add PC" and entered osTicket-Lab as the friendly name. I then connected to the VM by entering the credentials created in Step 1.</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/b20294b6-96a6-4521-b04e-db5ecdbe1751" height="80%" width="80%" alt="Step 2 Image 1"/>
</p>



<p><strong>Enable IIS and CGI Step 3</strong>: I enabled IIS and CGI in the Windows VM by navigating to the Control Panel, selecting "Programs," and clicking "Turn Windows features on or off." I checked the box next to Internet Information Services (IIS) and then enabled CGI under the World Wide Web Services section.</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/ea33be6f-594c-439a-b80d-518a7d85c70e" height="80%" width="80%" alt="Step 3 Image 2"/>
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/4abd9dc4-77fd-4e1b-8a65-7fce73754fec" height="80%" width="80%" alt="Step 3 Image 3"/>
</p>



<p><strong>Installing PHP, Rewrite Module, and VC_redist Step 4</strong>: I navigated to the `osTicket-Installation-Files` folder on my desktop within the VM and installed PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi) and the Rewrite Module (rewrite_amd64_en-US.msi). Next, I created a folder at `C:\PHP` and unzipped PHP 7.3.8 into it. Finally, I installed the Microsoft Visual C++ Redistributable (VC_redist.x86.exe) to ensure all necessary libraries were available.</p>
<p align="center">
  <img width="1440" alt="Screenshot 2024-10-01 at 2 49 31 AM" src="https://github.com/user-attachments/assets/8be90b70-8cb5-4679-9ac0-89e6fb3bb23c">
</p>
<p align="center">
  <img width="1440" alt="Screenshot 2024-10-01 at 2 50 09 AM" src="https://github.com/user-attachments/assets/17e5b78d-eb3c-438c-a859-190fb386e5fc">
</p>



<p><strong>Installing MySQL Step 5</strong>: From the `osTicket-Installation-Files` folder, I installed MySQL 5.5.62 (mysql-5.5.62-win32.msi) using the Typical Setup. After installation, I launched the Configuration Wizard, chose "Standard Configuration," and set the MySQL root username and password to `root` for both fields.</p>
<p align="center">
  <img width="1440" alt="Screenshot 2024-10-01 at 3 20 21 AM" src="https://github.com/user-attachments/assets/109d9b25-e4c0-4814-bab5-d02d0caaeb57">
</p>


<p><strong>Configure IIS and Install osTicket Step 6</strong>: I opened IIS as an administrator by searching for "IIS Manager" and selecting "Run as Administrator." I then registered PHP in IIS by navigating to "PHP Manager" and setting the path to "C:\PHP\php-cgi.exe". Once PHP was registered, I reloaded IIS by stopping and starting the server through IIS Manager.</p>

<p>After that, I installed osTicket v1.15.8. I went to the "osTicket-Installation-Files" folder on my desktop, unzipped "osTicket-v1.15.8.zip," and copied the "upload" folder into "C:\inetpub\wwwroot." I renamed the "upload" folder to "osTicket." After renaming, I reloaded IIS again by stopping and starting the server.</p>

<p>Next, I accessed osTicket by going to IIS Manager, navigating to "Sites" -> "Default Website" -> "osTicket", and clicking "Browse *:80" on the right-hand side. This opened osTicket in my browser. When certain PHP extensions were not enabled, I returned to IIS Manager, navigated to "Sites" -> "Default Website" -> "osTicket", double-clicked "PHP Manager", and then clicked "Enable or disable an extension." I enabled the following extensions: "php_imap.dll", "php_intl.dll", and "php_opcache.dll". After enabling these extensions, I refreshed the osTicket site in my browser.</p>

<p align="center">
  <img width="1440" alt="Screenshot 2024-10-01 at 3 46 25 AM" src="https://github.com/user-attachments/assets/2e98275a-efcb-4fe9-9556-47418b294a14">
</p>
<p align="center">
  <img width="1440" alt="Screenshot 2024-10-01 at 3 47 19 AM" src="https://github.com/user-attachments/assets/a0442318-a068-4f18-bb75-c38e39cf0c74">
</p>




<p><strong>Finalizing osTicket Setup and Database Configuration Step 7</strong>: I continued setting up osTicket in my browser by clicking "Continue" on the setup page. When prompted, I named the helpdesk (I chose "Helpdesk") and set the default email address that would receive messages from customers.</p>

<p>Next, from the "osTicket-Installation-Files" folder, I installed **HeidiSQL** by launching the installer. Once installed, I opened **HeidiSQL** and created a new session with the username "root" and the password "root". I connected to the session and created a new database named "osTicket".</p>

<p>After the database was created, I returned to the osTicket setup in my browser. I entered the following MySQL details: MySQL Database: "osTicket", MySQL Username: "root", and MySQL Password: "root". Once these details were filled in, I clicked "Install Now!"</p>
