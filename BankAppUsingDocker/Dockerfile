FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /BankAppUsingDocker
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BankAppUsingDocker/BankAppUsingDocker.csproj", "BankAppUsingDocker/"]
RUN dotnet restore "BankAppUsingDocker/BankAppUsingDocker.csproj"
COPY . .
WORKDIR "/src/BankAppUsingDocker"
RUN dotnet build "BankAppUsingDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BankAppUsingDocker.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BankAppUsingDocker.dll"]
