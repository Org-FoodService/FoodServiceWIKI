# 📒 Logging Implementation

Logging plays a crucial role in monitoring the health and behavior of an application. In FoodServiceAPI, logging has been implemented using the Serilog library, ensuring that important information, warnings, and errors are captured efficiently. Below are the key points regarding the logging implementation:

### Serilog Integration

#### Library

The Serilog library is utilized for logging, offering robust capabilities and flexibility in log management.

#### Log Destinations

* **Console**: Logs are written to the console, providing real-time visibility during application runtime.
* **File**: Log files are generated in the `Logs` folder with a rolling interval of a day, ensuring organized and manageable log storage.
*   **Serilog Seq Server**: Logs are ingested into a Serilog Seq server (`http://localhost:5341/`), facilitating centralized log management and dashboard support for better visibility and analysis.

    <figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### Logging Configuration

**Minimum Log Level**

* The default log level is set to "Information".
* Specific log levels for Microsoft-related components are also set to "Information".

**Log Enrichment**

Enrichment properties include:

* `FromLogContext`
* `WithMachineName`
* `WithThreadId`

These properties provide additional context to logs.

#### Docker Container for Serilog Seq Server

To streamline the setup process, code to start the Docker container for the Serilog Seq server is added in `Program.cs`. This code ensures that the Seq server is available for logging, executing only once during the initial deployment if no server is already available.

#### Docker Engine Requirement

Running the logging feature with Serilog Seq Server requires [Docker to be installed](../first-steps/installing-docker.md) and running on the host machine. Ensure Docker is properly configured and accessible for seamless integration with the logging setup. While Docker is not crucial for running the application, without it, the application will not have all the logging functionalities, such as centralized log management and enhanced dashboard support provided by the Seq server.

### Sensitive Data Logging

Logging request and response data can sometimes expose sensitive information. To mitigate this risk, the following practices are implemented:

#### Middleware Replacement

Instead of using middlewares for logging request/response, use `IAsyncActionFilter`.

#### Property Exclusion

Use the NuGet package [Destructurama.Attributed](https://github.com/destructurama/attributed) to exclude specific properties from being logged.

#### Implementation

* **Attribute Usage**: Apply the `[NotLogged]` attribute on class properties that should not be logged.

#### Example

```csharp
public class RequestDTO
{
    public string UserName { get; set; }
    
    [NotLogged]
    public string Password { get; set; }
}
```

In this example, the `Password` property will not be logged, ensuring that sensitive details are not exposed.

### Summary

Logging serves as a critical component in maintaining the health and performance of FoodServiceAPI, enabling efficient troubleshooting and proactive monitoring of the application's behavior. By integrating Serilog, setting up proper log destinations, configuring log levels, enriching logs with context, and securely handling sensitive data, we ensure a robust and efficient logging system.
