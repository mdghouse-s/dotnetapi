# Use the official .NET 7 SDK image as the build environment
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env

# Set the working directory in the container
WORKDIR /app

# Copy the .csproj and .nuget.config files and restore any dependencies (if applicable)
COPY *.csproj ./
COPY NuGet.Config ./

# Run the restore to download NuGet packages
RUN dotnet restore

# Copy the remaining source code to the container
COPY . .

# Build the application (you can specify the configuration here, e.g., Release)
RUN dotnet publish -c Release -o out

# Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime

# Set the working directory in the runtime container
WORKDIR /app

# Copy the published output from the build environment to the runtime container
COPY --from=build-env /app/out .

# Expose the port that your application will listen on (replace 80 with your actual port)
EXPOSE 80

# Define the entry point for your application (replace YourNamespace.YourApp.dll with your app's DLL)
ENTRYPOINT ["dotnet", "YourNamespace.YourApp.dll"]