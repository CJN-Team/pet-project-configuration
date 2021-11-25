#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Pet.Project.Configuration.Api/Pet.Project.Configuration.Api.csproj", "Pet.Project.Configuration.Api/"]
RUN dotnet restore "Pet.Project.Configuration.Api/Pet.Project.Configuration.Api.csproj"
COPY . .
WORKDIR "/src/Pet.Project.Configuration.Api"
RUN dotnet build "Pet.Project.Configuration.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Pet.Project.Configuration.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Pet.Project.Configuration.Api.dll"]