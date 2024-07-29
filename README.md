# JWT Authorization in .NET Core Web API 6

This project demonstrates how to implement JWT (JSON Web Token) authorization in a .NET Core Web API 6 application. It includes the setup for secure endpoints using `AddSecurityRequirement`, `AddSecurityDefinition`, and service authorization.

## Features

- **JWT Authentication**: Secure your API endpoints using JWT tokens.
- **Swagger Integration**: Integrated Swagger UI with JWT authorization configuration for easy testing of secured endpoints.
- **Role-Based Authorization**: Implement role-based access control to restrict access to specific parts of the API.
- **Token Validation**: Validate JWT tokens to ensure authenticity and integrity.

## Getting Started


### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/your-username/jwt-authorization-dotnet-core-webapi6.git
    ```

2. Navigate to the project directory:
    ```bash
    cd jwt-authorization-dotnet-core-webapi6
    ```

3. Restore the dependencies:
    ```bash
    dotnet restore
    ```

4. Build the project:
    ```bash
    dotnet build
    ```

5. Run the application:
    ```bash
    dotnet run
    ```

### Configuration

1. **JWT Settings**: Update the `appsettings.json` file with your JWT settings:
    ```json
    "Jwt": {
      "Key": "your_secret_key",
      "Issuer": "your_issuer",
      "Audience": "your_audience",
      "Subject": "your_subject"
    }
    ```

2. **Swagger Configuration**: The `Startup.cs` or `Program.cs` file is configured to add JWT authentication to Swagger:
    ```csharp
    services.AddSwaggerGen(c =>
    {
        c.SwaggerDoc("v1", new OpenApiInfo { Title = "JWT Authorization API", Version = "v1" });
        c.AddSecurityDefinition("Bearer", new OpenApiSecurityScheme
        {
            Name = "Authorization",
            Type = SecuritySchemeType.ApiKey,
            Scheme = "Bearer",
            BearerFormat = "JWT",
            In = ParameterLocation.Header,
            Description = "JWT Authorization header using the Bearer scheme."
        });
        c.AddSecurityRequirement(new OpenApiSecurityRequirement
        {
            {
                new OpenApiSecurityScheme
                {
                    Reference = new OpenApiReference
                    {
                        Type = ReferenceType.SecurityScheme,
                        Id = "Bearer"
                    }
                },
                new string[] {}
            }
        });
    });
    ```

### Usage

1. **Generate Token**: Use the `/api/auth/login` endpoint to generate a JWT token by providing valid user credentials.
2. **Authorize Requests**: Include the generated token in the `Authorization` header with the `Bearer` scheme to access secured endpoints.
3. **Testing with Swagger**: Use the Swagger UI to test the API endpoints. Click on the `Authorize` button and enter the JWT token to authenticate.

### Contributing

Feel free to submit issues or pull requests if you have any improvements or fixes.




