# 🔻 Getting Started with SQL Server and SQL Server

#### Overview

This guide will assist you in setting up SQL Server for your development environment. Additionally, you have the option to install SQL Server Management Studio (SSMS), a powerful tool for managing your SQL Server databases. Follow these steps to get started with SQL Server.

#### Prerequisites

* A computer running Windows
* Administrator privileges for installing software

#### Step 1: Install SQL Server

**Windows**

1. Download SQL Server Installer:
   * Go to the Microsoft SQL Server Downloads page.
   * Select the desired edition of SQL Server and download the installer.
2. Run the Installer:
   * Open the downloaded installer.
   * Select the desired installation options.
   * Follow the on-screen instructions to complete the installation.
3. Configure SQL Server:
   * During the installation process, you will be prompted to configure SQL Server, including setting a password for the 'sa' user (system administrator).

**Linux**

1. Download and Add the SQL Server Repository:
   * Follow the instructions in the official SQL Server documentation to add the appropriate repository for your Linux distribution.
2. Install SQL Server:
   * Execute the appropriate command for your Linux distribution to install SQL Server.
3. Configure SQL Server:
   * During the installation, you will be prompted to set a password for the 'sa' user.

#### Step 2: Install SQL Server Management Studio (SSMS) (Optional)

**Windows**

1. Download SSMS Installer:
   * Go to the Microsoft SQL Server Management Studio Downloads page.
   * Download the SSMS installer.
2. Run the Installer:
   * Open the downloaded installer.
   * Follow the on-screen instructions to complete the installation.
3. Launch SQL Server Management Studio:
   * Open SSMS from the Start Menu.

#### Verification of Installation

* Open Command Prompt (Windows) or Terminal (Linux).
*   Execute the following command to verify the installed version of SQL Server:

    ```
    sqlcmd -S localhost -U sa -P your_password -Q "SELECT @@VERSION"
    ```
* You should see the installed version of SQL Server.

This guide should help you get started with installing SQL Server and optionally SQL Server Management Studio in your development environment.
