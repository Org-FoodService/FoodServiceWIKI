# 🔐 Authentication

## Authentication Domain in FoodService MVC Application

### Overview

The authentication domain in the FoodService MVC application is designed to handle user authentication and authorization processes. This includes user registration (sign-up), login (sign-in), managing user roles, and retrieving user information. The domain is structured to ensure secure and efficient handling of these operations, leveraging modern ASP.NET Core MVC practices and patterns.

### Key Components

#### Controllers

**AuthController**

* **Purpose**: Manages user authentication actions such as sign-up and sign-in.
* **Key Actions**:
  * `SignUp()`: Displays the sign-up page.
  * `SignUp(SignUpDto)`: Handles form submission for user registration.
  * `SignIn()`: Displays the sign-in page.
  * `SignIn(SignInDto)`: Handles form submission for user login.

#### HTTP Requests

**AuthHttpRequest**

* **Purpose**: Provides methods to make HTTP requests related to authentication.
* **Key Methods**:
  * `SignUp(SignUpDto)`: Registers a new user.
  * `SignIn(SignInDto)`: Authenticates a user and retrieves an SSO token.
  * `AddUserToAdminRole(int userId)`: Adds a user to the admin role.
  * `GetCurrentUser()`: Retrieves information about the currently authenticated user.
  * `GetUserDto(int id)`: Retrieves a user DTO by ID.
  * `ListUsers()`: Lists all users.

#### Models

**Data Transfer Objects (DTOs)**

* **SignUpDto**: Represents data required for user registration.
* **SignInDto**: Represents data required for user login.
* **SsoDto**: Represents Single Sign-On (SSO) token details.
* **UserDto**: Represents detailed user information.
* **UserBase**: Basic user information model.
* **ClientUser**: Represents user data for client-side operations.

#### Responses

**ResponseCommon**

* **Purpose**: Encapsulates the response structure for HTTP requests.
* **Attributes**:
  * `IsSuccess`: Indicates if the request was successful.
  * `Message`: Contains any error or success messages.
  * `Data`: Contains the data returned by the request.
  * `StatusCode`: HTTP status code of the response.

#### View Components

**AuthenticationStatusViewComponent**

* **Purpose**: Determines and displays the authentication status of the user in the UI.
* **Key Method**:
  * `Invoke()`: Checks if the user is logged in and returns the appropriate view.

#### Services

**AccessTokenManager**

* **Purpose**: Manages the storage and retrieval of the user's access token.
* **Key Functions**:
  * `SetAccessToken(string token, DateTime expiration, string roles)`: Stores the access token and related information.
  * `GetAccessToken()`: Retrieves the stored access token.

**LanguageService**

* **Purpose**: Provides localization services for the application.
* **Key Functions**:
  * `GetKey(string key)`: Retrieves the localized string for a given key.

### Workflow

1. **Sign-Up Process**:
   *   User navigates to the sign-up page.

       <figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
   * Submits the sign-up form with user details.
   * `AuthController.SignUp(SignUpDto)` processes the form and sends a request to `AuthHttpRequest.SignUp(SignUpDto)`.
   * If successful, the user is redirected to the sign-in page.
2. **Sign-In Process**:
   *   User navigates to the sign-in page.\


       <figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
   * Submits the sign-in form with login credentials.
   * `AuthController.SignIn(SignInDto)` processes the form and sends a request to `AuthHttpRequest.SignIn(SignInDto)`.
   * If successful, the user's token is stored using `AccessTokenManager`, and the user is redirected to the home page or profile page.
3. **User Role Management**:
   * Admin can add a user to the admin role using `AuthHttpRequest.AddUserToAdminRole(int userId)`.
4. **Retrieving User Information**:
   * Current user information can be retrieved using `AuthHttpRequest.GetCurrentUser()`.
   * Specific user details can be retrieved using `AuthHttpRequest.GetUserDto(int id)`.
5. **Displaying Authentication Status**:
   * `AuthenticationStatusViewComponent` checks if the user is authenticated and renders the appropriate UI elements (e.g., Sign-Up, Sign-In, Profile).

###
