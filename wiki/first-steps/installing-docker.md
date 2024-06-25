# 🐋 Installing Docker

## Installing Docker Engine

This guide will walk you through the process of installing Docker Engine on various operating systems. Docker Engine is a platform that allows you to package, distribute, and run applications in containers, providing a lightweight and efficient way to deploy software.

### Prerequisites

* A computer running Windows, macOS, or Linux
* Administrator privileges for installing software

### Step 1: Install Docker Engine

#### Windows

Refer to the official Docker documentation for instructions specific to your Windows:[ Install Docker Engine Windows.](https://docs.docker.com/desktop/install/windows-install/)

1. Download Docker Desktop:
   * Go to the Docker Desktop download page.
   * Click on the download link for the installer.
   * Run the downloaded installer and follow the on-screen instructions to complete the installation.
2. Enable Hyper-V (required for Docker Desktop):
   * Open "Control Panel" > "Programs" > "Turn Windows features on or off".
   * Check the box next to "Hyper-V".
   * Click "OK" and restart your computer if prompted.
3. Verify Installation:
   * Open Command Prompt or PowerShell.
   *   Run the following command to verify the installation:

       ```
       docker --version
       ```

#### macOS

Refer to the official Docker documentation for instructions specific to your Windows:[ Install Docker Engine MacOS.](https://docs.docker.com/desktop/install/mac-install/)

1. Download Docker Desktop for Mac:
   * Go to the Docker Desktop for Mac download page.
   * Click on the download link for the installer.
   * Open the downloaded .dmg file and drag the Docker icon to the Applications folder.
2. Launch Docker Desktop:
   * Open Docker from the Applications folder.
   * If prompted, allow Docker to make changes to your system.
3. Verify Installation:
   * Open Terminal.
   *   Run the following command:

       ```
       docker --version
       ```

#### Linux

1. Install Docker Engine:
   * Refer to the official Docker documentation for instructions specific to your Linux distribution: [Install Docker Engine](https://docs.docker.com/engine/install/).
2. Verify Installation:
   * Open Terminal.
   *   Run the following command:

       ```
       docker --version
       ```

