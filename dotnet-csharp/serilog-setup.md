
## Add and configure Serilop to an Asp.Net Core project

Add packages:

`dotnet add <ProjectName>.csproj package Serilog.AspNetCore -v 6.1.0`

`main.cs` code - using [two stage initialization](https://github.com/serilog/serilog-aspnetcore#two-stage-initialization):

```csharp
using Serilog;
Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateLogger();
try
{
    Log.Information("Starting web host");
    var builder = WebApplication.CreateBuilder(args);
    
     
    builder.Logging.ClearProviders();
    builder.Host.UseSerilog((context, services, configuration) =>
    {
        configuration
            .ReadFrom.Configuration(context.Configuration)
            .ReadFrom.Services(services)
            .Enrich.FromLogContext()
            .WriteTo.Console();
    });

    // other stuff...
    builder.Services.AddControllers();
    var app = builder.Build();
    app.UseHttpsRedirection();
    app.UseAuthorization();
    app.MapControllers();
    app.Run();
}
catch (Exception ex)
{
    Log.Fatal(ex, "Host terminated unexpectedly");
}
finally
{
    Log.CloseAndFlush();
}
```

More at [github serilog - getting started](https://github.com/serilog/serilog/wiki/Getting-Started)

#### Log message template

Avoid using string interpolation when logging
If using string interpolations, you’ll lose the benefits of structured logs.

`_logger.LogInformation("Getting item {Id} at {RequestTime}", id, DateTime.Now);`


[source](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/logging/) - Microsoft - Logging in .NET Core and ASP.NET Core
[source](https://code-maze.com/structured-logging-in-asp-net-core-with-serilog/) - CodeMaze - Structured Logging in ASP.NET Core with Serilog
