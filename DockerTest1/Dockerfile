# Base image for the runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

# Build image using .NET SDK 6.0
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy project file and restore dependencies
COPY *.csproj .
RUN dotnet restore

# Copy everything else and build the app
COPY . ./
RUN dotnet publish --no-restore -c Release -o out

# Final stage - use the base runtime image
FROM base AS final
WORKDIR /app
COPY --from=build /app/out .

# Run the application
ENTRYPOINT ["dotnet", "DockerTest1.dll"]
