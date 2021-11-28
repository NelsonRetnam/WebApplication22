#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WebApplication22/WebApplication22.csproj", "WebApplication22/"]
RUN dotnet restore "WebApplication22/WebApplication22.csproj"
COPY . .
WORKDIR "/src/WebApplication22"
RUN dotnet build "WebApplication22.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication22.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication22.dll"]