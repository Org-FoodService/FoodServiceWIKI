# 🔐 Authentication

## Authentication Domain

### Overview

The authentication domain within the FoodService application encompasses the functionalities related to user authentication, authorization, and user management. This domain ensures secure access to the application's resources by verifying the identity of users and managing their roles and permissions.

### Components

#### AuthController

The `AuthController` is responsible for handling incoming requests related to user authentication and authorization. It includes endpoints for user registration (`SignUp`), user login (`SignIn`), adding users to administrative roles (`AddUserToAdminRole`), retrieving the current user (`GetCurrentUser`), listing users (`ListUsers`), and retrieving user details (`GetUserDto`). This controller enforces authorization rules using ASP.NET Core's authorization attributes, restricting access to certain endpoints based on user roles.

#### AuthCommand

The `AuthCommand` class implements the business logic for authentication operations defined in the `IAuthCommand` interface. It delegates the execution of these operations to the `IAuthService`. The class handles user sign-up, sign-in, adding users to admin roles, retrieving the current user, listing users, and retrieving user DTOs. It encapsulates the responses using `ResponseCommon` objects to indicate the success or failure of operations.

#### AuthService

The `AuthService` class provides implementations for authentication-related operations defined in the `IAuthService` interface. It interacts with repositories, ASP.NET Identity's user manager, configuration settings, and HTTP context accessor to perform operations such as listing users, retrieving user details, updating and deleting users, user sign-up, adding users to admin roles, user sign-in, and retrieving the current user. This class utilizes ASP.NET Identity for user management and JWT authentication for generating authentication tokens.

### OpenAPI Endpoints

#### `/api/Auth/sign-up`

* **HTTP Method:** POST
* **Description:** Registers a new user.
* **Request Body:** Accepts a JSON object of type `SignUpDto`.
* **Response:** Returns a `BooleanResponseCommon` indicating the success or failure of the operation.
*   **Flowchart**:

    ```plaintext
    |--- Start
    |    |
    |    |--- Call SignUp method of AuthCommand
    |    |    |
    |    |    |--- Call SignUp method of AuthService
    |    |    |    |
    |    |    |    |--- Check if username already exists
    |    |    |    |    |
    |    |    |    |    |--- If exists, throw ArgumentException "Username already exists"
    |    |    |    |
    |    |    |    |--- Check if email already exists
    |    |    |    |    |
    |    |    |    |    |--- If exists, throw ArgumentException "Email already exists"
    |    |    |    |
    |    |    |    |--- Create a new ClientUser with the provided information
    |    |    |    |
    |    |    |    |--- Call _userManager.CreateAsync to create the user
    |    |    |    |    |
    |    |    |    |    |--- If fails, throw ArgumentException with error description
    |    |    |    |
    |    |    |    |--- Check if this is the first user
    |    |    |    |    |
    |    |    |    |    |--- If true, call _userManager.AddToRoleAsync to add the user to the Admin role
    |    |    |    |    |    |
    |    |    |    |    |    |--- If fails, throw ArgumentException "Failed to add user to admin role"
    |    |    |    |
    |    |    |    |--- Return true if signup is successful
    |    |    |
    |    |    |--- Return ResponseCommon<bool> indicating success or failure to the SignUp method of AuthCommand
    |    |
    |--- End
    ```

#### `/api/Auth/sign-in`

* **HTTP Method:** POST
* **Description:** Signs in a user.
* **Request Body:** Accepts a JSON object of type `SignInDto`.
* **Response:** Returns an `SsoDtoResponseCommon` containing the authentication token and user information.
*   **Flowchart**:

    ```plaintext
    |--- Start
    |    |
    |    |--- Call SignIn method of AuthCommand
    |    |    |
    |    |    |--- Call SignIn method of AuthService
    |    |    |    |
    |    |    |    |--- Find user by username
    |    |    |    |    |
    |    |    |    |    |--- If not found, throw ArgumentException "User not found"
    |    |    |    |
    |    |    |    |--- Check if the password is valid
    |    |    |    |    |
    |    |    |    |    |--- If invalid, throw ArgumentException "Invalid password"
    |    |    |    |
    |    |    |    |--- Retrieve user roles
    |    |    |    |
    |    |    |    |--- Create a list of authentication claims
    |    |    |    |
    |    |    |    |--- Add user roles to the authentication claims
    |    |    |    |
    |    |    |    |--- Create signing key using the secret from configuration
    |    |    |    |
    |    |    |    |--- Define token expiration time
    |    |    |    |
    |    |    |    |--- Create JWT token with the claims, signing credentials, issuer, audience, and expiration time
    |    |    |    |
    |    |    |    |--- Return SsoDto containing the token, expiration time, user roles, and user information if sign-in is successful
    |    |    |
    |    |    |--- Return ResponseCommon<SsoDto> indicating success or failure to the SignIn method of AuthCommand
    |    |
    |--- End
    ```

#### `/api/Auth/add-user-to-admin-role`

