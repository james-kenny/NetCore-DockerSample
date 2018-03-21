FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY NetCore-DockerSample.sln ./
COPY NetCore-DockerSample/NetCore-DockerSample.csproj NetCore-DockerSample/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/NetCore-DockerSample
RUN dotnet build NetCore-DockerSample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCore-DockerSample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCore-DockerSample.dll"]
