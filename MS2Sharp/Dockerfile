FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MS2Sharp/MS2Sharp.csproj", "MS2Sharp/"]
RUN dotnet restore "MS2Sharp/MS2Sharp.csproj"
COPY . .
WORKDIR "/src/MS2Sharp"
RUN dotnet build "MS2Sharp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MS2Sharp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MS2Sharp.dll"]
