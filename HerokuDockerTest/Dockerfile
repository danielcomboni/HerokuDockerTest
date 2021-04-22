#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
RUN pwd
COPY ["src/HerokuDockerTest/HerokuDockerTest.csproj", "HerokuDockerTest/"]

RUN pwd

RUN dotnet restore "HerokuDockerTest/HerokuDockerTest.csproj"
COPY . .

RUN pwd

WORKDIR "/src/HerokuDockerTest"

RUN pwd

RUN dotnet build "HerokuDockerTest.csproj" -c Release -o /app/build

RUN pwd

FROM build AS publish
RUN dotnet publish "HerokuDockerTest.csproj" -c Release -o /app/publish

RUN pwd

FROM base AS final
WORKDIR /app

RUN pwd

COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HerokuDockerTest.dll"]
