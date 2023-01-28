FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Gefest-Vision.Monitor/Gefest-Vision.Monitor.csproj", "Gefest-Vision.Monitor/"]
RUN dotnet restore "Gefest-Vision.Monitor/Gefest-Vision.Monitor.csproj"
COPY . .
WORKDIR "/src/Gefest-Vision.Monitor"
RUN dotnet build "Gefest-Vision.Monitor.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Gefest-Vision.Monitor.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Gefest-Vision.Monitor.dll"]
