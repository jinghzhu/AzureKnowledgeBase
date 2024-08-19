# <center>Microsoft Authentication Library (MSAL)</center>

<br></br>



## What
The Microsoft Authentication Library (MSAL) enables developers to acquire tokens from Microsoft identity platform in order to authenticate users and access secured web APIs. It can be used to provide secure access to Microsoft Graph, other Microsoft APIs, or your own web API. MSAL supports different architectures and platforms including .NET, JavaScript, Java, Python, Android, and iOS.

Using MSAL provides the following benefits:
- No need to directly use the OAuth libraries or code against the protocol in your application.
- Acquires tokens on behalf of a user or on behalf of an application (when applicable to the platform).
- Maintains a token cache and refreshes tokens for you when they're close to expire. You don't need to handle token expiration on your own.
- Helps you specify which audience you want your application to sign in.
- Helps you set up your application from configuration files.
- Helps you troubleshoot your app by exposing actionable exceptions, logging, and telemetry.

<br>


### Public client, and confidential client applications
Multiple types of applications can acquire security tokens. These applications tend to be separated into the following two categories. Each is used with different libraries and objects.

1. Public client applications: Are apps that run on devices or desktops or in a web browser. They're not trusted to safely keep application secrets, so they only access web APIs on behalf of user. (They support only public client flows.) Public clients can't hold configuration-time secrets, so they don't have client secrets.

2. Confidential client applications: Are apps that run on servers (web apps, web API apps, or even service/daemon apps). They're considered difficult to access, and for that reason capable of keeping an application secret. It can hold configuration-time secrets. Each instance of the client has a distinct configuration (including client ID and client secret).

<br></br>



## Exercise
### Initialize client applications
The recommended way to instantiate an application is by using the application builders: `PublicClientApplicationBuilder` and `ConfidentialClientApplicationBuilder`. Before initializing an application, you first need to register it so that app can be integrated with Microsoft identity platform. After registration, you may need following information (which can be found in portal):
- Client ID (a string representing a GUID)
- Identity provider URL (named the instance) and the sign-in audience for your application. These two parameters are collectively known as authority.
- Tenant ID if you're writing a line of business application solely for your organization (also named single-tenant application).
- Application secret (client secret string) or certificate (of type X509Certificate2) if it's a confidential client app.
- For web apps, and sometimes for public client apps (in particular when app needs to use a broker), you have to set `redirectUri` where identity provider connects back to your application with security tokens.

<br>


#### Initializing public and confidential client applications from code
The following code instantiates a public client application, signing-in users in Azure, with their work and school accounts, or their personal Microsoft accounts.

```csharp
IPublicClientApplication app = PublicClientApplicationBuilder.Create(clientId).Build();
```

The following code instantiates a confidential application (a Web app located at `https://myapp.azurewebsites.net`) handling tokens from users in Azure, with their work and school accounts, or their personal Microsoft accounts. The application is identified with the identity provider by sharing a client secret:

```csharp
string redirectUri = "https://myapp.azurewebsites.net";
IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(clientId)
    .WithClientSecret(clientSecret)
    .WithRedirectUri(redirectUri )
    .Build();
```

<br>


#### Builder modifiers
In the code snippets using application builders, `.With` methods can be applied as modifiers (for example, `.WithAuthority` and `.WithRedirectUri`).

- `.WithAuthority` modifier: sets the application default authority to a Microsoft Entra authority, with possibility of choosing Azure Cloud, the audience, the tenant (tenant ID or domain name), or providing directly the authority URI.

    ```csharp
    var clientApp = PublicClientApplicationBuilder.Create(client_id)
        .WithAuthority(AzureCloudInstance.AzurePublic, tenant_id)
        .Build();
    ```

- `.WithRedirectUri` modifier: overrides the default redirect URI.
    
    ```csharp
    var clientApp = PublicClientApplicationBuilder.Create(client_id)
        .WithAuthority(AzureCloudInstance.AzurePublic, tenant_id)
        .WithRedirectUri("http://localhost")
        .Build();
    ```

<br>


### Implement interactive authentication
First, register a new app:
1. In the portal, search for and select Microsoft Entra ID.
2. Under Manage, select App registrations > New registration.

Next, add code for interactive authentication:
1. Ned two variables to hold the Application (client) and Directory (tenant) IDs. You can copy those values from portal. Add the following code and replace the string values with the appropriate values from portal.

    ```csharp
    private const string _clientId = "APPLICATION_CLIENT_ID";
    private const string _tenantId = "DIRECTORY_TENANT_ID";
    ```

2. Use `PublicClientApplicationBuilder` class to build out authorization context.

    ```csharp
    var app = PublicClientApplicationBuilder
        .Create(_clientId)
        .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
        .WithRedirectUri("http://localhost")
        .Build();
    ```

Now, we need acquire a token. When registered the `az204appreg` app, it automatically generated an API permission `user.read` for Microsoft Graph. You use that permission to acquire a token.

1. Set permission scope for token request. Add following code below `PublicClientApplicationBuilder`.

    ```csharp
    string[] scopes = { "user.read" };
    ```

2. Add code to request the token and write result to console.

    ```chsarp
    AuthenticationResult result = await app.AcquireTokenInteractive(scopes).ExecuteAsync();
    Console.WriteLine($"Token:\t{result.AccessToken}");
    ```

The `Program.cs` should resemble the following:

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Identity.Client;

namespace az204_auth
{
    class Program
    {
        private const string _clientId = "APPLICATION_CLIENT_ID";
        private const string _tenantId = "DIRECTORY_TENANT_ID";

        public static async Task Main(string[] args)
        {
            var app = PublicClientApplicationBuilder
                .Create(_clientId)
                .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
                .WithRedirectUri("http://localhost")
                .Build(); 
            string[] scopes = { "user.read" };
            AuthenticationResult result = await app.AcquireTokenInteractive(scopes).ExecuteAsync();

            Console.WriteLine($"Token:\t{result.AccessToken}");
        }
    }
}
```

After running the app, you should see

![](./Images/msal_example1.png)

You should alsosee the results similar to the example below in the console.

```
Token:  eyJ0eXAiOiJKV1QiLCJub25jZSI6IlVhU.....
```

<br></br>
