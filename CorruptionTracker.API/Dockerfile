FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["CorruptionTracker.API/CorruptionTracker.API.csproj", "CorruptionTracker.API/"]
RUN dotnet restore "CorruptionTracker.API/CorruptionTracker.API.csproj"
COPY . .
WORKDIR "/src/CorruptionTracker.API"
RUN dotnet build "CorruptionTracker.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CorruptionTracker.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CorruptionTracker.API.dll"]