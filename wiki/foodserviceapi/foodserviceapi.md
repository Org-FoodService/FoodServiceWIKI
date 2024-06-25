# 👨‍💼 FoodServiceAPI

### Introduction

FoodServiceAPI is a .NET application that utilizes .NET Core 8.0. It connects to a MySQL database for data storage, authentication is performed via JWT , and it utilizes Entity Framework Core for data access.

### Requirements

To use FoodServiceAPI, you need to have:

* [.NET Core 8.0](../first-steps/installing-.net.md)
* [SQLServer](../documentation/sql-server.md)
* [Docker ](../first-steps/installing-docker.md)([required for logging features](logging-implementation.md))
* [FoodService.Models](../first-steps/github-as-a-source-for-nuget.md)

### Installation

1. Clone the repository:

```bash
git clone https://github.com/Org-FoodService/FoodServiceAPI.git
```

2. Open the project in Visual Studio or your preferred code editor.
3.  **Update the connection string in the `appsettings.json` file** to match your SQLServer database configuration. For example:

    <pre class="language-json" data-title="appsettings.json"><code class="lang-json">...
    "ConnectionStrings": {
    <strong>    "DefaultConnection": "Server=NICOLAS-DESKTOP\\FOODSERVICE;Initial Catalog=foodservice;Integrated Security=True;Encrypt=True;TrustServerCertificate=True;Connection Timeout=30;"
    </strong>}
    ...
    </code></pre>
4. Build and run the application.
