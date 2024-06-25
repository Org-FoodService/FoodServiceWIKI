# 🔧 Installing  .NET

## Getting Started with .NET and Visual Studio Installation

### Overview

This guide will help you set up your development environment for .NET 8.0 and optionally, install Visual Studio, a powerful Integrated Development Environment (IDE) for .NET development. Follow these steps to get started with building .NET applications.

{% content-ref url="../documentation/.net-framework.md" %}
[.net-framework.md](../documentation/.net-framework.md)
{% endcontent-ref %}

### Prerequisites

* A computer running Windows, macOS, or Linux
* Administrator privileges for installing software

### Step 1: Install .NET 8.0 SDK

#### Windows

1. **Download the .NET 8.0 SDK**:
   * Go to the [.NET download page](https://dotnet.microsoft.com/download/dotnet/8.0).
   * Under "Run apps - Runtime", select the latest .NET 8.0 SDK version suitable for your OS.
   * Click on the download link for the installer.
2. **Run the Installer**:
   * Open the downloaded installer.
   * Follow the on-screen instructions to complete the installation.
3. **Verify Installation**:
   * Open Command Prompt or PowerShell.
   *   Run the following command to verify the installation:

       ```sh
       dotnet --version
       ```
   * You should see the installed version of .NET 8.0 SDK.

#### macOS

1. **Download the .NET 8.0 SDK**:
   * Go to the [.NET download page](https://dotnet.microsoft.com/download/dotnet/8.0).
   * Select the latest .NET 8.0 SDK version for macOS.
2. **Install the SDK**:
   * Open the downloaded `.pkg` file.
   * Follow the on-screen instructions to complete the installation.
3. **Verify Installation**:
   * Open Terminal.
   *   Run the following command:

       ```sh
       dotnet --version
       ```
   * You should see the installed version of .NET 8.0 SDK.

#### Linux

1. **Add Microsoft Package Repository**:
   *   Open Terminal and run the following commands:

       ```sh
       wget https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
       sudo dpkg -i packages-microsoft-prod.deb
       ```
2. **Install the SDK**:
   *   Update package lists and install the .NET 8.0 SDK:

       ```sh
       sudo apt-get update
       sudo apt-get install -y apt-transport-https
       sudo apt-get update
       sudo apt-get install -y dotnet-sdk-8.0
       ```
3. **Verify Installation**:
   *   Run the following command:

       ```sh
       dotnet --version
       ```
   * You should see the installed version of .NET 8.0 SDK.

### Step 2: Install Visual Studio (Optional)

#### Windows

1. **Download Visual Studio Installer**:
   * Go to the [Visual Studio download page](https://visualstudio.microsoft.com/downloads/).
   * Click on "Free download" under "Visual Studio Community".
2. **Run the Installer**:
   * Open the downloaded installer.
   * Select the workloads you want to install. For .NET development, select ".NET desktop development" and/or "ASP.NET and web development".
   * Click "Install".
3. **Launch Visual Studio**:
   * After installation, launch Visual Studio.
   * Sign in with a Microsoft account (optional, but recommended for additional features).

#### macOS

1. **Download Visual Studio for Mac**:
   * Go to the [Visual Studio for Mac download page](https://visualstudio.microsoft.com/vs/mac/).
   * Click on "Download Visual Studio for Mac".
2. **Install Visual Studio**:
   * Open the downloaded `.dmg` file.
   * Drag the Visual Studio for Mac icon to the Applications folder.
3. **Launch Visual Studio**:
   * Open Visual Studio from the Applications folder.
   * Sign in with a Microsoft account (optional, but recommended for additional features).

###
