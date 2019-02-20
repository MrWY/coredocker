FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY  /. /src
RUN dotnet restore
RUN dotnet build coredocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish coredocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "coredocker.dll"]
