<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

Required Software (included in the [osTicket-Installation-Files.zip](https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0))
- PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)
- URL Rewrite Module (rewrite_amd64_en-US.msi)
- PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip)
- Visual C++ Redistributable (VC_redist.x86.exe)
- MySQL 5.5.62 (mysql-5.5.62-win32.msi)
- HeidiSQL (database management tool)
- osTicket v1.15.8 (osTicket-v1.15.8.zip)

---

<h2>Installation Steps</h2>


## Part 1: Setting Up the Environment

### 1. Create and Access the Azure VM:
- Deploy a Windows 10 VM with 4 vCPUs in Azure
- Connect to the VM using Remote Desktop Protocol (RDP)

### 2. Download and Extract Installation Files:
- Download the `osTicket-Installation-Files.zip` to your VM desktop
- Extract the contents into a folder named `osTicket-Installation-Files`

### 3. Install and Configure IIS with CGI:
- Open **Control Panel → Programs → Turn Windows features on or off**
- Enable **Internet Information Services (IIS)**
- Expand **World Wide Web Services → Application Development Features**
- Check the **CGI** option and complete the installation

## Part 2: Installing Required Components

### 1. Install PHP Manager and URL Rewrite Module:
- Run `PHPManagerForIIS_V1.5.0.msi` from the installation files folder
- Run `rewrite_amd64_en-US.msi` from the installation files folder

### 2. Set Up PHP:
- Create a new directory: `C:\PHP`
- Extract the contents of `php-7.3.8-nts-Win32-VC15-x86.zip` to `C:\PHP`

### 3. Install Visual C++ Redistributable:
- Run `VC_redist.x86.exe` from the installation files folder

### 4. Install and Configure MySQL:
- Run `mysql-5.5.62-win32.msi`
- Select **Typical Setup**
- After installation, launch the Configuration Wizard
- Choose **Standard Configuration**
- Set root username and password to: `root/root`

## Part 3: Configuring IIS and PHP

### 1. Configure PHP in IIS:
- Open **IIS Manager** as Administrator (Run as administrator)
- Register PHP using PHP Manager (select `C:\PHP\php-cgi.exe`)
- Restart the IIS server (Stop then Start)

## Part 4: Installing osTicket

### 1. Deploy osTicket Files:
- Extract `osTicket-v1.15.8.zip` from the installation files folder
- Copy the **upload** folder to `C:\inetpub\wwwroot`
- Rename the folder from **upload** to **osTicket**
- Restart IIS server

### 2. Enable Required PHP Extensions:
- In IIS Manager, go to **Sites → Default → osTicket**
- Open **PHP Manager** and select **Enable or disable an extension**
- Enable the following extensions:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`

### 3. Configure osTicket Files:
- Rename `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php` to `ost-config.php`
- Set permissions for `ost-config.php`:
  - Right-click → **Properties → Security → Advanced**
  - Disable inheritance and remove all permissions
  - Add new permission: **Everyone** (All permissions)

## Part 5: Database Setup and Final Configuration

### 1. Create Database for osTicket:
- Install **HeidiSQL** from the installation files folder
- Launch HeidiSQL and create a new session (root/root)
- Connect to the session
- Create a new database named **osTicket**

### 2. Complete osTicket Web Installation:
- Open a browser and navigate to: `http://localhost/osTicket/setup`
- Complete the form with your helpdesk name and default email
- Configure database connection:
  - **MySQL Database**: osTicket
  - **MySQL Username**: root
  - **MySQL Password**: root
- Click **Install Now**

### 3. Post-Installation Cleanup:
- Delete the setup directory: `C:\inetpub\wwwroot\osTicket\setup`
- Set `ost-config.php` to "Read-only":
  - Navigate to `C:\inetpub\wwwroot\osTicket\include\`
  - Right-click `ost-config.php` → **Properties → Security**
  - Modify permissions to **"Read" only**

## Access Your osTicket Installation

- **Admin Panel**: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
- **End User Portal**: [http://localhost/osTicket/](http://localhost/osTicket/)

This completes the installation of osTicket on your Windows 10 Azure VM.
