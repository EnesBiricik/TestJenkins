# Base image for the runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY . ./
RUN dotnet restore --verbosity minimal
RUN dotnet publish -c Release -o /app --no-restore --verbosity minimal
FROM base AS final
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "DockerTest1.dll"]