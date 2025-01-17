# Clean Architecture The Template

This template is designed for backend developer working with ASP.NET Core. It provides you an efficient way to build enterprise applications effortlessly by leveraging advantages of clean architecture structre and .NET Core framework.

With this template, You'll benefit from zero configuration, and don't need to worry about struture, settings,environments or best practices for web APIs,because everything is already set up :smiley:.

If you find this template helpful and learn something from it, please consider giving it a :star:. Your support motivates me to deliver even better features and improvements in future versions.

# Definition

Clean Architecture is a software design philosophy introduced by Robert C. Martin (Uncle Bob). It emphasizes the separation of concerns and promotes the organization of code into layers, each with distinct responsibilities. The architecture's primary goal is to create systems that are independent of frameworks, UI, databases, and external agencies, allowing flexibility, scalability, and testability.

At its core, Clean Architecture organizes code into concentric circles, with each layer having a specific purpose.

![Alt text](Screenshots/clean-architecture.png "clean architecture common structure")

The dependency rule states that code dependencies should only point inward, ensuring that inner layers remain isolated from external layers.

### Advandtage

- **_Seperation of Concerns_**: Each layer is responsible for a specific aspect of the application, making the code easier to understand and maintain.
- **_Testability_**: Since business logic is decoupled from frameworks and UI, unit testing becomes simpler and more reliable.
- **_Flexibility and Adaptability_**: Changes to the framework, database, or external systems have minimal impact on the core logic.
- **_Reusability_**: Business rules can be reused across different applications or systems with minimal changes.
- **_Scalability_**: The clear structure supports growth and the addition of new features without significant refactoring.
- **_Framework Independence_**: Avoids being locked into a specific framework, making it easier to migrate to newer technologies.

### Disadvandtage

- **_Complexity_**: The layered structure can add complexity, especially for smaller projects where simpler architectures might suffice.
- **_Initial Overhead_**: Setting up Clean Architecture requires additional effort to organize layers and follow strict design principles.
- **_Learning Curve_**: Developers unfamiliar with the principles may take time to grasp the structure and its benefits.
- **_Over-Engineering Risk_**: For small-scale applications, the additional layers might be unnecessary and lead to over-complication.
- **_Performance Overhead_**: The abstraction and indirection between layers can introduce slight performance trade-offs, though typically negligible.

# Structure

**_Domain_**: Domain layer serves as the core of clean architecture application and contains key elements such as:

- Aggregates : It's a way to group together related entities, value objects, enums, repository interfaces and Specfication (optional) you can learn about it at [https://github.com/ardalis/Specification](https://github.com/ardalis/Specification). With principles are established to govern the interactions between the aggregate root and its relationship and more.
- Exceptions : Create custom exceptions for domain layer.

  📁 Domain\
   ├── 📁 Aggregates\
   &emsp;&emsp;&emsp;├── 📁 AuditLogs\
   &emsp;&emsp;&emsp;├── 📁 Regions\
   &emsp;&emsp;&emsp;├── 📁 Roles\
   &emsp;&emsp;&emsp;├── 📁 Users\
   ├── 📁 Common\
   &emsp;&emsp;&emsp;├── 📁 ElasticConfigurations\
   &emsp;&emsp;&emsp;├── 📁 Specs\
   ├── 📁 Exceptions

_it is independent of any external dependencies_

**_Application_**: Application layer play a important role in clean architecture, it contains business logics and rules for your application and consist of key elements such as:

- <ins>Common folder</ins>:
  - Behaviors : Create cross-cutting concerns such as : error logging, validation, performance logging...
  - DomainEventHandler: the implementations of sending domain events.
  - Exceptions: Contain exceptions for use case.
  - Interfaces: Define interfaces for repositories and external services.
  - Mapping: Create mapping objects.
- <ins>Features folder</ins>: where I group command and query handlers together for using CQRS pattern and MediaR.

  - Common : It's my own style, I place common things of those modules such as Mapping, validations, requests and responsess and reuse it across modules.

  📁 Application\
   ├── 📁 Common\
   &emsp;&emsp;&emsp;├── 📁 Auth\
   &emsp;&emsp;&emsp;├── 📁 Behaviors\
   &emsp;&emsp;&emsp;├── 📁 DomainEventHandler\
   &emsp;&emsp;&emsp;├── 📁 Exceptions\
   &emsp;&emsp;&emsp;├── 📁 Interface\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Registers\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Services\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 UnitofWorks\
   &emsp;&emsp;&emsp;├── 📁 Mapping\
   &emsp;&emsp;&emsp;├── 📁 QueryStringProcessing\
   &emsp;&emsp;&emsp;├── 📁 Security\
   ├── 📁 Features\
   &emsp;&emsp;&emsp;├── 📁 AuditLogs\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Commands\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Queries\
   &emsp;&emsp;&emsp;├── 📁 Common\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Mapping\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Projections\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Validators\
   &emsp;&emsp;&emsp;├── 📁 Permissions\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Commands\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Queries\
   &emsp;&emsp;&emsp;├── 📁 Regions\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Commands\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Queries\
   &emsp;&emsp;&emsp;├── 📁 Roles\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Commands\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Queries\
   &emsp;&emsp;&emsp;├── 📁 Users\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Commands\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Queries\

