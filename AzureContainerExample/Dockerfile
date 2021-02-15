#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
#WORKDIR /src
#COPY ["AzureContainerExample/AzureContainerExample.csproj", "AzureContainerExample/"]
#RUN dotnet restore "AzureContainerExample/AzureContainerExample.csproj"
#COPY . .
#WORKDIR "/src/AzureContainerExample"
#RUN dotnet build "AzureContainerExample.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "AzureContainerExample.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "AzureContainerExample.dll"]

# Get base SDK Image from Microsoft
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR /app

# Copy the CSPROJ file and restore any dependencies (via NUGET)
COPY *.csproj ./
RUN dotnet restore

# Copy the project files and build our release
COPY . ./
RUN dotnet publish -c Release -o out

# Generate runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "AzureContainerExample.dll"]

# Docker image name convention {dockerhub-id}/{project-name}:{version}
#docker build -t smileyhun/azurecontainerexample .
#docker images
#docker run -p 8080:80 -p 8081:443 smileyhun/azurecontainerexample

# List all running containers
#docker ps 
#docker stop {docker-id}


# Publish dockerfile
