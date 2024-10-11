<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
<br> This project is part of my Course Careers lab work, where I successfully set up and installed osTicket on a Windows 10 Virtual Machine (VM) hosted on Azure. This guide outlines the step-by-step process I followed, including configuring IIS, installing MySQL, and setting up osTicket. Screenshots have been added to show progress at key steps.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)



## Project Steps

### 1. Create an Azure Virtual Machine
In this project, I first created an Azure Virtual Machine with the following specs:
- **VM Name**: `osticket-vm`
- **Operating System**: Windows 10
- **vCPUs**: 4 (required for osTicket performance)
- **Username**: `labuser`
- **Password**: `osTicketPassword

<img width="472" alt="Screenshot 2024-10-11 144508" src="https://github.com/user-attachments/assets/540ba5e7-ec97-4752-ab0b-5457bdefac06">




After setting up the VM, I accessed it via Remote Desktop (RDP).

---

### 2. Install IIS and Enable CGI
To prepare the VM for osTicket, I enabled IIS and the necessary features:
1. Opened **Windows Features** from the Control Panel.
2. Enabled **Internet Information Services (IIS)**, ensuring **CGI** was checked under:
   - **World Wide Web Services** -> **Application Development Features**.


---

### 3. Download and Setup osTicket Files
After configuring IIS, I downloaded the required files and prepared the environment:
1. Downloaded the `osTicket-Installation-Files.zip` and extracted it to my desktop.
2. Installed:
   - **PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi`)
   - **Rewrite Module** (`rewrite_amd64_en-US.msi`)

---

### 4. PHP Setup
Next, I configured PHP to work with IIS:
1. Created the directory `C:\PHP`.
2. Extracted **PHP 7.3.8** (`php-7.3.8-nts-Win32-VC15-x86.zip`) to the `C:\PHP` folder.
3. Installed **VC_redist.x86.exe** to meet the PHP dependency requirements.

<img width="664" alt="Screenshot 2024-10-11 220531" src="https://github.com/user-attachments/assets/8beb62b9-1110-44ab-aa29-0ed9a09d03af">



---

### 5. MySQL Installation
MySQL was required for the osTicket database:
1. Installed **MySQL 5.5.62** (`mysql-5.5.62-win32.msi`).
2. Followed the **Typical Setup** and used **Standard Configuration**.
3. Set both the **root** username and password to `root`.

---

### 6. Setting Up IIS for osTicket
Now that PHP and MySQL were installed, I set up IIS for osTicket:
1. Registered PHP in IIS via **PHP Manager**, pointing to `C:\PHP\php-cgi.exe`.
2. Restarted IIS for the changes to take effect.
3. Unzipped **osTicket-v1.15.8.zip** and moved the `upload` folder to `C:\inetpub\wwwroot`.
4. Renamed the `upload` folder to `osTicket`.

<img width="781" alt="Screenshot 2024-10-11 215820" src="https://github.com/user-attachments/assets/bbb67351-19b9-4dd2-9ffc-803b66bb9b1a">



---

### 7. PHP Extensions Configuration
After setting up IIS, I configured PHP extensions required by osTicket:
1. In IIS, I opened **PHP Manager**.
2. Enabled the following extensions:
   - `php_imap.dll`
   - `php_intl.dll`
   - `php_opcache.dll`

This allowed osTicket to function properly. I then restarted IIS once more.

---

### 8. Configuring osTicket
With the basic setup complete, I moved on to osTicket’s configuration:
1. Renamed the file `ost-sampleconfig.php` to `ost-config.php` in `C:\inetpub\wwwroot\osTicket\include`.
2. Changed file permissions for `ost-config.php`:
   - Disabled inheritance and removed existing permissions.
   - Granted **Everyone** full control temporarily to complete the installation.

---

### 9. Completing osTicket Setup in the Browser
Finally, I accessed osTicket from a web browser to finalize the installation:
1. Browsed to `http://localhost/osTicket/scp/login.php` to start the setup.
2. Set the Helpdesk name and email for receiving tickets.
3. Connected osTicket to the MySQL database using:
   - **Database Name**: `osTicket`
   - **Username**: `root`
   - **Password**: `root`
4. Clicked **Install Now!** to complete the installation.


![osTicket Setup](https://github.com/user-attachments/assets/fd613ece-4fe7-497e-b7a9-d244f065d671)

---

### 10. Post-Installation Clean-up
Once the installation was complete:
1. Deleted the `setup` folder from `C:\inetpub\wwwroot\osTicket` to secure the system.
2. Set the permissions of `ost-config.php` to **Read-only** for added security.

---

## Access URLs
- **End Users osTicket URL**: `http://localhost/osTicket`
- **Admin Login URL**: `http://localhost/osTicket/scp/login.php`

---

## Conclusion
This project demonstrates the steps I took to successfully install and configure osTicket as part of my course work. Each step involved configuring the server environment, installing necessary software, and setting up a fully functioning helpdesk system. This hands-on experience provided valuable insights into server management and software installation in a real-world environment.



---