_It only depends on domain leyer_

**_Infrastucture_** : The infrastucture layer is responsible for handling data from external sources, such as databases and web services and Consists of some key elements such as:

- <ins>Data folder</ins>:
  - Configurations : contain configurations for entity at domain layer.
  - Interceptors : Where I do logic before and after entity framework apply changes, it's an awesome feature that EF Core bring to us.
  - Migrations: contain migration files for code first
- Services : Implement external services
- UnitOfWorks: Do implementations for unit of work and repository at application layer.

  📁 Infrastructure\
   ├── 📁 Constants\
   ├── 📁 Data\
   &emsp;&emsp;&emsp;├── 📁 Configurations\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Identity\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── 📁 Regions\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── :page_facing_up: AuditLogConfiguration.cs\
   &emsp;&emsp;&emsp;&emsp;&emsp;├── :page_facing_up: DeadLetterQueueConfiguration.cs\
   &emsp;&emsp;&emsp;├── 📁 Interceptors\
   &emsp;&emsp;&emsp;├── 📁 Migrations\
   &emsp;&emsp;&emsp;├── 📁 Seeds\
   &emsp;&emsp;&emsp;├── :page_facing_up: DatabaseSettings.cs\
   &emsp;&emsp;&emsp;├── :page_facing_up: DbInitializer.cs\
   &emsp;&emsp;&emsp;├── :page_facing_up: DesignTimeDbContextFactory.cs\
   &emsp;&emsp;&emsp;├── :page_facing_up: RegionDataSeeding.cs\
   &emsp;&emsp;&emsp;├── :page_facing_up: TheDbContext.cs\
   &emsp;&emsp;&emsp;├── :page_facing_up: ValidateDatabaseSetting.cs\
   ├── 📁 Services\
   ├── 📁 UnitofWork\

_It depends on Application and Domain layer_

**_Api_**: contains api endpoints and represents for main running project in application.

    📁 Api\
        ├── 📁 Converters\
        ├── 📁 Endpoints\
        ├── 📁 Extensions\
        ├── 📁 Middlewares\
        ├── 📁 Resources\
        ├── 📁 Settings\
        ├── 📁 wwwroot\

_It depends on Application and Infrastructure layer_

**_Contract_** : contains shared components across all layers

# How to run it

The following prerequisites are required to build and run the solution:

