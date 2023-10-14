## Logging into Elasticserach with Serilog and viewing logs with Kibana

Example app using default Asp.Net Core 7 Web Api template with Serilog, Elasticsearch and Kibana running in dockr containers.
---
NOTE - Issue with Elastsearch container: Failing with error Max virtual memory areas vm.max_map_count 65530 is too low, increase to at least 262144:
https://stackoverflow.com/questions/51445846/elasticsearch-max-virtual-memory-areas-vm-max-map-count-65530-is-too-low-inc

For MS Windows users, using wsl subsystem. Open powershell, run:

`wsl -d docker-desktop`
then
`sysctl -w vm.max_map_count=262144`
---

Add dummy exception trigger to WeatherForecastController.cs

```csharp
[HttpGet(Name = "GetWeatherForecast")]
    public IActionResult Get()
    {
        try
        {
            if (Random.Shared.Next(0, 5) < 2)
            {
                throw new Exception("Oops, what happened?");
            }
        
            return Ok(Enumerable.Range(1, 5).Select(index => new WeatherForecast
                {
                    Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
                    TemperatureC = Random.Shared.Next(-20, 55),
                    Summary = Summaries[Random.Shared.Next(Summaries.Length)]
                })
                .ToArray());
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Something bad happened");
            return new StatusCodeResult(500);
        }
    }
```

Nuget packages:
 `Serilog.AspNetCore`, `Serilog.Sinks.Elasticsearch` and `Serilog.Enrichers.Environment`

Dcoker compose file:

```yaml
version: "3.4"
services:
  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.9.0
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=es-docker-cluster
      - cluster.initial_master_nodes=es01
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data01:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - elastic

  kib01:
    image: docker.elastic.co/kibana/kibana:7.9.0
    container_name: kib01
    ports:
      - 5601:5601
    environment:
      ELASTICSEARCH_URL: http://es01:9200
      ELASTICSEARCH_HOSTS: http://es01:9200
    networks:
      - elastic
volumes: 
    data01:
        driver: local
        
networks:
  elastic:
    driver: bridge
```

Appsettings.json:
    
```json
{
  "Serilog": {
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Information",
        "System": "Warning"
      }
    }
  },
  "AllowedHosts": "*"
}
```

Program.cs:

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

builder.Logging.ClearProviders();
builder.Host.UseSerilog((context, services, configuration) =>
{
    configuration
        .Enrich.FromLogContext()
        .Enrich.WithMachineName()
        .WriteTo.Console()
        .WriteTo.Elasticsearch(
            new ElasticsearchSinkOptions(new Uri(context.Configuration["ElasticConfiguration:Uri"]))    
            {
                AutoRegisterTemplate = true,
                AutoRegisterTemplateVersion = AutoRegisterTemplateVersion.ESv7,
                IndexFormat = $"{context.Configuration["ApplicationName"]}-logs-{context.HostingEnvironment.EnvironmentName?.ToLower().Replace(".", "-") ?? "development"}-{DateTime.UtcNow:yyyy-MM}",
                NumberOfShards = 2,
                NumberOfReplicas = 1
            })
        .Enrich.WithProperty("Environment", context.HostingEnvironment.EnvironmentName)
        .ReadFrom.Configuration(context.Configuration);
});

builder.Services.AddControllers();
```

- Run application and run docker compose up to start Elasticsearch and Kibana containers.
- Open localhost:5601 in browser to view Kibana. Navigate to Manage Spaces: http://localhost:5601/app/management/
- Click Index Patterns and create new index pattern. An index with name based on Elasticsearch sink options in Program.cs should be visible (eg elasticserachlogs.api-logs-development-2023-08).

- Add pattern name based on the index name (eg elasticserachlogs.api-logs-*) and click next.
- Select Timefield @timestamp and click create index pattern.
- Navigate to http://localhost:5601/app/discover to view logs. Filter on e.g levl: level:Error to view only error logs.


[source - demo source code](https://github.com/OysteinBruin/ElasticsearchLogs)
[source - youtube](https://www.youtube.com/watch?v=0acSdHJfk64&t=20s)
