
```yml
version: "3.4"
services:
  app-api:
    container_name: AppApi
    build:
      context: .
      dockerfile: Dockerfile
    environment:
      - ASPNETCORE_URLS=http://+:5001
      - ASPNETCORE_ENVIRONMENT=Development
    depends_on:
      - app-db
    ports:
      - "5001:5001"
    networks:
      - app-network

  my-app-db:
    image: mysql:latest
    container_name: MyAppDb
    environment:
      - MYSQL_RANDOM_ROOT_PASSWORD=1
      - MYSQL_DATABASE=AppLocalDb
      - MYSQL_USER=myuser
      - MYSQL_PASSWORD=mysecretpwd!
    volumes:
      - ./.containers/database/mysqldatabase:/var/lib/mysql
    networks:
      - app-network
      
  app_seq:
    image: datalust/seq:latest
    volumes:
      - ./.containers/logs:/data
    ports:
      - 80:80
      - 5300:5341
    environment:
      - ACCEPT_EULA=Y
    networks:
      - app-network

networks:
  app-network:
  driver: bridge
```
Dockerfile for the app
```dockerfile
ARG IMG_BUILD=6.0
ARG VERSION=0.1.0
ARG PROJ_DIR=/proj
ARG DOTNETENV=Development



FROM mcr.microsoft.com/dotnet/sdk:${IMG_BUILD}-alpine AS restore
ARG PROJ_DIR

WORKDIR ${PROJ_DIR}
COPY ./*.sln .
COPY ./NuGet.config ./
COPY ./src/Namespace.Server/*.csproj ./src/Namespace.Server/
COPY ./src/Namespace.Core/*.csproj ./src/Namespace.Core/
COPY ./src/Namespace.Infrastructure/*.csproj ./src/Namespace.Infrastructure/
COPY ./src/Namespace.Client/*.csproj ./src/Namespace.Client/
COPY ./tests/Namespace.Unit.Tests/*.csproj ./tests/Namespace.Unit.Tests/

RUN dotnet --info
RUN dotnet restore 

FROM restore as build

COPY ./src/Namespace.Server/ ./src/Namespace.Server/
COPY ./src/Namespace.Core/ ./src/Namespace.Core/
COPY ./src/Namespace.Client/ ./src/Namespace.Client/
COPY ./src/Namespace.Infrastructure/ ./src/Namespace.Infrastructure/
COPY ./tests/Namespace.Unit.Tests/ ./tests/Namespace.Unit.Tests/

RUN dotnet build ./src/Namespace.Server/Namespace.Server.csproj --configuration Release

RUN dotnet restore
RUN dotnet publish src/Namespace.Server/Namespace.Server.csproj -c Release --runtime alpine-x64 -o /proj/dist --self-contained true --no-restore /p:PublishTrimmed=true

RUN dotnet build ./tests/**/*.csproj --configuration Release --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/runtime-deps:${IMG_BUILD}-alpine
ENV ASPNETCORE_URLS=http://*:8010 \
	DOTNET_RUNNING_IN_CONTAINER=true \
	DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1    


WORKDIR /app
COPY --from=build /proj/dist .
EXPOSE 8010

ENTRYPOINT ["./Namespace.Server"]
```


Other compose services examples

SqlServer
```yml
sqlserver-db:
    image: "mcr.microsoft.com/mssql/server:2017-latest"
    environment:
      ACCEPT_EULA: "Y"
      SA_PASSWORD: "changeme"
      MSSQL_PID: "Express"
    ports:
      - "1433:1433"

postgres-db:
    image: postgres:latest
    restart: always
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=changeme
      - POSTGRES_DB=mydb
    ports:
      - '5432:5432'
```