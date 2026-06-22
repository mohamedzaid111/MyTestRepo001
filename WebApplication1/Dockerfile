# Stage 1: Build and publish the application
FROM ://microsoft.com AS build-env
WORKDIR /app

# Copy and restore project dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy remaining source code and build the app
COPY . ./
RUN dotnet publish -c Release -o out

# Stage 2: Create final runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .

# Expose HTTP port inside the container
EXPOSE 8080

# Run the compiled ASP.NET Core assembly
ENTRYPOINT ["dotnet", "WebApplication1.dll"]
