### Command Line basics

##### Create a new database migration
Create new migration:
`dotnet ef migrations add <NameOfMigration>`

Undo last migraton:
`dotnet ef migrations remove <NameOfMigration>`

##### Update database
`dotnet ef database update`

### Command Line with Entity Framework in separate class library
#### Create a new database migration
Create new migration:
```
dotnet ef migrations add {NameOfMigration} --project src\Namespace.ClassLibraryName --startup-project src\Namespace.StartupProjectName --output-dir Persistence\Migrations
```
Undo last migraton:
```
dotnet ef migrations remove --project src\Namespace.ClassLibraryName --startup-project src\Namespace.StartupProjectName
```
#### Update database
```
dotnet ef database update --startup-project src\Namespace.StartupProjectName --project src\Namespace.ClassLibraryName
```


### Visual Studio PM Console

##### Create a new database migration
Create new migration:
PM> `add-migration <NameOfMigration>`

##### Update database
PM> `update-database`