FROM microsoft/dotnet:2.2-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY TestApp/TestApp.csproj TestApp/
RUN dotnet restore TestApp/TestApp.csproj
COPY . .
WORKDIR /src/TestApp
RUN dotnet build TestApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TestApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestApp.dll"]
