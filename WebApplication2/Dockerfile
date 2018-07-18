FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 62815
EXPOSE 44312

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY WebApplication2/WebApplication2.csproj WebApplication2/
RUN dotnet restore WebApplication2/WebApplication2.csproj
COPY . .
WORKDIR /src/WebApplication2
RUN dotnet build WebApplication2.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplication2.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication2.dll"]
