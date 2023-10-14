# Create your own .NET CLI tool
List all available templates:
`dotnet new --list`

## Steps


### Create a console app

Create the project to be used from the cli.

### Modify the csproj file

Add the following to the csproj file:

```xml
<PropertyGroup>
    <OutoPutType>Exe</OutoPutType>
    ....
    <PackAsTool>true</PackAsTool>  // Add this
    <ToolCommandName>mytool</ToolCommandName> // Add this
    <PackageOutputPath>./nupkg</PackageOutputPath> // Add this



### Pack the project
`dotnet pack`

### Install globally (from source)
Navigate to the project folder where nupkg folder is located and run:
`dotnet tool install --global --add-source ./nupkg <App root namespace>`


### Install from nuget.org (after publishing)

`dotnet tool install --global <nuget.org App Name> --version <version>`


