FROM mcr.microsoft.com/dotnet/sdk:7.0-bullseye-slim AS build-env
WORKDIR /source

# Copy necessary files and restore as distinct layer
COPY TrafficControlService.csproj .
RUN dotnet restore

# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o /app TrafficControlService.csproj

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0-bullseye-slim
WORKDIR /app
COPY --from=build-env /app .

# Expose ports
EXPOSE 6000/tcp
ENV ASPNETCORE_URLS http://*:6000

# Start
ENTRYPOINT ["dotnet", "TrafficControlService.dll"]
