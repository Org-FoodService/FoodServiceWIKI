# 🐈‍⬛ GitHub as a Source for NuGet

## Adding GitHub as a Source for NuGet Packages

### Overview

This guide will walk you through the process of adding GitHub as a source for NuGet packages in your project using the `dotnet nuget add source` command. This is particularly useful if you host your own packages on GitHub or need to use packages that are not available on the official NuGet repository.

### Prerequisites

* .NET SDK installed
* A GitHub account with access to the repository containing the NuGet packages
* Personal Access Token generated on GitHub

### Step 1: Generate a GitHub Personal Access Token

1. **Navigate to GitHub Settings**:
   * Log in to your GitHub account.
   * Click on your profile picture in the top right corner and select "Settings".
2.  **Generate a New Token**:

    * In the left-hand menu, select "Developer settings".
    * Click on "Personal access tokens".
    * Click on "Generate new token".\
      ![](<../.gitbook/assets/Imagem do WhatsApp de 2024-06-06 à(s) 17.47.32\_c3b397e7.jpg>)
    * Give your token a descriptive name and select the scopes you need. For accessing packages, you typically need the `repo`, `read:packages`, and `write:packages` scopes.\


    <figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

    * Click "Generate token".
    * **Important**: Copy the token immediately as it will not be shown again.

### Step 2: Add GitHub as a NuGet Source

1. **Open Terminal or Command Prompt**:
   * Open your terminal or command prompt.
2. **Run the `dotnet nuget add source` Command**:
   * Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.
   * `YOUR_PERSONAL_ACCESS_TOKEN` with the personal access token you generated earlier.
   *   Run the following command:

       ```sh
       dotnet nuget add source --username YOUR_GITHUB_USERNAME --password YOUR_PERSONAL_ACCESS_TOKEN --store-password-in-clear-text --name github "https://nuget.pkg.github.com/Org-FoodService/index.json"

       ```

       \


After successfully executing the command, if everything goes well, you should be able to see the newly added source in the NuGet Package Manager settings like shown in the following image:\


<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

You can verify the packages associated with your project on this link: [Org-FoodService GitHub Packages](https://github.com/orgs/Org-FoodService/packages)\
This confirms that GitHub has been successfully added as a source for NuGet packages in your project, and you can access the packages associated with the `Org-FoodService` organization/repository using the provided link.

### Step 3: Using GitHub Packages in Your Project

1. **Restore Packages**:
   * Navigate to your project directory in the terminal.
   *   Run the following command to restore the packages:

       ```sh
       dotnet restore
       ```
2. **Use the Packages**:
   * You can now use the packages in your project as you would any other NuGet package. Simply add the necessary `using` statements and start coding.

