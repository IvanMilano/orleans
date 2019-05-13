#FROM microsoft/aspnetcore:2.2 AS base
FROM mcr.microsoft.com/dotnet/core/runtime:2.2 AS base
WORKDIR /app

#FROM microsoft/aspnetcore-build:2.2 AS build
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY *.sln ./
COPY Silo/Silo.csproj Silo/
COPY Directory.Build.props .
RUN dotnet restore
COPY . .
WORKDIR /src/Silo
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Silo.dll"]
