FROM mcr.microsoft.com/dotnet/core/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS build
WORKDIR /src
COPY ["pywebapi/pywebapi.csproj", "pywebapi/"]

RUN dotnet restore "pywebapi/pywebapi.csproj"
COPY . .
WORKDIR "/src/pywebapi"
RUN dotnet build "pywebapi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "pywebapi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "pywebapi.dll"]