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
