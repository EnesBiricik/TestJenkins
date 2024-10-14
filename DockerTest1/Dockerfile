# Base image for the runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

# Build environment
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy project files and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the entire source code and publish the application
COPY . ./
RUN dotnet publish --no-restore -c Release -o out

# Final stage for running the application
FROM base AS final
WORKDIR /app
COPY --from=build-env /app/out ./
ENTRYPOINT ["dotnet", "DockerTest1.dll"]
