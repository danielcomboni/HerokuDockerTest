#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
RUN pwd
COPY ["src/HerokuDockerTest/HerokuDockerTest.csproj", "HerokuDockerTest/"]

RUN pwd #1

RUN dotnet restore "HerokuDockerTest/HerokuDockerTest.csproj"
COPY . .

RUN pwd #2

WORKDIR "/src/HerokuDockerTest"

RUN pwd #3

RUN dotnet build "HerokuDockerTest.csproj" -c Release -o /app/build

RUN pwd #4

FROM build AS publish
RUN dotnet publish "HerokuDockerTest.csproj" -c Release -o /app/publish

RUN pwd #5

FROM base AS final
WORKDIR /app

RUN pwd #6

COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HerokuDockerTest.dll"]
