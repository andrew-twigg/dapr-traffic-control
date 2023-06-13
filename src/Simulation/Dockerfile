FROM mcr.microsoft.com/dotnet/sdk:7.0-bullseye-slim AS build-env
WORKDIR /source

# Copy necessary files and restore as distinct layer
COPY Simulation.csproj .
RUN dotnet restore

# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o /app Simulation.csproj

# Build runtime image
FROM mcr.microsoft.com/dotnet/runtime:7.0-bullseye-slim
WORKDIR /app
COPY --from=build-env /app .

# Start
ENTRYPOINT ["dotnet", "Simulation.dll"]