* **HTTP Method:** POST
* **Description:** Adds a user to the administrator role.
* **Request Body:** Accepts an integer representing the user ID.
* **Response:** Returns a `BooleanResponseCommon` indicating the success or failure of the operation.
*   **Flowchart**:&#x20;

    ```plaintext
    |--- Start
    |    |
    |    |--- [Authorize(Roles = "Admin")]
    |    |    |
    |    |    |--- If the user is not in the "Admin" role, return unauthorized response
    |    |
    |    |--- Call AddUserToAdminRole method of AuthCommand
    |    |    |
    |    |    |--- Call AddUserToAdminRole method of AuthService
    |    |    |    |
    |    |    |    |--- Retrieve properties of ApplicationRole that are of type bool
    |    |    |    |
    |    |    |    |--- Call AddUserToRoleAsync with userId, "Admin" role, and boolProperties
    |    |    |    |    |
    |    |    |    |    |--- If successful, return to AddUserToAdminRole method of AuthService
    |    |    |    |    |
    |    |    |    |    |--- If an error occurs, log error and throw exception
    |    |    |    |
    |    |    |    |--- Return from AddUserToAdminRole method of AuthService
    |    |    |
    |    |    |--- Return ResponseCommon<bool> indicating success or failure to AddUserToAdminRole method of AuthCommand
    |    |
    |--- End
    ```

#### `/api/Auth/get-current-user`

* **HTTP Method:** GET
* **Description:** Retrieves the currently authenticated user.
* **Response:** Returns a `UserBaseResponseCommon` containing information about the current user.
*   **Flowchart**:&#x20;

    ```plaintext
    |--- Start
    |    |
    |    |--- Call GetCurrentUser method of AuthCommand
    |    |    |
    |    |    |--- Call GetCurrentUser method of AuthService
    |    |    |    |
    |    |    |    |--- Retrieve the current user from _httpContextAccessor.HttpContext.User using _userManager.GetUserAsync
    |    |    |    |    |
    |    |    |    |    |--- If successful, return the UserBase object
    |    |    |    |    |
    |    |    |    |    |--- If an error occurs, log error and throw exception
    |    |    |    |
    |    |    |    |--- Return from GetCurrentUser method of AuthService
    |    |    |
    |    |    |--- Return ResponseCommon<UserBase> indicating success or failure to GetCurrentUser method of AuthCommand
    |    |
    |--- End
    ```

#### `/api/Auth/list-users`

* **HTTP Method:** GET
* **Description:** Lists all users.
* **Response:** Returns a `ClientUserListResponseCommon` containing a list of users.
*   **Flowchart**:

    ```plaintext
    |--- Start
    |    |
    |    |--- [Authorize(Roles = "Admin")]
    |    |    |
    |    |    |--- If the user is not in the "Admin" role, return unauthorized response
    |    |
    |    |--- Call ListUsers method of AuthCommand
    |    |    |
    |    |    |--- Call ListUsers method of AuthService
    |    |    |    |
    |    |    |    |--- Retrieve all users from _userRepository.ListAll().ToListAsync()
    |    |    |    |    |
    |    |    |    |    |--- If successful, return the list of ClientUser objects
    |    |    |    |    |
    |    |    |    |    |--- If an error occurs, log error and throw exception
    |    |    |    |
    |    |    |    |--- Return from ListUsers method of AuthService
    |    |    |
    |    |    |--- Return ResponseCommon<List<ClientUser>> indicating success or failure to ListUsers method of AuthCommand
    |    |
    |--- End
    ```

#### `/api/Auth/get-userdto`

* **HTTP Method:** GET
* **Description:** Retrieves a user DTO by ID.
* **Parameters:** Accepts an integer `id` as a query parameter.
* **Response:** Returns a `UserDtoResponseCommon` containing the user DTO.
*   **Flowchart**:

    ```plaintext
    |--- Start
    |    |
    |    |--- [Authorize(Roles = "Employee")]
    |    |    |
    |    |    |--- If the user is not in the "Employee" role, return unauthorized response
    |    |
    |    |--- Call GetUserDto method of AuthCommand
    |    |    |
    |    |    |--- Call GetUserDto method of AuthService
    |    |    |    |
    |    |    |    |--- Retrieve the user DTO by ID
    |    |    |    |    |
    |    |    |    |    |--- If successful, return the UserDto object
    |    |    |    |    |
    |    |    |    |    |--- If an error occurs, log error and throw exception
    |    |    |    |
    |    |    |    |--- Return from GetUserDto method of AuthService
    |    |    |
    |    |    |--- Return ResponseCommon<UserDto> indicating success or failure to GetUserDto method of AuthCommand
    |    |
    |--- End
    ```

### References

* [ASP.NET Core Authentication](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/)
* [ASP.NET Identity](https://docs.microsoft.com/en-us/aspnet/identity/)
* [JSON Web Tokens (JWT)](https://jwt.io/)
