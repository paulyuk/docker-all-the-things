FROM mcr.microsoft.com/dotnet/core/runtime:2.1-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["pywebfront.Test/pywebfront.Test.csproj", "pywebfront.Test/"]
COPY ["pywebfrontend/pywebfrontend.csproj", "pywebfrontend/"]
RUN dotnet restore "pywebfront.Test/pywebfront.Test.csproj"
COPY . .
WORKDIR "/src/pywebfront.Test"
RUN dotnet build "pywebfront.Test.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "pywebfront.Test.csproj" -c Release -o /app

FROM publish AS test
WORKDIR /app
COPY . .
RUN dotnet test

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "pywebfront.Test.dll"]