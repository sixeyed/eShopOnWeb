FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build

WORKDIR /src
COPY ./ApplicationCore/ApplicationCore.csproj ./ApplicationCore/
COPY ./Infrastructure/Infrastructure.csproj ./Infrastructure/
COPY ./Web/Web.csproj ./Web/

RUN dotnet restore ./Web/Web.csproj

COPY . .
WORKDIR /src/Web
RUN dotnet publish -c Release -o /app

# app image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2

EXPOSE 80
WORKDIR /app
ENTRYPOINT ["dotnet", "Web.dll"]

COPY --from=build /app .
