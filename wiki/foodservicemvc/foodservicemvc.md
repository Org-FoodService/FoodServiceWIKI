# 🥗 FoodServiceMVC

### Introduction

FoodServiceMVC is a .NET MVC application that serves as the frontend for the FoodServiceAPI. It allows users to perform various operations related to the food service, such as user authentication, managing food orders, and viewing menus. The frontend communicates with the backend API to retrieve and update data.

### Requirements

To use FoodServiceMVC, you need to have:

* [.NET Core 8.0](../first-steps/installing-.net.md)
* [FoodServiceAPI ](../foodserviceapi/foodserviceapi.md)(running and accessible)
* [FoodService.Models](../first-steps/github-as-a-source-for-nuget.md) (shared models between API and MVC)

### Installation

Follow these steps to set up and run FoodServiceMVC:

1.  Clone the repository:

    ```
    git clone https://github.com/Org-FoodService/FoodServiceMVC.git
    ```
2. Open the project in Visual Studio or your preferred code editor.
3.  Ensure that the `BASE_URL_API` environment variable is correctly configured in either the `appsettings.json` or `launchsettings.json` file. This variable should point to the running instance of FoodServiceAPI. For example:

    ```json
    // appsettings.json
    "BASE_URL_API": "https://localhost:7259/"
    ```

    ```json
    // launchsettings.json
    "profiles": {
       "FoodServiceMVC": {
          "environmentVariables": {
             "BASE_URL_API": "https://localhost:7259/"
          }
       }
    }
    ```
4. Build and run the application.

### Getting Started

Once the application is running, you can navigate to the login page to authenticate yourself. After successful authentication, you will be able to access various features of the FoodService application through the user interface provided by FoodServiceMVC.

