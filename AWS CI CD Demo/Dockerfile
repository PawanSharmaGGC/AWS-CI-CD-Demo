# Build stage
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src

# Copy project file and restore dependencies
COPY ["AWS CI CD Demo.csproj", "./"]

RUN dotnet restore "AWS CI CD Demo.csproj"

# Copy source code
COPY . .

# Build and publish application
RUN dotnet publish "AWS CI CD Demo.csproj" \
    -c Release \
    -o /app/publish \
    /p:UseAppHost=false


# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final

WORKDIR /app

# Application listens on port 8080
ENV ASPNETCORE_HTTP_PORTS=8080

EXPOSE 8080

# Copy published application
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "AWS CI CD Demo.dll"]