#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/services/WDSystem.WorldPremios.Identidade.API/WDSystem.WorldPremios.Identidade.API.csproj", "src/services/WDSystem.WorldPremios.Identidade.API/"]
RUN dotnet restore "src/services/WDSystem.WorldPremios.Identidade.API/WDSystem.WorldPremios.Identidade.API.csproj"
COPY . .
WORKDIR "/src/src/services/WDSystem.WorldPremios.Identidade.API"
RUN dotnet build "WDSystem.WorldPremios.Identidade.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WDSystem.WorldPremios.Identidade.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WDSystem.WorldPremios.Identidade.API.dll"]