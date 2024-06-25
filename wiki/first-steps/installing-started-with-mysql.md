# 🐬 Installing Started with MySQL

## Getting Started with MySQL and MySQL Workbench Installation

### Overview

This guide will help you set up MySQL for your development environment. Additionally, you have the option to install MySQL Workbench, a powerful tool for managing your MySQL databases. Follow these steps to get started with MySQL.

{% content-ref url="../documentation/sql-server.md" %}
[sql-server.md](../documentation/sql-server.md)
{% endcontent-ref %}

### Prerequisites

* A computer running Windows, macOS, or Linux
* Administrator privileges for installing software

### Step 1: Install MySQL Server

#### Windows

1. **Download MySQL Installer**:
   * Go to the [MySQL Community Downloads page](https://dev.mysql.com/downloads/installer/).
   * Click on "MySQL Installer for Windows" and download the installer.
2. **Run the Installer**:
   * Open the downloaded installer.
   * Choose the setup type (Developer Default is recommended).
   * Follow the on-screen instructions to complete the installation.
   * Configure MySQL Server with a root password and set up any other required configurations.
3. **Verify Installation**:
   * Open Command Prompt.
   *   Run the following command to verify the installation:

       ```sh
       mysql --version
       ```
   * You should see the installed version of MySQL.

#### macOS

1. **Download MySQL DMG Archive**:
   * Go to the [MySQL Community Downloads page](https://dev.mysql.com/downloads/mysql/).
   * Select macOS as your operating system and download the DMG archive.
2. **Install MySQL**:
   * Open the downloaded `.dmg` file.
   * Run the MySQL installer package.
   * Follow the on-screen instructions to complete the installation.
   * Configure MySQL Server with a root password during the installation process.
3. **Start MySQL Server**:
   * Open System Preferences and go to MySQL.
   * Start the MySQL server.
4. **Verify Installation**:
   * Open Terminal.
   *   Run the following command:

       ```sh
       mysql --version
       ```
   * You should see the installed version of MySQL.

#### Linux

1. **Add MySQL APT Repository**:
   *   Open Terminal and run the following commands (for Ubuntu/Debian-based distributions):

       ```sh
       wget https://dev.mysql.com/get/mysql-apt-config_0.8.17-1_all.deb
       sudo dpkg -i mysql-apt-config_0.8.17-1_all.deb
       sudo apt-get update
       ```
2. **Install MySQL Server**:
   *   Run the following command:

       ```sh
       sudo apt-get install mysql-server
       ```
   * During the installation, you will be prompted to set a root password.
3. **Start MySQL Server**:
   *   Ensure MySQL server is running:

       ```sh
       sudo systemctl start mysql
       ```
4. **Verify Installation**:
   *   Run the following command:

       ```sh
       mysql --version
       ```
   * You should see the installed version of MySQL.

### Step 2: Install MySQL Workbench (Optional)

#### Windows

1. **Download MySQL Workbench**:
   * Go to the [MySQL Workbench Downloads page](https://dev.mysql.com/downloads/workbench/).
   * Select the appropriate version for Windows and download the installer.
2. **Run the Installer**:
   * Open the downloaded installer.
   * Follow the on-screen instructions to complete the installation.
3. **Launch MySQL Workbench**:
   * Open MySQL Workbench from the Start Menu or Desktop.

#### macOS

1. **Download MySQL Workbench**:
   * Go to the [MySQL Workbench Downloads page](https://dev.mysql.com/downloads/workbench/).
   * Select the appropriate version for macOS and download the DMG archive.
2. **Install MySQL Workbench**:
   * Open the downloaded `.dmg` file.
   * Drag the MySQL Workbench icon to the Applications folder.
3. **Launch MySQL Workbench**:
   * Open MySQL Workbench from the Applications folder.

#### Linux

1. **Download MySQL Workbench**:
   * Go to the [MySQL Workbench Downloads page](https://dev.mysql.com/downloads/workbench/).
   * Select the appropriate version for your Linux distribution and download the package.
2. **Install MySQL Workbench**:
   *   For Ubuntu/Debian-based distributions, use the following commands:

       ```sh
       sudo dpkg -i mysql-workbench-community_<version>.deb
       sudo apt-get install -f
       ```
3. **Launch MySQL Workbench**:
   * Open MySQL Workbench from the applications menu or run `mysql-workbench` from the terminal.

###
