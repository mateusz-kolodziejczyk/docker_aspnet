FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["docker_aspnet.csproj", "docker_aspnet/"]
RUN dotnet restore "docker_aspnet/docker_aspnet.csproj"
WORKDIR "/src/docker_aspnet"
COPY . .
RUN dotnet build "docker_aspnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "docker_aspnet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "docker_aspnet.dll"]
