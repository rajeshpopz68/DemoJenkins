
# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
 
# Copy the project file and restore dependencies
COPY PipelineDemo.csproj ./
RUN dotnet restore
 
# Copy the rest of the source code
COPY . ./
RUN dotnet publish -c Release -o /app/publish
 
# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
 
 
# Copy published output from build stage
COPY --from=build /app/publish .
 
# Expose port 5000 for the API
EXPOSE 8085
 
 
# Set environment variable for ASP.NET Core to listen on port 5000
ENV ASPNETCORE_URLS=http://+:8085
 
# Run the application
ENTRYPOINT ["dotnet", "PipelineDemo.dll"]

 
 
 