FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

#imagen de construcción
FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Produ.NetCoreWeb/Produ.NetCoreWeb.csproj", "Produ.NetCoreWeb/"]
RUN dotnet restore "Produ.NetCoreWeb/Produ.NetCoreWeb.csproj"
COPY . .
WORKDIR "/src/Produ.NetCoreWeb"
RUN dotnet build "Produ.NetCoreWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Produ.NetCoreWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Produ.NetCoreWeb.dll"]