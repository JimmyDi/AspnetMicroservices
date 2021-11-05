#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Services/Catalog/Catelog.API/Catelog.API.csproj", "Services/Catalog/Catelog.API/"]
RUN dotnet restore "Services/Catalog/Catelog.API/Catelog.API.csproj"
COPY . .
WORKDIR "/src/Services/Catalog/Catelog.API"
RUN dotnet build "Catelog.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Catelog.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Catelog.API.dll"]