- [Net 8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
- [Docker](https://www.docker.com/)

The first step :point_up: :

we're going to copy content of appsettings.example.json to your own appsettings.json.

Modify postgresql connection string (this template is using postgresql currently).

```json
"DatabaseSettings": {
    "DatabaseConnection": "Host=localhost;Username=[your_username];Password=[your_password];Database=example"
},
```

If you want to use difference database then just customize a few things at DependencyInjection.cs in Infrastructure layer

```csharp
    services.AddDbContextPool<TheDbContext>(
            (sp, options) =>
            {
                NpgsqlDataSource npgsqlDataSource = sp.GetRequiredService<NpgsqlDataSource>();
                options
                    .UseNpgsql(npgsqlDataSource)
                    .AddInterceptors(
                        sp.GetRequiredService<UpdateAuditableEntityInterceptor>(),
                        sp.GetRequiredService<DispatchDomainEventInterceptor>()
                    );
            }
    );
```

Simply Replace UseNpgsql with whatever database you want :smile:.

Navigate to Data folder, and then open DesignTimeDbContextFactory file

```
builder.UseNpgsql(connectionString);
```

Replace it as you did above :point_up_2:.

The next step :point_right::

change mino username and password at .env if needed and you're gonna use it for logging in Web UI Manager

`MINIO_ROOT_USER=the_template_storage
MINIO_ROOT_PASSWORD=storage@the_template1`

```
cd Dockers/Minio_S3
docker-compose up -d
```

To Run Amazon S3 service for media file storage.

This is a really good trick for using AWS for free :dollar: that I learned from my previous company :pray:

_Note that If you already have similar one You can skip this step._

Modify this json setting at your appsettings.json

```json
"S3AwsSettings": {
      "ServiceUrl": "[your_host]:9000",
      "AccessKey": "[yours]",
      "SecretKey": "[yours]",
      "BucketName": "the-template-project",
      "PublicUrl": "[your_host]:9000",
      "PreSignedUrlExpirationInMinutes": 1440,
      "Protocol": 1
    },
```

You can create access and secret key pair with Web UI manager at [http://localhost:9001](http://localhost:9001)

The final step

```
cd src/Api
dotnet run
```

"localhost:8080/docs" is swagger UI path

Congrat! you are all set up :tada: :tada: :tada: :clap:

# Basic Usage

**_Authorize_**
To Achieve this, let's add AuthorizeBy attribute on controller

```csharp
    [HttpPost(Router.UserRoute.Users)]
    [SwaggerOperation(Tags = [Router.UserRoute.Tags], Summary = "create User")]
    [AuthorizeBy(permissions: $"{ActionPermission.create}:{ObjectPermission.user}")]
    public override async Task<ActionResult<ApiResponse>> HandleAsync(
        [FromForm] CreateUserCommand request,
        CancellationToken cancellationToken = default
    )
    {
        CreateUserResponse user = await sender.Send(request, cancellationToken);
        return this.Created201(Router.UserRoute.GetRouteName, user.Id, user);
    }
```

***Create role inlcude permission***

Json payload is like
```json
{
  "description": "this is super admin role",
  "name": "superAdmin",
  "roleClaims": [
    {
      "claimType": "permission",
      "claimValue": "create:customer"
    },
    {
      "claimType": "permission",
      "claimValue": "update:customer"
    }
  ]
}
```
***How to add new permissions***

To get this, let's navigate to constants folder in Infrastructure layer, then open Credential.cs file and look at PermissionGroups Dictionary

```csharp
    public static readonly Dictionary<string, string[]> PermissionGroups =
        new()
        {
            {
                nameof(User) + "s",

                [
                    CreatePermission(ActionPermission.create, ObjectPermission.user),
                    CreatePermission(ActionPermission.update, ObjectPermission.user),
                    CreatePermission(ActionPermission.delete, ObjectPermission.user),
                    CreatePermission(ActionPermission.list, ObjectPermission.user),
                    CreatePermission(ActionPermission.detail, ObjectPermission.user),
                ]
            },
            {
                nameof(Role) + "s",

                [
                    CreatePermission(ActionPermission.create, ObjectPermission.role),
                    CreatePermission(ActionPermission.update, ObjectPermission.role),
                    CreatePermission(ActionPermission.delete, ObjectPermission.role),
                    CreatePermission(ActionPermission.list, ObjectPermission.role),
                    CreatePermission(ActionPermission.detail, ObjectPermission.role),
                ]
            },
        };
```

Notice that, the key is your entity name plus "s" and the value is list of permission for that entity.

Permission combibes from action and entity name.
For example:

```
create:user
```
Look at ActionPermission and ObjectPermission class

```csharp
public static class ActionPermission
{
    public const string create = nameof(create);
    public const string update = nameof(update);
    public const string delete = nameof(delete);
    public const string detail = nameof(detail);
    public const string list = nameof(list);
    public const string testa = nameof(testa);
}

public static class ObjectPermission
{
    public const string user = nameof(user);
    public const string role = nameof(role);
}
```
Define your new one and push it into PermissionGroups dictionary.

# Technology

- .NET 8
- EntityFramework core 8
- AutoMapper
- Fluent validation
- Medator
- XUnit, FluentAssertion, Respawn
- OpenTelemetry
- Redis
- ElasticSearch
- Serilog


# Support

If you are having problems, please let me know by

# Acknowledgements

Thank you guys so much :pray:.

- [Clean architecture by Jayson Taylor](https://github.com/jasontaylordev/CleanArchitecture)\
A fantastic guide to structuring projects with clean architecture principles, which helped shape the design of this template.

- [Clean architecture by amantinband](https://github.com/amantinband/clean-architecture)\
A concise and practical implementation of clean architecture that provided fresh perspectives and further deepened my understanding of this powerful approach.

- [Clean architecture by Ardalis](https://github.com/ardalis/CleanArchitecture)\
A thoughtful and thorough take on clean architecture that helped refine the modular structure and scalability of this template.

- [Specification pattern](https://github.com/ardalis/Specification)\
A brilliant implementation of the Specification pattern, simplifying complex query logic and promoting cleaner, more maintainable code.

- [REPR Pattern](https://github.com/ardalis/ApiEndpoints)\
A practical implementation of the Request-Endpoint-Response (REPR) pattern, which provided a clear and structured approach to organizing API endpoints. It emphasizes simplicity and single-responsibility for each endpoint, ensuring clarity and maintainability.

- [Clean testing by Jayson Taylor](https://github.com/jasontaylordev/CleanArchitecture/tree/main/tests)\
An inspiring repository of testing best practices, showcasing how to write robust and meaningful tests to ensure the reliability of clean architecture-based projects.